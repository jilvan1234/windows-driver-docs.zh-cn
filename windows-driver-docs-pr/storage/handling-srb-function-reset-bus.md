---
title: 处理 SRB_FUNCTION_RESET_BUS
description: 处理 SRB_FUNCTION_RESET_BUS
ms.assetid: 285cbd5c-e364-4f0f-9020-0bc6f3d45cac
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_RESET_BUS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fac1ca0389068fd7f130d8e2cc14e9850911fc0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371173"
---
# <a name="handling-srbfunctionresetbus"></a>处理 SRB\_函数\_重置\_总线


## <span id="ddk_handling_srb_function_reset_bus_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_RESET_BUS_KG"></span>


系统端口驱动程序始终将其自身重置总线请求发送到微型端口驱动程序的直接[ *HwScsiResetBus* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))例程中所述[SCSI 微型端口驱动程序 HwScsiResetBus例程](scsi-miniport-driver-s-hwscsiresetbus-routine.md)。

但是，有可能[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))例程，以调用使用在其中 SRB**函数**成员设置为 SRB\_函数\_重置\_总线如果基于 NT 的操作系统存储类驱动程序请求此操作。 *HwScsiStartIo*例程可以简单地调用*HwScsiResetBus*例程，以满足传入总线重置请求。

 

 




