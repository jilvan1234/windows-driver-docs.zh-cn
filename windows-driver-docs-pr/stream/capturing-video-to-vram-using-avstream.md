---
title: 使用 AVStream 将视频捕获到 VRAM
description: 使用 AVStream 将视频捕获到 VRAM
ms.assetid: c4ca4a67-83cb-4a89-bc84-e06b1dc67b66
keywords:
- AVStream WDK，vram 能够捕获
- Vram 能够捕获 WDK AVStream
- 捕获到 vram 能够 WDK AVStream 视频
- 视频捕获到 vram 能够 WDK AVStream
- 到 vram 能够 WDK AVStream 音频捕获
- 数据捕获到 vram 能够 WDK AVStream
- 显示微型驱动程序 WDK vram 能够捕获
- 微型驱动程序 WDK vram 能够捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e33a58ce1de5794913affa95b9e2396dff608f5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386658"
---
# <a name="capturing-video-to-vram-using-avstream"></a>使用 AVStream 将视频捕获到 VRAM


从 Windows Vista 开始，视频和音频图形适配器的 vram 能够直接向可以捕获 AVStream 驱动程序。 AVStream 驱动程序在 Windows Vista 之前已存在的必须首先将数据置于 vram 能够、 将其传输到系统内存，然后最后再到 vram 能够显示。

新的 vram 能够捕获支持利用 GPU 计划和所提供的 vram 能够虚拟化的[Windows Vista 显示器驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)。

若要捕获到 vram 能够，设备必须包括捕获并显示相同的视频卡上的功能。

以下部分介绍如何将 vram 能够捕获支持添加到新的或现有驱动程序：

[在 AVStream 中捕获的 vram 能够概述](overview-of-vram-capture-in-avstream.md)

[Vram 能够捕获属性](vram-capture-properties.md)

[捕获到 vram 能够未压缩的数据](capturing-uncompressed-data-to-vram.md)

[将 vram 能够捕获支持添加到现有 AVStream 驱动程序](adding-vram-capture-support-to-existing-avstream-drivers.md)

您可以找到示例代码显示中的 vram 能够捕获[AVStream 模拟硬件示例驱动程序 (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083)。

 

 




