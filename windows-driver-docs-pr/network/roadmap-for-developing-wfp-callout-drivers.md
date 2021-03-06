---
title: WFP 标注驱动程序开发路线图
description: WFP 标注驱动程序开发路线图
ms.assetid: 98c857d9-e4a6-4a7f-8427-642763864f3e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8a32ae092cee3034371070c5f0b91d719689d72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842008"
---
# <a name="roadmap-for-developing-wfp-callout-drivers"></a>WFP 标注驱动程序开发路线图


若要创建 Windows 筛选平台（WFP）标注驱动程序，请执行以下步骤：

-   步骤1：了解 WFP 体系结构。

    有关 WFP 的信息，请参阅[Windows 筛选平台](https://docs.microsoft.com/windows/desktop/FWP/windows-filtering-platform-start-page)。 你可能会发现，你可以开发 WFP 用户模式应用程序，并避免写入 WFP 标注驱动程序。

-   步骤2：了解 Windows 体系结构和驱动程序。

    您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅[所有驱动程序开发人员的概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)。

-   步骤3：确定适用于 WFP 标注驱动程序的 Windows 驱动程序模型。

    可以使用 Windows 驱动模型（WDM）或内核模式驱动程序框架（KMDF）编写 WFP 标注驱动程序。 有关如何选择驱动程序模型的详细信息，请参阅[选择驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)。 有关 WDM 的详细信息，请参阅[Windows 驱动程序简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-windows-drivers)和[编写 WDM 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-wdm-drivers)。 有关 KMDF 的详细信息，请参阅[WDF 驱动程序开发指南](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)。

-   步骤4：确定其他 Windows 驱动程序设计决策。

    有关如何进行其他 Windows 设计决策的信息，请参阅[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)、 [64 位驱动程序的编程问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)以及[创建国际 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

-   步骤5：了解 Windows 驱动程序的生成、测试和调试过程和工具。

    构建驱动程序不同于构建用户模式应用程序。 有关 Windows 驱动程序生成、调试和测试过程、驱动程序签名和[Windows 硬件认证工具包（HCK）](https://go.microsoft.com/fwlink/p/?LinkId=733613)测试的信息，请参阅[生成、调试和测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 有关生成、测试、验证和调试工具的信息，请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)。

-   步骤6：查看 GitHub 上[windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[windows 筛选平台（WFP）驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=618680)。

-   步骤7：作出有关 WFP 标注驱动程序的设计决策。

    有关如何设计 WFP 标注驱动程序的信息，请参阅[标注驱动程序编程注意事项](callout-driver-programming-considerations.md)。

-   步骤8：开发、构建、测试和调试 WFP 标注驱动程序。

    有关 WFP 标注驱动程序的详细信息，请参阅[标注驱动程序操作](callout-driver-operations.md)和[标注驱动程序安装](callout-driver-installation.md)。 有关特定于 WFP 的函数、结构、枚举或常量的信息，请参阅[Windows 筛选平台标注驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。 有关迭代生成、测试和调试的信息，请参阅[生成、调试和测试过程的概述](https://docs.microsoft.com/windows-hardware/drivers)。 此过程有助于确保构建一个可正常工作的驱动程序。

-   步骤9：创建用于 WFP 标注驱动程序的驱动程序包。

    有关详细信息，请参阅[提供驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)和[标注驱动程序安装](callout-driver-installation.md)。

-   步骤10：签署和分发 WFP 标注驱动程序。

    最后一步是对驱动程序进行签名（可选）和分发。 如果你的驱动程序满足为[Windows 硬件认证包（HCK）](https://go.microsoft.com/fwlink/p/?LinkId=733613)定义的质量标准，你可以通过 Microsoft Windows 更新计划分发它。 有关如何分发驱动程序的详细信息，请参阅[分发驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。

 

 





