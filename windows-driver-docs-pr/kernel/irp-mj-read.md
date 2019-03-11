---
title: IRP_MJ_READ
description: 将数据从其设备传输到系统每个设备驱动程序必须处理 DispatchRead 或 DispatchReadWrite 例程中的读取的请求，因为必须上层的此类设备驱动程序的任何更高级别的驱动程序。
ms.date: 08/12/2017
ms.assetid: 5ae4c6c5-d8f2-4dc5-8cfd-ecb751fc88be
keywords:
- IRP_MJ_READ Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: fee47dc083df75a8e15a89a55e9563c2274c4f9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544458"
---
# <a name="irpmjread"></a>IRP\_MJ\_READ


将数据从其设备传输到系统每个设备驱动程序必须处理中的读取的请求[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)或[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程，必须为任何更高级别的驱动程序上层的此类设备驱动程序。

<a name="when-sent"></a>发送时间
---------

每当创建请求在成功完成后。

可能是用户模式应用程序或具有表示目标设备对象的文件对象的句柄的 Win32 组件已请求数据传输从设备。 可能是更高级别的驱动程序已创建并设置了读取 IRP。

## <a name="input-parameters"></a>输入参数


驱动程序的 I/O 堆栈位置中 IRP 指示在传输的字节数**Parameters.Read.Length**。

某些驱动程序使用处的值**Parameters.Read.Key**排序传入的读取的请求到设备队列中或驱动程序管理的 Irp 的内部队列中以驱动程序确定的顺序。

某些类型的驱动程序还使用处的值**Parameters.Read.ByteOffset**，指示在传输操作的起始偏移量。 有关示例，请参阅[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff549327)可安装文件系统 (IFS) 文档中的主题。

## <a name="output-parameters"></a>输出参数


具体取决于基础设备驱动程序是否设置了目标设备对象的**标志**使用\_缓冲\_IO 或使用\_直接\_IO，数据传输到其中一个以下内容：

-   在缓冲区**Irp-&gt;AssociatedIrp.SystemBuffer**如果驱动程序将使用缓冲的 I/O。

-   描述在 MDL 缓冲区**Irp-&gt;MdlAddress**如果基础设备驱动程序使用 （DMA 或 PIO） 的直接 I/O。

<a name="operation"></a>操作
---------

接收的读取请求时，更高级别的驱动程序设置中的下一步较低的驱动程序，IRP 的 I/O 堆栈位置或它会创建并设置其他 Irp 的一个或多个较低的驱动程序。 可以设置其[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，这是可选的输入 IRP，但所需的驱动程序创建 Irp，通过调用[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679). 然后，该驱动程序将传递到下一步低驱动程序和请求[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。

接收到的读取请求，将设备驱动程序将数据从传输其设备到系统内存。 设备驱动程序集**信息**时完成 IRP，传输的 I/O 状态块的字节数的字段。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)

 

 



