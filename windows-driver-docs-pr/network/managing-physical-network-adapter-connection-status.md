---
title: 管理物理网络适配器连接状态
description: 管理物理网络适配器连接状态
ms.assetid: B8C6EB48-59D7-469B-87C8-57E60CB5C5D2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fec7c4f864c80a14e2112907bb5b98dfb87f7fc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343523"
---
# <a name="managing-physical-network-adapter-connection-status"></a>管理物理网络适配器连接状态


HYPER-V 可扩展交换机体系结构支持与单个外部网络适配器连接到基础物理介质的访问。 外部网络适配器可以绑定到一个或多个基础各种配置中的物理网络适配器。 有关这些配置的详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

可扩展交换机接口通知的以下步骤通过每个物理网络适配器连接状态的扩展：

1.  可扩展交换机的协议边缘发出的一个对象标识符 (OID) 组请求[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)。 此 OID 请求通知基础有关网络连接到可扩展交换机外部网络适配器创建可扩展的交换机扩展。

    创建网络连接后，会分配 NDIS\_交换机\_NIC\_索引值。 此索引值标识的可扩展交换机端口上的适配器的网络连接。 与外部网络适配器的网络连接分配 NDIS\_交换机\_NIC\_索引值**NDIS\_开关\_默认\_NIC\_索引**。

2.  有关每个网络适配器绑定直接或间接到外部网络适配器，可扩展交换机的协议边缘问题的一个单独的 OID 集请求[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263). 此 OID 请求通知有关与基础的网络适配器的网络连接创建的扩展。

    每个绑定到外部网络适配器的物理或虚拟网络适配器被分配一个标识符，如下所示：

    -   如果一个物理适配器绑定到外部网络适配器，则会分配 NDIS\_交换机\_NIC\_之一的索引值。

    -   如果负载平衡故障转移 (LBFO) 团队的网络适配器绑定到外部网络适配器，则会分配 NDIS\_交换机\_NIC\_之一的索引值。

        **请注意**中 LBFO 团队配置仅支持 LBFO 团队的 LBFO 提供程序的虚拟微型端口边缘视为要绑定到外部网络适配器。




-   如果网络适配器的可扩展交换机团队绑定到外部网络适配器，团队中的每个物理网络适配器分配唯一的 NDIS\_切换\_NIC\_大于或等于 1 的索引值。

    **请注意**在可扩展交换机团队配置中，团队中的每个物理网络适配器被视为绑定到外部网络适配器。




3.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)外部网络适配器。

    **请注意**此时，与外部网络的连接不可操作，且不能用于数据包流量。



4.  有关每个绑定到外部网络适配器的网络适配器，可扩展交换机的协议边缘问题的一个单独的 OID 集请求[OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)。 OID 设置的请求后发出此 OID 请求[OID\_交换机\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598263)已成功完成。

    [OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262) OID 请求通知该扩展，可扩展交换机的网络连接现在是操作。 如果外部网络适配器绑定到 MUX 驱动程序的虚拟微型端口边缘，协议边缘会发出一个单独的 OID\_交换机\_NIC\_连接请求。

    **请注意**就立即[OID\_交换机\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)请求针对发出的物理网络适配器与的 NDIS\_交换机\_NIC\_索引值大于或等于一，与外部网络的连接是否可正常运行。 此时，还可以发送或接收通过外部网络数据包流量。



5.  如果外部网络连接被被撤销，可扩展交换机的协议边缘会首先发出一个单独的 OID 集请求的[OID\_切换\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)为每个网络绑定到外部网络适配器的适配器。 完成这些 OID 请求后，可扩展交换机的协议边缘然后发出单独的 OID 集请求的[OID\_切换\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598264)为每个物理网络适配器，绑定到外部网络适配器，

    一旦所有网络连接到基础物理已断开连接并删除，可扩展交换机问题的协议边缘适配器[OID\_切换\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)和[OID\_交换机\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598264)断开连接，然后删除外部网络适配器连接的请求。

有关详细信息 NDIS\_交换机\_NIC\_索引值，请参阅[网络适配器索引值](network-adapter-index-values.md)。








