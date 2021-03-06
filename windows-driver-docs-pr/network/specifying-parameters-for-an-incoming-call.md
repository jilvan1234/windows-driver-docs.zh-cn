---
title: 指定来电的参数
description: 指定来电的参数
ms.assetid: f1436c05-f475-454c-b68f-e387821834d4
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络连接、 传入调用
- WDK WAN，传入呼叫的电话服务
- CoNDIS TAPI WDK 网络连接、 传入调用
- 流式处理 WDK networing，传入呼叫语音
- WDK 的 CoNDIS WAN 的传入呼叫
- 调用 WDK 的 CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32e80d8a27e3860d054c959d18cec9bfaac4f716
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383628"
---
# <a name="specifying-parameters-for-an-incoming-call"></a>指定来电的参数





时，该值指示的传入呼叫**Ndis (M) CmDispatchIncomingCall**，呼叫管理器或支持语音的流式处理的 MCM 必须指定以下值中的[**共同\_调用\_管理器\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545381(v=vs.85))结构：

-   最大传输 SDU 大小 (CallMgrParameters-&gt;Transmit.MaxSduSize)

-   最大接收 SDU 大小 (CallMgrParameters-&gt;Receive.MaxSduSize)

此外，调用管理器或 MCM 必须指定以下值的行中\_调用\_信息结构：

-   **ulMediaMode**

    此字段应包含 LINEMEDIAMODE\_AUTOMATEDVOICE，映射到 TAPIMEDIAMODE\_音频 TAPI 3.0 中。

-   **ulCallerIDFlags**

-   **ulCallerIDSize**

-   **ulCallerIDOffset**

-   **ulCallerIDNameSize**

-   **ulCallerIDNameOffset**

-   **ulCalledIDFlags**

-   **ulCalledIDSize**

-   **ulCalledIDOffset**

-   **ulCalledIDNameSize**

-   **ulCalledDNameOffset**

-   **ulCallerIDAddressType**

-   **ulCalledIDAddressType**

呼叫管理器或支持共同以外的地址族的 MCM\_地址\_系列\_TAPI\_代理指定的前面行\_调用\_信息成员时响应[OID\_共同\_TAPI\_TRANSLATE\_NDIS\_CALLPARAMS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-translate-ndis-callparams)查询。

呼叫管理器或支持产生的 CO MCM\_地址\_系列\_TAPI\_代理系列指定的上述行\_调用\_信息中的特定于媒体的一部分的成员CO\_调用\_MANAGER\_参数结构，它提供给**Ndis (M) CmDispatchIncomingCall**。

有关在行中的成员的说明\_调用\_信息结构，请参阅 Microsoft Windows SDK 文档中的 LINECALLINFO 结构。

 

 





