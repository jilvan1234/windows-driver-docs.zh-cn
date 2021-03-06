---
title: KSPROPERTY\_插孔\_CONTAINERID
description: KSPROPERTY\_插座\_CONTAINERID 属性实现为使用筛选器句柄访问的按位数属性。
ms.assetid: 01A157B0-41EE-4713-B5D3-B9BF9C2B80CE
keywords:
- KSPROPERTY_JACK_CONTAINERID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK_CONTAINERID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74037d3400203ef5e32178311a15fd33efdba61e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832748"
---
# <a name="ksproperty_jack_containerid"></a>KSPROPERTY\_插孔\_CONTAINERID


KSPROPERTY\_插座\_CONTAINERID 属性实现为使用筛选器句柄访问的按位数属性。

与一个或多个物理插孔或其他有线或无线连接关联的任何桥接 pin 都可以支持此属性。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>固定工厂（通过筛选器句柄）</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td align="left"><p><strong>GUID</strong></p></td>
</tr>
</tbody>
</table>

 

属性值（实例数据）是一个 GUID。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_插孔\_CONTAINERID 属性请求返回 GUID，该 GUID 具有与物理插孔关联的设备的容器 ID，或其他有线或无线连接。

<a name="remarks"></a>备注
-------

当且仅当满足以下条件时，音频驱动程序才支持此属性：

-   关联音频设备的容器 ID 不同于要为其加载音频驱动程序的设备节点的容器 ID。

-   驱动程序可以通过其他方式获得正确的容器 ID。

如果音频终结点位于音频适配器的不同塑料片上，则只需填充 KSPROPERTY\_插孔\_CONTAINERID 属性。 默认情况下，音频端点将继承其父端点的容器 ID。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**BTHHFP\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ns-bthhfpddi-_bthhfp_descriptor)

[**IOCTL\_BTHHFP\_设备\_获取\_CONTAINERID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_containerid)

 

 






