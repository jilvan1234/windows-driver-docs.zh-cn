---
title: SO_EXCLUSIVEADDRUSE
description: SO_EXCLUSIVEADDRUSE
ms.assetid: d281086f-4d8b-4e1e-b2bd-7b0a20338222
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_EXCLUSIVEADDRUSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cf54ae5ff50218e6809e6d20b79275423c63639c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841887"
---
# <a name="so_exclusiveaddruse"></a>\_EXCLUSIVEADDRUSE


SO\_EXCLUSIVEADDRUSE 套接字选项的状态确定是否将套接字绑定到的本地传输地址专门保留以供该套接字使用。 此套接字选项仅适用于侦听套接字、数据报套接字和面向连接的套接字。

如果 WSK 应用程序设置此套接字选项，则必须在将套接字绑定到本地传输地址之前执行此操作。

若要设置此套接字选项的状态，WSK 应用程序需要使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof （ULONG）</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量包含套接字选项的新状态值：</p>
<p>0：禁用本地传输地址的独占使用</p>
<p>1：启用本地传输地址的独占使用</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


若要检索此 socket 选项的状态，WSK 应用程序需要使用以下参数调用**WskControlSocket**函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_EXCLUSIVEADDRUSE</p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof （ULONG）</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收 socket 选项的状态值：</p>
<p>0：已禁用本地传输地址的独占使用</p>
<p>1：已启用本地传输地址的独占使用</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>


WSK 应用程序必须在调用**WskControlSocket**函数时指定一个指向 IRP 的指针，以便设置或检索\_EXCLUSIVEADDRUSE 套接字选项的状态。

此套接字选项的默认状态是禁用本地传输地址的独占使用。

若要详细了解如何使用\_EXCLUSIVEADDRUSE 套接字选项及其对套接字间本地传输地址的影响，请参阅[共享传输地址](https://docs.microsoft.com/windows-hardware/drivers/network/sharing-transport-addresses)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ws2def （包括 Wsk）</td>
</tr>
</tbody>
</table>

 

 




