---
title: 输入装配器阶段
description: 输入装配器阶段
ms.assetid: 8db6a2ab-8354-4690-8141-2cdd91c77d5c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd733f6aa8806d218bfd5624548e9352ebd62c65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840366"
---
# <a name="input-assembler-stage"></a>输入装配器阶段


输入汇编（IA）通过将源几何数据拉出1D 缓冲区来向渲染管道引入三角形、线条或点。

顶点数据可以来自多个缓冲区，并且可以从每个缓冲区以结构数组的方式进行访问。 缓冲区每个都绑定到单个输入槽，并具有结构步幅。 所有缓冲区中的数据布局由输入声明指定，其中每个条目都定义一个*元素*。 元素包含输入槽、结构偏移量、数据类型和目标寄存器（对于管道中的第一个活动着色器）。

给定的顶点序列是从缓冲区中提取的数据构造而来的。 数据是在由固定函数状态和各种*绘图\** （） DDI 调用的组合定向的遍历中提取的。 可以使用各种基元拓扑（例如，点列表、行列表、三角列表和三角带）来使顶点数据的序列表示一系列基元。

可以通过以下两种方式之一来生成顶点数据。 生成顶点数据的第一种方法是*非索引*呈现，这是包含顶点数据的缓冲区的顺序遍历。 顶点数据产生于每个缓冲区绑定的起始偏移量处。 生成顶点数据的第二种方法是*索引*呈现，这是包含标量整数索引的单个缓冲区的顺序遍历。 索引源自缓冲区中的起始偏移量。 每个索引都指示从包含顶点数据的缓冲区中提取数据的位置。 索引值与它们引用的缓冲区的特征无关。 缓冲区按声明进行描述。 非索引和索引呈现，每个都以自己的方式生成要从中提取顶点数据的地址，然后将结果组合成顶点和基元。

通过允许在每个顶点缓冲区（非索引用例）或索引缓冲区（索引用例）内的范围内循环，可以实现的实例化几何呈现。 可以将缓冲区绑定标识为*实例数据*或*顶点数据*。 此标识指定如何在执行实例化呈现时使用绑定缓冲区。 由非索引或索引呈现生成的地址用于提取顶点数据，在运行时执行实例呈现时，还会将这些数据用于循环。 另一方面，实例数据总是从每个缓冲区的偏移量开始，其频率等于每个实例一个步骤（例如，遍历实例中的顶点数目后的一个步骤）。 还可以选择实例数据的阶数，使其成为实例频率（也就是说，每个实例、每个第三个实例，等等）的下一步。

IA 的另一种特殊情况是，它可以读取流输出阶段写入的缓冲区。 此类方案启用了一种新的绘图操作类型[**DrawAuto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_drawauto)。 *DrawAuto*允许在不占用 CPU 的情况下重用写入流输出缓冲区的动态输出量，以确定实际写入的数据量。

除了从缓冲区生成顶点数据外，IA 还可以自动生成三个标量计数器值： VertexID、PrimitiveID 和 InstanceID，以便在呈现管道中输入着色器阶段。

在条带拓扑的索引呈现（如三角形带）中，提供一种机制，用于通过单个 * 绘图\*<em>（）调用 * 来绘制多个带

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁 IA：

[**CalcPrivateElementLayoutSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateelementlayoutsize)

[**CreateElementLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createelementlayout)

[**DestroyElementLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyelementlayout)

[**IaSetIndexBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)

[**IaSetInputLayout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setinputlayout)

[**IaSetTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_settopology)

[**IaSetVertexBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setvertexbuffers)

 

 





