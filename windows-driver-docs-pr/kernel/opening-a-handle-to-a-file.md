---
title: 打开文件的句柄
description: 打开文件的句柄
ms.assetid: 9378282a-ee29-44b6-b206-602eee94ec3b
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- 对象 WDK 文件对象
- 文件处理 WDK 内核
- 文件 WDK 内核的句柄
- 正在打开文件的句柄
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b47def9148f071e3fcc59e01f5054b060b702eb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827737"
---
# <a name="opening-a-handle-to-a-file"></a>打开文件的句柄





若要打开文件的句柄，请执行以下步骤：

1.  创建一个[ **\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_object_attributes)结构的对象，并调用[**InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)宏来初始化该结构。 将文件的对象名称指定为**InitializeObjectAttributes**的*ObjectName*参数。

2.  通过将**对象\_特性**结构传递到[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)、 [**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)或[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)，打开文件的句柄。

    如果该文件不存在，则**IoCreateFile**和**ZwCreateFile**将创建该文件，而**ZWOPENFILE**将返回状态\_对象\_名称\_找不到\_。

请注意，驱动程序几乎始终使用**ZwCreateFile**或**ZwOpenFile** ，而不是**IoCreateFile**。

调用**IoCreateFile**、 **ZwCreateFile**或**ZwOpenFile**时，Windows executive 会创建一个新的文件对象来表示文件，并为对象提供一个打开的句柄。 此文件对象会一直保留，直到关闭所有打开的句柄。

无论你调用哪个例程，你都必须将所需的访问权限作为*DesiredAccess*参数进行传递。 这些权限必须涵盖驱动程序将执行的所有操作。 下表列出了这些操作以及要请求的相应访问权限。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>必需的访问权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>从文件中读取。</p></td>
<td><p>FILE_READ_DATA 或 GENERIC_READ</p></td>
</tr>
<tr class="even">
<td><p>写入文件。</p></td>
<td><p>FILE_WRITE_DATA 或 GENERIC_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>仅写入文件结尾。</p></td>
<td><p>FILE_APPEND_DATA</p></td>
</tr>
<tr class="even">
<td><p>读取文件的元数据，如文件的创建时间。</p></td>
<td><p>FILE_READ_ATTRIBUTES 或 GENERIC_READ</p></td>
</tr>
<tr class="odd">
<td><p>写入文件的元数据，如文件的创建时间。</p></td>
<td><p>FILE_WRITE_ATTRIBUTES 或 GENERIC_WRITE</p></td>
</tr>
</tbody>
</table>

 

有关*DesiredAccess*的可用值的详细信息，请参阅[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)。

 

 




