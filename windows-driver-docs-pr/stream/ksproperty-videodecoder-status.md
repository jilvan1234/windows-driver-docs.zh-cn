---
title: KSPROPERTY\_VIDEODECODER\_状态
description: KSPROPERTY\_VIDEDECODER\_STATUS 属性从视频解码器检索状态信息。 必须实现此属性。
ms.assetid: 1d8cb537-1d85-4536-bd75-33beea0f586d
keywords:
- KSPROPERTY_VIDEODECODER_STATUS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d1fc113b2585f461807f9dfd7eefb091f9e9c01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837866"
---
# <a name="ksproperty_videodecoder_status"></a>KSPROPERTY\_VIDEODECODER\_状态


KSPROPERTY\_VIDEDECODER\_STATUS 属性从视频解码器检索状态信息。 必须实现此属性。

## <span id="ddk_ksproperty_videodecoder_status_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_STATUS_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)"><strong>KSPROPERTY_VIDEODECODER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSPROPERTY\_VIDEODECODER\_状态\_S 结构，用于指定视频解码设备的当前状态，例如传入模拟信号中的行数，以及信号是否已锁定。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEODECODER\_状态\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_status_s)

 

 






