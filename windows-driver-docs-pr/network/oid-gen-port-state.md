---
title: OID_GEN_PORT_STATE
description: 为查询，基础驱动程序使用 OID_GEN_PORT_STATE OID 获取 NDIS_OID_REQUEST 结构的端口号成员中指定的端口的当前状态。
ms.assetid: e0705b2e-08ea-4ed4-a6df-4c33b934c3dd
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PORT_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6349425aff9bb0a08bd6b14f85076eda1c2a6d19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367585"
---
# <a name="oidgenportstate"></a>OID\_GEN\_端口\_状态


为查询，基础驱动程序使用 OID\_常规\_端口\_要获取在指定的端口的当前状态的状态 OID **PortNumber**隶属[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 返回 NDIS\_状态\_成功并返回中的端口状态信息[ **NDIS\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566800)结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566800)

 

 



