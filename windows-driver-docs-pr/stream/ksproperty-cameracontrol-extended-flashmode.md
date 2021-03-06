---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE
description: Flash 属性控件为相机的正常和序列照片模式设置 flash 模式操作。
ms.assetid: A190CB91-0AC4-4ECC-8C55-F0C48CF7B190
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 11dd98552f76e8e88d585cb8a7e536a0965ceea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843232"
---
# <a name="ksproperty_cameracontrol_extended_flashmode"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_FLASHMODE


Flash 属性控件为相机的正常和序列照片模式设置 flash 模式操作。

## <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_值）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含驱动程序支持的下列一种或多种闪存模式的按位 "或" 组合。

| 闪光模式                                           | 描述                                                                |
|------------------------------------------------------|----------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_闪存\_关闭                   | 闪光灯处于关闭状态。                                                              |
| KSCAMERA\_EXTENDEDPROP\_闪存\_                    | 闪光灯处于默认强度级别。                                |
| \_ADJUSTABLEPOWER 上的 KSCAMERA\_EXTENDEDPROP\_闪存\_   | 闪存在特定电源级别打开。                                     |
| KSCAMERA\_EXTENDEDPROP\_闪存\_自动                  | 闪存是根据照明条件自动进行的。                           |
| KSCAMERA\_EXTENDEDPROP\_闪存\_自动\_ADJUSTABLEPOWER | 闪存是根据特定电源级别的照明条件自动进行的。 |

 

除了 KSCAMERA\_EXTENDEDPROP\_闪存\_关闭之外，以下功能标志可与以前的闪存设置组合。

| 闪光功能 | 描述 |
|---|---|
| KSCAMERA\_EXTENDEDPROP\_闪存\_REDEYEREDUCTION | 启用防红眼功能。 此标志可以与其他任何设置结合。 |
| KSCAMERA\_EXTENDEDPROP\_闪存\_SINGLEFLASH | 仅将闪存设置为一个触发器。 当照相机未处于照片序列模式时，将忽略此功能。 |
| KSCAMERA\_EXTENDEDPROP\_闪存\_MULTIFLASHSUPPORTED | 将 flash 设置为每个序列帧上的触发器。 当照相机未处于照片序列模式时，将忽略此功能。 |

 

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的闪光模式。

照相机的默认闪光模式为 KSCAMERA\_EXTENDEDPROP\_FLASH\_关闭。 如果相机支持 flash、KSCAMERA\_EXTENDEDPROP\_FLASH\_OFF、KSCAMERA\_EXTENDEDPROP\_闪存\_，以及 KSCAMERA\_EXTENDEDPROP\_闪存\_"自动" 是必需的模式。 KSCAMERA\_EXTENDEDPROP\_闪存\_自动\_ADJUSTABLEPOWER 和 KSCAMERA\_EXTENDEDPROP\_闪存\_自动\_ADJUSTABLEPOWER 模式是可选的。

如果相机支持照片序列模式，则闪存控制属性是对 KSCAMERA\_EXTENDEDPROP\_FLASH\_SINGLEFLASH 的支持所必需的。

此属性控件是同步的，不可取消。

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求时，驱动程序会将[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的成员设置为以下项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>支持闪存模式值。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>（当前 flash 模式值设置） |（flash 功能标志）</td>
</tr>
</tbody>
</table>

 

当 torch 模式为 KSCAMERA\_EXTENDEDPROP\_闪存\_\_ADJUSTABLEPOWER 或 KSCAMERA\_EXTENDEDPROP\_闪存\_上\_ADJUSTABLEPOWER，U)**成员为** [**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)包含介于 0-100 之间的强度级别值。 强度值为0，表示最小级别为100，表示最大强度级别。 如果未设置可调整的电源标志，则将在**u)** 中返回标准化强度设置的值。

如果以前未设置任何 flash 模式，则会将**标志**设置为 KSCAMERA\_EXTENDEDPROP\_FLASH\_关闭（默认值）。

### <a name="setting-the-property"></a>设置属性

设置属性时，KSPROPERTY\_类型\_SET 请求， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的 torch 模式。 [**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)中的**u)** 成员将包含设置的强度级别，如果**标志**为 KSCAMERA\_EXTENDEDPROP\_FLASH\_在\_ADJUSTABLEPOWER 或 KSCAMERA 上\_EXTENDEDPROP\_FLASH\_自动\_ADJUSTABLEPOWER。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
