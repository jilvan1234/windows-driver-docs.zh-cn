---
title: 文件系统对象的创建和删除
description: 文件系统对象的创建和删除
ms.assetid: 71e342cf-455f-4b01-af55-12568bf06728
keywords:
- 小型重定向程序 WDK，对象创建
- 小型重定向程序 WDK，对象删除
- 文件对象 WDK 微型重定向程序
- 对象 WDK 微型重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcc313d55a7ca43bf52697599455ea37c78d7199
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841421"
---
# <a name="file-system-object-creation-and-deletion"></a>文件系统对象的创建和删除


许多由网络小型重定向程序实现的例程用于创建和删除文件。 RDBSS 通过创建多个结构来抽象此过程，其中包括引用计数的 SRV\_OPEN、FCB 和 FOBX 结构。 通常，创建或打开文件系统对象需要创建 SRV\_OPEN、FCB 和 FOBX 结构。 正常过程是 RDBSS 调用由网络小型重定向程序实现的[**MRxCreate**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)例程，以将信息填充到这些结构中。 还可以使用[**MRxShouldTryToCollapseThisOpen**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen)和[**MRxCollapseOpen**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen)例程来展开现有 SRV\_open 结构上的打开/创建文件请求。

在网络重定向程序的上下文中，文件对象指的是文件控制块（FCB）结构和文件对象扩展（FOBX）结构。 文件对象与 FOBXs 之间存在一对一的对应关系。 许多文件对象将引用相同的 FCB 结构，该结构表示远程服务器上某个位置的单个文件。 客户端可以在同一 FCB 上具有多个不同的打开请求（NtCreateFile 请求），其中每个请求都将创建一个新的文件对象。 RDBSS 和网络微型重定向程序可以选择发送比收到的 NtCreateFile 请求更少的[**MRxCreate**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)请求，这会在多个 FOBXs 之间有效共享服务器打开请求（SRV\_打开）。

RDBSS 和网络小型重定向程序不必在用户关闭文件时关闭 SRV\_打开的结构。 RDBSS 可以尝试重复使用 SRV\_开放结构和数据，无需与服务器联系。 某些 Windows 应用程序可以打开、读取和关闭文件，然后快速重新打开同一文件。 在这些情况下，重用 SRV\_开放结构可以提高性能。

有几个例程用于关闭并完成这些数据结构，并释放不再需要的任何内存或其他资源。 这些例程包括[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))、 [**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)、 [**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)、 [**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)和[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)。

下表列出了可由网络小型重定向程序为文件系统对象创建和删除操作实现的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown" data-raw-source="[&lt;strong&gt;MRxAreFilesAliased&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)"><strong>MRxAreFilesAliased</strong></a></td>
<td align="left"><p>如果两个 FCB 对象表示同一个文件，RDBSS 将调用此例程来查询网络微型重定向程序。 当处理两个看起来相同但名称不同的文件（例如，MS-DOS 短名称和长名称）时，RDBSS 将调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85)" data-raw-source="[&lt;strong&gt;MRxCleanupFobx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))"><strong>MRxCleanupFobx</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序关闭文件系统对象扩展。 RDBSS 发出此调用以响应在文件对象上接收 IRP_MJ_CLEANUP。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown" data-raw-source="[&lt;strong&gt;MRxCloseSrvOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)"><strong>MRxCloseSrvOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向器关闭 SRV_OPEN 对象。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen" data-raw-source="[&lt;strong&gt;MRxCollapseOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcollapseopen)"><strong>MRxCollapseOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序将打开的文件系统请求折叠到现有的 SRV_OPEN。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate" data-raw-source="[&lt;strong&gt;MRxCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxcreate)"><strong>MRxCreate</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序创建文件系统对象。 此调用由 RDBSS 发出，以响应接收 IRP_MJ_CREATE。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb" data-raw-source="[&lt;strong&gt;MRxDeallocateForFcb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)"><strong>MRxDeallocateForFcb</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序释放 FCB。 此调用用于响应关闭文件系统对象的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx" data-raw-source="[&lt;strong&gt;MRxDeallocateForFobx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)"><strong>MRxDeallocateForFobx</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序释放 FOBX。 此调用用于响应关闭文件系统对象的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown" data-raw-source="[&lt;strong&gt;MRxExtendForCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)"><strong>MRxExtendForCache</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序在缓存管理器缓存文件时扩展文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache" data-raw-source="[&lt;strong&gt;MRxExtendForNonCache&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxextendfornoncache)"><strong>MRxExtendForNonCache</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序在缓存管理器未缓存文件时扩展文件。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush" data-raw-source="[&lt;strong&gt;MRxFlush&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxflush)"><strong>MRxFlush</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序刷新文件系统对象。 RDBSS 发出此调用以响应接收 IRP_MJ_FLUSH_BUFFERS。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown" data-raw-source="[&lt;strong&gt;MRxForceClosed&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)"><strong>MRxForceClosed</strong></a></td>
<td align="left"><p>RDBSS 调用此例程来请求网络小型重定向程序强制关闭。 当 SRV_OPEN 的条件不良好或 SRV_OPEN 标记为已关闭时，将调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable" data-raw-source="[&lt;strong&gt;MRxIsLockRealizable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)"><strong>MRxIsLockRealizable</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器指示此 NET_ROOT 是否支持字节范围锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen" data-raw-source="[&lt;strong&gt;MRxShouldTryToCollapseThisOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxshouldtrytocollapsethisopen)"><strong>MRxShouldTryToCollapseThisOpen</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络小型重定向程序指示 RDBSS 是否应尝试并将打开的请求折叠到现有的文件系统对象。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate" data-raw-source="[&lt;strong&gt;MRxTruncate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxtruncate)"><strong>MRxTruncate</strong></a></td>
<td align="left"><p>RDBSS 调用此例程，请求网络最小化重定向器截断文件系统对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend" data-raw-source="[&lt;strong&gt;MRxZeroExtend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxzeroextend)"><strong>MRxZeroExtend</strong></a></td>
<td align="left"><p>如果文件大小大于 FCB 的有效数据长度，RDBSS 将调用此例程来请求网络最小化重定向程序扩展文件系统对象（清除时使用零）来填充文件。</p></td>
</tr>
</tbody>
</table>

 

 

 




