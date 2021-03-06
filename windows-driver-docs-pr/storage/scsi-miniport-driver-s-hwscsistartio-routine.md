---
title: SCSI 微型端口驱动程序的 HwScsiStartIo 例程
description: SCSI 微型端口驱动程序的 HwScsiStartIo 例程
ms.assetid: cb818e5f-b91f-44cb-972b-22f75459edeb
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- 传入的 I/O 请求 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0244f798a433b05f5cb46fb9b523addfb991c931
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386496"
---
# <a name="scsi-miniport-drivers-hwscsistartio-routine"></a>SCSI 微型端口驱动程序的 HwScsiStartIo 例程


## <span id="ddk_scsi_miniport_drivers_hwscsistartio_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSISTARTIO_ROUTINE_KG"></span>


顾名思义， [ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程是传入的请求上 HBA 驱动 bus(es) 外围设备的入口点。 *HwScsiStartIo*每个 HBA 状态使用 SCSI 请求块 (SRB) 和微型端口驱动程序的设备扩展的指针调用。 有关语法的此例程，请参阅**HwScsiStartIo**。

如果微型端口驱动程序**DriverEntry**例程也被请求的内存分配逻辑单元扩展 (请参阅[调用 ScsiPortInitialize](calling-scsiportinitialize.md))，则*HwScsiStartIo*例程调用**ScsiPortGetLogicalUnit**用输入的设备扩展指针并**PathId**， **TargetId**，和**Lun**输入 SRB 中的值。

如果**DriverEntry**例程请求的内存分配 SRB 扩展**SrbExtension**中每个 SRB 成员包含微型端口驱动程序的每个请求存储区域的指针。 请注意微型端口驱动程序必须请求的内存分配给**SrbExtension**s 如果维护每个请求的状态信息。 它不能使用 SRB 实现此目的。

 

 




