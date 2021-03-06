---
title: C28175
description: 警告 C28175 不应由驱动程序访问结构的成员。
ms.assetid: 259a90d7-29ef-4a27-a921-8fff93b325bd
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28175
ms.openlocfilehash: ad7e951940569535e83044217f9968385f12868a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840312"
---
# <a name="c28175"></a>C28175


警告 C28175：结构的成员不应由驱动程序访问

此警告表明驱动程序访问了驱动程序绝不应访问的未记录的结构成员。

驱动程序不应访问指定的未记录的结构成员。 对于不透明或部分不透明结构的大多数未记录的成员，此禁止是绝对的。 但是，驱动程序可能从特定例程访问某些未记录的结构成员。 例如，驱动程序可能只在驱动程序\_INITIALIZE 或驱动程序\_卸载例程内访问部分不透明的[**驱动程序\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)结构的未记录成员。

有时，此规则应用于特定成员的原因并不明显。 例如，出现这种情况的一个实例是 **\_设备\_对象**的**NextDevice**成员。 在这种情况下，应使用锁来安全地访问此链接列表，但该锁对驱动程序不可用。 在这种情况下，违反此规则会导致不常发生但难以诊断的故障。 访问相关设备的正确方法是使用[**IoEnumerateDeviceObjectList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioenumeratedeviceobjectlist)函数。

 

 





