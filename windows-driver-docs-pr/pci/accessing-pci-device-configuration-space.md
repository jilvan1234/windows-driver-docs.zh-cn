---
title: 访问 PCI 设备配置空间
description: 访问 PCI 设备配置空间
ms.assetid: 05e0ada9-d465-4787-abc5-469a75352ee0
keywords:
- PCI 配置空间 WDK 总线
- 配置空间 WDK 总线
- IRP_MN_READ_CONFIG
- IRP_MN_WRITE_CONFIG
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6dddd28faeddcb591bc4ee1218c4008b59e2fea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837734"
---
# <a name="accessing-pci-device-configuration-space"></a>访问 PCI 设备配置空间


外围组件互连（PCI）设备上的某些操作是为设备的功能驱动程序预留的。 例如，此类操作包括访问总线的设备特定配置空间和对直接内存访问（DMA）控制器进行编程。 Microsoft 通过两种方法为访问 PCI 设备的配置空间提供系统支持：

-   [**总线\_接口\_标准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)总线接口

-   配置 i/o 请求数据包（Irp）、 [**IRP\_MN\_读取\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-read-config)和[**IRP\_MN\_写入\_配置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-write-config)

Windows XP 和 Windows Server 2003 及更高版本的操作系统可以独占控制*PCI 本地总线*规范定义的配置空间标头以及功能链接列表中的所有功能。 驱动程序不得尝试修改这些寄存器。

但是，驱动程序可以使用 IRP\_MN\_写入\_CONFIG 请求或总线的**SetBusData**方法，写入不属于该标头或供应商定义的功能列表的配置空间\_INTERFACE\_STANDARD。 驱动程序还可以使用 IRP\_MN\_读取\_CONFIG 请求或总线\_接口的**GetBusData**方法\_STANDARD 中读取设备的功能。 若要使用 IRP\_MN\_读取\_CONFIG 或 IRP\_MN\_写入\_配置，驱动程序必须在被动\_级别运行。 有关驱动程序可以查询的功能列表和相应结构，请参阅[PCI 结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)部分。

驱动程序可以使用 IRP\_MN\_读取\_CONFIG 请求或总线\_接口的**GetBusData**方法，从扩展的 PCI 设备配置空间（也就是超过256字节的配置数据）进行读取\_标准. 同样，驱动程序可以使用 IRP\_MN\_写入\_CONFIG 请求或总线\_接口的**SetBusData**方法\_STANDARD 来写入扩展 PCI 设备配置空间。 如果设备没有扩展配置空间或平台未定义设备上扩展配置空间的路径，则读取请求将返回0xFFFF 并且写入请求将不起作用。 若要确定操作是否成功，驱动程序可以检查读取或写入的字节数。

PCI Express 和 PCI-X 模式2支持大于256个字节的扩展 PCI 设备配置空间。 驱动程序可以读取和写入此配置空间，但仅支持相应的硬件和 BIOS 支持。 在 ACPI BIOS 中，根总线必须具有 PNP0A08 或 PNP0A03 的 PNP ID。 对于 PNP ID 为 PNP0A03 的根总线，具有函数4的 \_DSM 方法应指示当前模式为 PCI-X 模式2。 所有桥和设备都应为 PCI express，或在 PCI-X 模式2中运行。

此外，系统应支持内存映射配置空间访问。 这是通过在系统 BIOS/固件中定义 MCFG 表。 Windows Vista 和 Windows Server 2008 及更高版本的操作系统会自动支持内存映射配置空间访问。

下面的代码示例演示如何查询设备的电源管理功能数据：

```cpp
#define LSZ sizeof(ULONG)
#define HEADERSIZE (FIELD_OFFSET (PCI_COMMON_CONFIG, DeviceSpecific)) / LSZ

 // The PCI_COMMON_CONFIG structure includes 
// device specific data. The following
// structure is used to retrieve the
// 64 bytes of data that precedes the
// device-specific data.

typedef struct {
    ULONG  Reserved[HEADERSIZE];
} PCI_COMMON_HEADER, *PPCI_COMMON_HEADER;

PCI_COMMON_HEADER Header;
PCI_COMMON_CONFIG *pPciConfig = (PCI_COMMON_CONFIG *)&Header;
// declare power management capabilities header
 PCI_PM_CAPABILITY  PowerMgmtCapability;
PCI_PM_CAPABILITY  *pPowerMgmtCapability = &Capability; 
UCHAR CapabilityOffset;

// Read the first part of the header
// to get the status register and
// the capabilities pointer.
// The "capabilities pointer" is
// actually an offset from the
// beginning of the header to a
// linked list of capabilities.
BusInterface.GetBusData(Context,
    PCI_WHICHSPACE_CONFIG,
    pPciConfig, // output buffer
    0, // offset of the capability to read
 sizeof(PCI_COMMON_HEADER)); // just 64 bytes

// Check the Status register to see if 
// this device supports capability lists.
 
if ((pPciConfig->Status &
   PCI_STATUS_CAPABILITIES_LIST) == 0) {
   // does not support capabilities list
   return(STATUS_NOT_IMPLEMENTED);
}

// The device supports capability lists.
// Find the capabilities.

// The position of the capabilities pointer
// in the header depends on whether this is 
// a bridge type device. Check the type.

if ((pPciConfig->HeaderType & 
   (~PCI_MULTIFUNCTION)) == PCI_BRIDGE_TYPE) {
   CapabilityOffset = 
       pPciConfig->u.type1.CapabilitiesPtr;
} else if ((pPciConfig->HeaderType & 
   (~PCI_MULTIFUNCTION)) == PCI_CARDBUS_TYPE) {
   CapabilityOffset = 
       pPciConfig->u.type2.CapabilitiesPtr;
} else {
   CapabilityOffset = 
       pPciConfig->u.type0.CapabilitiesPtr;
}

// Loop through the capabilities in search
// of the power management capability. The
// list is NULL-terminated, so the last 
// offset will always be zero.

while (CapabilityOffset != 0) {

    // Read the header of the capability at 
    // this offset.

    // If the retrieved capability is not
    // the power management capability that
    // we are looking for, follow the
    // link to the next capability and
    // continue looping.

    BusInterface.GetBusData(Context,
        PCI_WHICHSPACE_CONFIG,
        pPowerMgmtCapability,
        CapabilityOffset,
        sizeof(PCI_CAPABILITIES_HEADER));

    if (Capability->Header.CapabilityID ==
 PCI_CAPABILITY_ID_POWER_MANAGEMENT) {
        // Found the power management capability
        break;
    } else {
        // This is some other capability.
        // Keep looking for the power 
        // management capability.
        CapabilityOffset = Capability->Header.Next;
    }
}

if (CapabilityOffset == 0) {
    // We didn't find a power management
    // capability. Return an error.
    return(STATUS_NOT_IMPLEMENTED);
}

// Skip past the capabilities header and read
// the rest of the power management capability

BusInterface.GetBusData(Context,
   PCI_WHICHSPACE_CONFIG,
   // write to location immediately following header
   & (pPowerMgmtCapability->Header) + 1, 
   CapabilityOffset + 
       sizeof(PCI_CAPABILITIES_HEADER),
   sizeof(PCI_PM_CAPABILITY) - 
       sizeof(PCI_CAPABILITIES_HEADER)
);
```

 

 




