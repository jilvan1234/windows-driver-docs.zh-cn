---
title: OID_WDI_SET_REMOVE_WOL_PATTERN
description: OID_WDI_SET_REMOVE_WOL_PATTERN 从固件中删除 LAN 唤醒 (WOL) 模式。
ms.assetid: 9fb03747-b585-4c73-b004-1bdc2a995e9d
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_REMOVE_WOL_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 865c4fc0d84655e12705463559bb06a68107b80d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533117"
---
# <a name="oidwdisetremovewolpattern"></a>OID\_WDI\_SET\_REMOVE\_WOL\_PATTERN


OID\_WDI\_设置\_删除\_WOL\_模式从固件中删除对 LAN 唤醒 (WOL) 模式。

| 范围 | 设置与任务序列化 | 正常执行时间 （秒） |
|-------|--------------------------|---------------------------------|
| 端口  | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


| TLV                                                                                        | 允许多个 TLV 实例 | 可选 | 描述     |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------|
| [**WDI\_TLV\_WAKE\_PACKET\_PATTERN\_REMOVE**](https://msdn.microsoft.com/library/windows/hardware/dn898186) |                                |          | WOL 模式 id。 |

 

## <a name="set-property-results"></a>设置属性结果


任何其他参数。 标头中的数据就足够了。
要求
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
<td><p>标头</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WDI\_SET\_ADD\_WOL\_PATTERN](oid-wdi-set-add-wol-pattern.md)

 

 



