---
title: WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS
description: WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS 是包含默认 TLV OID_WDI_SET_DEFAULT_KEY_ID 的数据包传输的端口上的密钥 ID。
ms.assetid: 24E7E758-FEED-4D2A-BAA8-6DBC08726FBA
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_DEFAULT_TX_KEY_ID_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bbb949a18f4a03c35d6fb7c77bc30e8bbdcd5773
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379377"
---
# <a name="wditlvdefaulttxkeyidparameters"></a>WDI\_TLV\_DEFAULT\_TX\_KEY\_ID\_PARAMETERS


WDI\_TLV\_默认\_TX\_密钥\_ID\_参数是包含默认 TLV 密钥 ID 的端口上的数据包传输[OID\_WDI\_设置\_默认\_密钥\_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-default-key-id)。

## <a name="tlv-type"></a>TLV 类型


0x54

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                     |
|--------|-----------------------------------------------------------------|
| UINT32 | 指定的默认端口上的数据包传输的密钥 ID。 |

 

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

 

 




