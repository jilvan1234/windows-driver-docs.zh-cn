---
title: KSPROPERTY\_ONESHOT\_断开连接
description: KSPROPERTY\_ONESHOT\_断开连接属性用于提示音频驱动程序以断开与蓝牙音频设备的连接。
ms.assetid: B79B3B1E-A34A-4FF9-852A-938C0D5202E9
keywords:
- KSPROPERTY_ONESHOT_DISCONNECT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ONESHOT_DISCONNECT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98361d8e8fbc5ad4261f6a598344756ccc9df1d1
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391668"
---
# <a name="kspropertyoneshotdisconnect"></a>KSPROPERTY\_ONESHOT\_断开连接


**KSPROPERTY\_ONESHOT\_断开连接**属性用于提示音频驱动程序以断开与蓝牙音频设备的连接。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>NULL</p></td>
</tr>
</tbody>
</table>

 

没有属性值请求而发送的此属性。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

**KSPROPERTY\_ONESHOT\_断开连接**属性将返回状态\_成功请求是否成功。

&gt; \[!请注意\]&gt;成功的请求表示该驱动程序尝试以断开与蓝牙音频设备，但并不一定意味着的尝试已成功。

 

<a name="remarks"></a>备注
-------

您可以实现[ **KSPROPERTY\_JACK\_说明**](ksproperty-jack-description.md)固定在中，您的驱动程序的属性。 此实现允许你检查连接状态的终结点进行后**KSPROPERTY\_ONESHOT\_断开连接**属性请求。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSPROPERTY\_JACK\_说明**](ksproperty-jack-description.md)

 

 






