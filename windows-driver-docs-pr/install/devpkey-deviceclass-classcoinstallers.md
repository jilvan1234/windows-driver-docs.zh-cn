---
title: DEVPKEY_DeviceClass_ClassCoInstallers
description: DEVPKEY_DeviceClass_ClassCoInstallers
ms.assetid: c1369006-5329-48c7-afe0-ddce44889bbc
keywords:
- DEVPKEY_DeviceClass_ClassCoInstallers 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_ClassCoInstallers
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aa225fade9b9efd4be7a01954a10434a04c72032
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362992"
---
# <a name="devpkeydeviceclassclasscoinstallers"></a>DEVPKEY_DeviceClass_ClassCoInstallers


DEVPKEY_DeviceClass_ClassCoInstallers 设备属性表示的类共同安装程序安装了一系列[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_ClassCoInstallers</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据格式</strong></p></td>
<td align="left"><p>"<em>coinstaller1.dll</em>,<em>coinstaller1-entry-point</em>\0…<em>coinstallerN.dll</em>,<em>coinstallerN-entry-point</em>\0\0"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入访问权限通过安装应用程序和安装程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>相应的注册表值名称</strong></p></td>
<td align="left"><p><strong>HLM\System\CurrentControlSet\Control\CoDeviceInstallers{</strong><em>device-setup-class-guid</em><strong>}</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

类共同安装程序列表中的每个类安装程序都由其 DLL 和入口点标识。

有关如何安装类共同安装程序的信息，请参阅[注册类共同安装程序](https://docs.microsoft.com/windows-hardware/drivers/install/registering-a-class-co-installer)。

可以通过调用检索的值 DEVPKEY_DeviceClass_ClassCoInstallers [ **SetupDiGetClassProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)或[ **SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw). 可以通过调用设置 DEVPKEY_DeviceClass_ClassCoInstallers [ **SetupDiSetClassProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)或[ **SetupDiSetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw).

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_DeviceClass_ClassCoInstallers 属性键。 有关如何访问这些早期版本的 Windows 上的相应信息的信息，请参阅[访问的设备安装程序类将共同安装程序注册表项值](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-the-co-installers-registry-entry-value-of-a-device-setup-cla)。

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


[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

[**SetupDiSetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)

 

 






