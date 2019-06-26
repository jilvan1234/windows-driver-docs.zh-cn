---
title: DEVPKEY_Device_DevType
description: DEVPKEY_Device_DevType
ms.assetid: acbc0d6f-96e7-4e7c-acc3-d4cded2080d7
keywords:
- DEVPKEY_Device_DevType 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DevType
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9cfe18d5b50b5028e9917369ab7cc0b62673df4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382924"
---
# <a name="devpkeydevicedevtype"></a>DEVPKEY_Device_DevType


DEVPKEY_Device_DevType 设备属性表示设备实例的设备的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DevType</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_DEVTYPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 的设备类型成员的值设置的值 DEVPKEY_Device_DevType [ **DEVICE_OBJECT** ](https://msdn.microsoft.com/library/windows/hardware/ff543147)设备实例结构。 DEVPKEY_Device_DevType 的值是中列出的系统定义的设备类型值之一[指定设备类型](https://msdn.microsoft.com/library/windows/hardware/ff563821)。

可以使用设置的值 DEVPKEY_Device_DevType [ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)包含在[ **INF *DDInstall*。硬件部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)安装设备的 INF 文件中。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_DevType 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_DevType 属性键。 相反，相应的 SPDRP_DEVTYPE 标识符可用于访问这些早期版本的 Windows 上的属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://msdn.microsoft.com/library/windows/hardware/ff537737)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVICE_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff543147)

[**INF *DDInstall*。硬件部分**](https://msdn.microsoft.com/library/windows/hardware/ff547330)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 





