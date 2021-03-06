---
title: DEVPROP_TYPE_UINT64
description: 在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_INT64 标识符表示基本数据类型标识符，该值指示数据类型为 ULONG64 类型无符号的整数。
ms.assetid: a6dfb90d-0cae-4b63-bc27-57d7b0f6b897
keywords:
- DEVPROP_TYPE_UINT64 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_UINT64
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3326d7a926b6598dfb70c1e681194cafe9320eed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331274"
---
# <a name="devproptypeuint64"></a>DEVPROP_TYPE_UINT64


在 Windows Vista 和更高版本的 Windows，DEVPROP_TYPE_INT64 标识符表示基本数据类型标识符，该值指示数据类型为 ULONG64 类型无符号的整数。

<a name="remarks"></a>备注
-------

可以仅与组合 DEVPROP_TYPE_UINT64 [ **DEVPROP_TYPEMOD_ARRAY** ](devprop-typemod-array.md)属性数据类型修饰符。

**设置此属性类型**

若要设置其基本数据类型为 DEVPROP_TYPE_UINT64 的属性，调用对应**SetupDiSet * Xxx*** 属性函数和集函数的输入参数，如下所示：

- 设置*PropertyType* DEVPROP_TYPE_UINT64，参数设置*PropertyBuffer*参数指向的缓冲区可包含至少一个 ULONG64 值，并设置*PropertyBufferSize*参数<strong>sizeof (</strong>ULONG64<strong>)</strong>。

- 根据需要设置其他函数输入的参数设置的属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

 

 





