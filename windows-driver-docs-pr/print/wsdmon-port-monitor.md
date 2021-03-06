---
title: WSDMON 端口监视器
description: WSDMON 端口监视器
ms.assetid: fd6b0136-ca6e-4882-b6b9-be868f0dfc18
keywords:
- 打印监视器 WDK WSDMON
- WSDMON 端口监视器 WDK
- 端口监视器 WDK 打印 WSDMON
- 对于设备 WDK WIA，端口监视器的 web 服务
- WSD 法规遵从性 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af40e6f9317e808f6bcc85dcc7aee74c5f3379f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356970"
---
# <a name="wsdmon-port-monitor"></a>WSDMON 端口监视器


WSDMON 端口监视器是支持打印到符合的网络打印机的打印机端口监视器[Web Services for Devices (WSD) 技术](https://docs.microsoft.com/windows-hardware/drivers/print/web-services-for-devices-print-service-schema)。 WSDMON 端口监视器侦听的 WSD 事件，并相应地更新打印机状态。 此端口监视器是 Windows Vista 的新增功能。

WSDMON 端口监视器可以：

-   发现网络打印机并安装它们。

-   将作业发送到 WSD 打印机。

-   监视状态和配置的 WSD 打印机，并相应地更新打印机对象状态。

-   对于受支持的响应双向 (bidi) 查询[bidi 架构](bidirectional-communication-schema.md)。

-   监视 bidi 架构值发生更改并发送通知

WSDMON 的同类的方式类似于 TCP/IP 端口监视器 ([TCPMON](tcpmon-xcv-interface.md))。 WSDMON 中不支持以下 TCPMON 命令：

AddPort

DeletePort

MonitorUI

WSDMON 支持以下 Xcv 命令：

[CleanupPort](cleanupport.md)

[DeviceID](deviceid2.md)

[PnPXID](pnpxid.md)

[ResetCommunication](resetcommunication.md)

[ServiceID](serviceid.md)

有关适用于设备的 Web 服务的详细信息，请参阅 Microsoft Windows SDK 文档。

 

 




