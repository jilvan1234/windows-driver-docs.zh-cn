---
title: 编写电池微型类驱动程序
description: 编写电池微型类驱动程序
ms.assetid: 4135af1a-1448-46ad-af6f-26ce8aee6b1d
keywords:
- 电池 miniclass 驱动程序 WDK
- 电池 miniclass 驱动程序 WDK，有关编写电池 miniclass 驱动程序
- 独立于设备的电池支持 WDK
- 特定于设备的电池支持 WDK
- 电池类驱动程序 WDK
- 电池类驱动程序 WDK、 有关电池类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc25453bdb285ae71edd8fd64d59296ccc9115a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328418"
---
# <a name="writing-battery-miniclass-drivers"></a>编写电池微型类驱动程序


## <span id="ddk_writing_battery_miniclass_drivers_dg"></span><span id="DDK_WRITING_BATTERY_MINICLASS_DRIVERS_DG"></span>


电池通常有一对驱动程序：Microsoft 提供的通用电池类驱动程序，以及专门为具体电池类型编写的小型驱动程序。

类驱动程序定义系统中电池的整体功能，并与电源管理器进行交互。

Miniclass 驱动程序处理特定于设备的功能，例如添加和删除电池，以及跟踪的其容量和费用。 Miniclass 驱动程序将导出的类驱动程序调用以获取有关它控制的设备的信息的例程。

有关编写电池 miniclass 驱动程序信息的组织方式如下：

[系统电池管理概述](overview-of-system-battery-management.md)

[电池类和 Miniclass 驱动程序的交互](interaction-of-battery-class-and-miniclass-drivers.md)

[提供所需的电池 Miniclass 驱动程序的功能](supplying-required-battery-miniclass-driver-functionality.md)

[DriverEntry 例程的电池 Miniclass 驱动程序](driverentry-routine-of-a-battery-miniclass-driver.md)

[AddDevice 例程的电池 Miniclass 驱动程序](adddevice-routine-of-a-battery-miniclass-driver.md)

[DispatchDeviceControl Routine 电池 Miniclass 驱动程序](dispatchdevicecontrol-routine-of-a-battery-miniclass-driver.md)

[DispatchSystemControl Routine 电池 Miniclass 驱动程序](dispatchsystemcontrol-routine-of-a-battery-miniclass-driver.md)

[响应电池类驱动程序查询](responding-to-battery-class-driver-queries.md)

[提供设备电池严重短缺通知](supplying-battery-device-notification.md)

[卸载电池 Miniclass 驱动程序例程](unload-routine-of-a-battery-miniclass-driver.md)

[安装电池驱动程序](installing-a-battery-driver.md)

 

 




