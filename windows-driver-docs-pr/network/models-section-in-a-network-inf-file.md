---
title: 网络 INF 文件中的 Models 节
description: 网络 INF 文件中的 Models 节
ms.assetid: 0340a875-ae5a-49c8-9498-1f8aba97e029
keywords:
- INF 文件 WDK 网络，模型部分
- 可使用网络 INF 文件 WDK，模型部分
- 模型部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca1450d79b01141757a3af63c0e7bed1d8b32418
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382209"
---
# <a name="models-section-in-a-network-inf-file"></a>网络 INF 文件中的 Models 节





**模型**网络 INF 文件中的部分基于泛型[ **INF 模型部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)。

**模型**INF 文件中的部分包含下列格式为每种类型的情况下的 INF 文件安装的组件的一项：

\[*device-description*= *install-section.name*, *hw-id*\[, *compatible-id*...\]

此项的详细说明，请参阅[创建一个 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)。

*Hw id* （也称为设备、 硬件或组件 ID） 的网络适配器必须与匹配的 PnP 管理器为适配器提供的硬件 ID。

*Hw id*网络软件组件应包含的提供程序名称后, 跟下划线和制造商名称或产品名称，例如：

-   MS\_DLC

-   MS\_IBMDLC

一个*提供程序名称*标识提供程序的 INF 文件。 一个*制造商名称*标识软件组件的制造商。 *产品名称*标识软件组件。

 

 





