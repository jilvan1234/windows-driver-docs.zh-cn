---
title: Stream 指针计时器
description: Stream 指针计时器
ms.assetid: 98413fc6-2b62-4c52-9ac4-bd2a3a60db60
keywords:
- 流指针 WDK AVStream，计时器
- 计时器 WDK AVStream
- 超时 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 260dfebf9324a34365ba757d25daeb42d6f47b4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533682"
---
# <a name="stream-pointer-timers"></a>Stream 指针计时器





若要在流指针上设置一个计时器，调用[ **KsStreamPointerScheduleTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff567135)。 如果按时间未被删除了指定的流指针*间隔*过期，AVStream 调用供应商提供的计时器回调例程。 指定*间隔*以 100 毫微秒为单位。

若要取消超时，请调用[ **KsStreamPointerCancelTimeout**](https://msdn.microsoft.com/library/windows/hardware/ff567128)。

 

 



