---
title: WDI_TLV_DOT11_RESET_PARAMETERS
description: WDI_TLV_DOT11_RESET_PARAMETERS 是包含参数的 OID_WDI_TASK_DOT11_RESET TLV。
ms.assetid: 14F3DECD-E875-44BB-969B-705B075E4636
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DOT11_RESET_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b4b318d8626a7e15672861f5a4009cb4496422ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358562"
---
# <a name="wditlvdot11resetparameters"></a>WDI\_TLV\_DOT11\_RESET\_PARAMETERS


WDI\_TLV\_DOT11\_重置\_参数是包含参数的 TLV [OID\_WDI\_任务\_DOT11\_重置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-dot11-reset).

## <a name="tlv-type"></a>TLV 类型


0xA2

## <a name="length"></a>长度


超出 UINT8 的大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入  | 描述                                                                                                     |
|-------|-----------------------------------------------------------------------------------------------------------------|
| UINT8 | 当 （且仅当） 此值设置为 1，端口正在重置所有 MIB 属性都设置为其默认值。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




