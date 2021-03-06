---
title: 有关变形的注意事项
description: 本主题讨论双用型计时和性能的注意事项。
ms.assetid: 2353023A-989A-4836-A39C-0B5F749E7FF2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c5eedb732e502156623dce31328a5c6cc233e05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326110"
---
# <a name="considerations-for-convertibles"></a>有关变形的注意事项


本主题讨论双用型计时和性能的注意事项。

可转换系统为用户提供一个系统中有一台平板电脑和便携式计算机的选项。 本部分提供有关如何创建便携式计算机模式和盖板模式之间的转换的示例。

键盘存在取决于为便携式计算机和平板电脑模式之间的区别主要的准则。 应遵循的一般规则是，可转换便携式计算机键盘将成为完全可供用户和用户可以轻松键入自然位置时。

需要时触发一个模式或停靠更改是为了确保模式或停靠更改发生时发送任何不需要的状态更改，请考虑一个重要方面。 从这个角度看，一种方法是在系统已达到新的稳定状态，但不是更快地立即触发指示器更改。

一般规则是触发指示器模式更改后在用户完成其操作和系统完全转换到新的模式。

模式指示器示例如下所示：

-   附加或分离键盘
-   翻转屏幕
-   可在屏幕旋转
-   若要覆盖或发现键盘将屏幕滑动

停靠指示器示例如下所示：

-   将附加到经典停靠系统
-   将附加到端口复制器

若要提供最佳用户体验，状态指示器更改应快速用户体验。 应不高于 200 毫秒后系统达到新的状态发送状态更改通知。

以下两个示例使用便携式计算机模式下启动，并说明最佳计时时应切换指示器状态：

![键盘附加和分离的转换](images/keyboardattachdetachconvertible.jpg)

**图 1 键盘附加和分离的转换**

![屏幕旋转转换](images/screenswivelconvertible.jpg)

**图 2 屏幕旋转转换**

 

 




