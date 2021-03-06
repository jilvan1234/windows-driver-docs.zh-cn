---
title: NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG 以指示 TCP 中的更改时将卸载的硬件功能。
ms.assetid: 4E73F09A-965F-4F32-AFF7-FDF1E3B2853C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_TASK_OFFLOAD_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 271e8e4eee97df291dde3239b32823b4087cb0ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375198"
---
# <a name="ndisstatuswdiindicationtaskoffloadcurrentconfig"></a>NDIS\_状态\_WDI\_指示\_任务\_卸载\_当前\_配置


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_任务\_卸载\_当前\_配置，以指示 TCP 中的更改时卸载功能硬件。

| Object |
|--------|
| Port   |

 

当更改 TCP 卸载功能的硬件，LE 将此未经请求的指示发送到下，用户设备，与新的 TCP/LSO 校验和功能。 使用值**NDIS\_卸载\_设置\_OFF**并**NDIS\_卸载\_设置\_ON** 中的成员[**WDI\_TLV\_TCP\_卸载\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-offload-capabilities)用于指示在更改卸载功能。 当 UE 向下发送[OID\_WDI\_设置\_TCP\_卸载\_参数](oid-wdi-set-tcp-offload-parameters.md)，LE 应更新的卸载功能，然后将发送此指示，以便OS 更新的最新的卸载功能信息。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                              |
|---------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI\_TLV\_TCP\_卸载\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-offload-capabilities) |                                | X        | TCP/IP 校验和与大量发送卸载功能。 |

 

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WDI\_SET\_TCP\_OFFLOAD\_PARAMETERS](oid-wdi-set-tcp-offload-parameters.md)

 

 




