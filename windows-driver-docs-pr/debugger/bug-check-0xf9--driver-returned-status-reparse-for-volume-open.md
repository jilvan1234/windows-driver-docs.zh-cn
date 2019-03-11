---
title: Bug 检查 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
description: 指示一个驱动程序与任何尾随名称 IRP_MJ_CREATE 请求返回 STATUS_REPARSE DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN bug 检查。
ms.assetid: 60eeb24a-accf-4db8-ba5b-1738a9aa4b46
keywords:
- Bug 检查 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b229f28e86b65db5995d53b1253878bc9915fdb1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522406"
---
# <a name="bug-check-0xf9-driverreturnedstatusreparseforvolumeopen"></a>Bug 检查 0xF9:驱动程序\_退回\_状态\_重新分析\_有关\_卷\_打开


驱动程序\_退回\_状态\_重新分析\_有关\_卷\_打开 bug 检查的值为 0x000000F9。 这指示一个驱动程序返回状态\_重新分析到 IRP\_MJ\_没有尾随名称创建请求。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="driverreturnedstatusreparseforvolumeopen-parameters"></a>驱动程序\_退回\_状态\_重新分析\_有关\_卷\_打开参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>打开设备对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>向其颁发 IRP_MJ_CREATE 请求设备对象</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>包含新名称的文件 （若要重新分析） 与 Unicode 字符串的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>返回 IRP_MJ_CREATE 请求的驱动程序的信息</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

状态\_应仅为 IRP 返回重分析\_MJ\_创建请求，该值指示该驱动程序结尾的名称，一种支持命名空间。

 

 



