---
title: OID_GEN_RCV_NO_BUFFER
description: 为查询，OID_GEN_RCV_NO_BUFFER OID 指定接收缓冲区空间的 NIC 无法接收 NIC 所致的帧数。
ms.assetid: 0fcbc7cc-439b-450f-b256-3584b29909fb
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RCV_NO_BUFFER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c97d6ef76b43e91ae2e2f02974a8b56e15b28637
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376448"
---
# <a name="oidgenrcvnobuffer"></a>OID\_GEN\_RCV\_否\_缓冲区


为查询，OID\_GEN\_RCV\_否\_缓冲区 OID 指定接收缓冲区空间的 NIC 无法接收 NIC 所致的帧数。 某些 Nic 不提供丢失的帧; 的精确数目它们提供只错过了至少一个帧的时间量。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本的驱动程序  
未请求。 使用[OID\_代\_统计信息](oid-gen-statistics.md)相反。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a name="remarks"></a>备注
-------

有关 Oid 的统计信息的常规信息，请参阅[General Statistics](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-general-statistics-oids)。

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


[OID\_GEN\_STATISTICS](oid-gen-statistics.md)

 

 




