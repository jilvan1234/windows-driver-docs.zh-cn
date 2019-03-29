---
title: CompleteRequestStatusCheck 规则 (wdm)
description: CompleteRequestStatusCheck 规则验证在 IRP 的 I/O 状态值匹配较低的驱动程序返回的状态值。
ms.assetid: 3B61137E-1D10-443B-A653-B32D638B17DB
ms.date: 05/21/2018
keywords:
- CompleteRequestStatusCheck 规则 (wdm)
topic_type:
- apiref
api_name:
- CompleteRequestStatusCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 669cf9c721cef0c8ff84d830d71e786c73e6af08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565227"
---
# <a name="completerequeststatuscheck-rule-wdm"></a>CompleteRequestStatusCheck 规则 (wdm)


**CompleteRequestStatusCheck**规则验证是否在 IRP 的 I/O 状态值匹配较低的驱动程序返回的状态值。

如果 IRP 状态是状态，驱动程序的调度例程不应完成 IRP\_PENDING。

驱动程序的调度例程不应完成状态 IRP\_如果较低的驱动程序失败 IRP 的成功。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>CompleteRequestStatusCheck</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)
 [ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)
[**IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350) 
 [**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 




