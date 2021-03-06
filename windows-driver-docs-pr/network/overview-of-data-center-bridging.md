---
title: 数据中心桥接概述
description: 数据中心桥接概述
ms.assetid: FEB3FDBB-8A3C-4907-A6D0-CB5E94BCFEFF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b5b7d6562551d0b4f3267d57a60f2a4aacfb4ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843748"
---
# <a name="overview-of-data-center-bridging"></a>数据中心桥接概述


IEEE 802.1 数据中心桥接（DCB）是一系列标准，它为局域网（LAN）和存储区域网络（SAN）技术定义了一个统一的802.3 以太网媒体接口或*构造*。 DCB 扩展了当前802.1 桥接规范，以支持在数据中心内的相同网络结构上共存基于 LAN 和基于 SAN 的应用程序。 DCB 还通过定义阻止数据包丢失的链接级别策略，来支持通过以太网（FCoE）和 iSCSI 的技术（如光纤通道。

DCB 包括以下802.1 草案标准，这些标准指定了网络设备在统一数据中心结构中的交互方式：

<a href="" id="priority-based-flow-control--pfc-"></a>基于优先级的流控制（PFC）  
PFC 是在 IEEE 802.1 Q b b 草案标准中指定的。 此标准是 DCB 界面框架的一部分。

PFC 支持可靠地传递数据，因为拥塞会显著减少数据包丢失。 这允许丢失敏感的协议（如 FCoE）与相同统一构造上的传统不区分的协议共存。

PFC 指定直接连接的对等方之间的链接级流控制机制。 PFC 类似于 IEEE 802.3 暂停帧，而是对单个 802.1 p 优先级别进行操作。 这允许接收方在任何优先级别暂停发送器。

有关 PFC 的详细信息，请参阅[基于优先级的流控制（PFC）](priority-based-flow-control--pfc.md)。

<a href="" id="enhanced-transmission-selection--ets-"></a>增强的传输选择（ETS）  
ETS 是在 IEEE 802.1 Qaz 草案标准中指定的传输选择算法（TSA）。 此标准是 DCB 界面框架的一部分。

ETS 在分配给不同 IEEE 802.1 p 优先级级别的流量类之间分配带宽。 每个流量类在 directlyconnected 对等方之间的数据链路上分配了可用带宽的百分比。 如果流量类不使用其分配的带宽，ETS 允许其他流量类使用流量类未使用的可用带宽。

有关 ETS 的详细信息，请参阅[增强的传输选择（ETS）算法](enhanced-transmission-selection--ets--algorithm.md)。

<a href="" id="data-center-bridging-exchange--dcbx--protocol"></a>数据中心桥接 Exchange （DCBX）协议  
还在 IEEE 802.1 Qaz 草案标准中指定了数据中心桥接 Exchange （DCBX）协议。 DCBX 允许在两个 directlyconnected 对等方之间交换 DCB 配置参数。 这允许这些对等方调整和调整服务质量（QoS）参数，以优化通过连接的数据传输。

DCBX 还用于检测网络适配器（*本地对等*）与远程对等节点之间的冲突的 QoS 参数设置。 根据本地和远程 QoS 参数设置，微型端口驱动程序可以解决冲突，并派生一组操作 QoS 参数。 网络适配器使用这些操作参数将数据包的优先级传输到远程对等方。 有关驱动程序如何解析其操作 NDIS QoS 参数设置的详细信息，请参阅[解决操作 Ndis qos](resolving-operational-ndis-qos-parameters.md)参数。

DCBX 包含 DCB 类型-值（TLV）设置，这些设置通过链路层发现协议（LLDP）数据包传输。 在 IEEE 802.1 AB-2005 标准中指定 LLDP。

**请注意**  DCBX 指定本地对等方在任何给定时间都只维护一个远程对等方的配置参数。 因此，网络适配器只维护一组本地、远程和操作 NDIS QoS 参数。

 

每个 ETS 流量类和 PFC 配置设置都与一个 IEEE 802.1 p 优先级关联。 优先级别指定为数据包的 802.1 Q 标记内的3位值。 对于 NDIS 数据包，802.1 p 优先级由[**NDIS\_NET\_缓冲器\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)的**UserPriority**成员指定，\_8021Q\_INFO 结构与数据包的[**网络关联\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

有关优先级别的详细信息，请参阅[IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

 

 





