---
title: Bug 检查 0x169 CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
description: CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP bug 检查具有 0x00000169 值。 这表示群集共享卷管理器要求创建一个新的卷设备对象，并且卷仍未送达的时间。
keywords:
- Bug 检查 0x169 CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
- CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
ms.date: 01/03/2019
topic_type:
- apiref
api_name:
- CLUSTER_CSV_VOLUME_ARRIVAL_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b764f08edc97637767c3480c76247d06be68440a
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743496"
---
# <a name="bug-check-0x169-clustercsvvolumearrivallivedump"></a>Bug 检查 0x169:群集\_CSV\_卷\_到达\_LIVEDUMP

群集\_CSV\_卷\_到达\_LIVEDUMP bug 检查的值为 0x00000169。 这表示群集共享卷管理器要求创建一个新的卷设备对象，并且卷仍未送达的时间。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="clustercsvvolumearrivallivedump-parameters"></a>群集\_CSV\_卷\_到达\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 群集服务 PID。 |
|2| 保留。|
|3| 保留。|
|4| 保留。|


## <a name="cause"></a>原因
-----

群集共享卷管理器要求创建一个新的卷设备对象，并及时到达不到卷。

系统生成的转储实时的分析的延迟。

（此代码可以永远不会用于实际的执行错误检查。）

## <a name="resolution"></a>分辨率
----------
 

## <a name="see-also"></a>请参阅
----------

[故障排除挂起使用实时转储 （博客）](https://blogs.msdn.microsoft.com/clustering/2016/03/02/troubleshooting-hangs-using-live-dump/)

[Bug 检查代码参考](bug-check-code-reference2.md)



