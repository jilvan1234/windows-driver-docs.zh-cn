---
title: 筛选数据
description: 为了优化数据吞吐量，传感器设备必须应用筛选器条件的数据更新事件，以便它们仅在需要时引发。
ms.assetid: 1895EC5C-08C1-4976-83F2-CD5A2B55338D
keywords:
- 更改敏感度
- 传感器变化敏感度
- CS
- 当前报告间隔
- 传感器当前报告间隔
- CRI
- 数据更新事件
- 传感器事件
- 传感器事件
- 筛选数据
- 数据筛选
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b96b1bbdda31d970127dc4ee1c1ddf763cba7a14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377801"
---
# <a name="filtering-data"></a>筛选数据


为了优化数据吞吐量，传感器设备必须应用筛选器条件的数据更新事件，以便它们仅在需要时引发。 此筛选将导致较低的 CPU 利用率 （由于减少了的传感器吞吐量） 和更少的功耗 （无论是传感器和 CPU）。

有两个值 （或属性） 的支持传感器设备的筛选条件。 第一个是当前报表时间间隔内 (CRI) 和第二个是变化敏感度 (CS)。 两个属性可以由传感器应用程序设置。

当前报告间隔是以毫秒为单位的数据更新的客户端希望接收有意义的更改发生时之间的最短期限。 变化敏感度是用来指定有意义的更改的值 （或百分比）。

因此，气象站应用程序可能会指定当前报告间隔 (CRI) 为 60000 温度传感器 （或一分钟）。 和温度传感器会要求变化敏感度的值 （而不是百分比表示）。 例如，如果此温度传感器返回摄氏度，而更改敏感度值温度为 2.0，此特定传感器将只会引发数据更新事件时，温度，按增大或减小，2.0 摄氏度通过请求的报表时间间隔内 （在此情况下，一分钟）。

环境光线传感器 (ALS) 是传感器的需要更改的敏感度以指定为百分比的示例。 例如，如果 Illuminance 的更改敏感度值是 2.0，此传感器将解释为百分比值和只会引发数据更新事件时的 LUX 值已删除或增加 2%。

下表列出了六个常见传感器，与每个，关联的数据并相应更改敏感度。

| Sensor             | 数据字段              | 更改敏感度值           |
|--------------------|------------------------|------------------------------------|
| 光传感器       | LUX                    | lux %更改                    |
| 加速计      | 加速 X         | 加速重力               |
|                    | 加速 Y         | 加速重力               |
|                    | 加速 Z         | 加速重力               |
| 三维陀螺测试仪感应       | Angular 速度 X        | Angular 速度 （度 / 秒） |
|                    | Angular 速度 Y        | Angular 速度 （度 / 秒） |
|                    | Angular 速度 Z        | Angular 速度 （度 / 秒） |
| 指南针            | 地方，磁北标题 | 度                            |
|                    | 北标题，则返回 true     | 度                            |
| 测斜仪       | Yaw                    | 度                            |
|                    | 俯仰                  | 度                            |
|                    | Roll                   | 度                            |
| 设备方向 | 四元             | 度移动                   |
|                    | 旋转矩阵        | 度移动                   |

 

下表列出了建议的当前报表时间间隔 (CRI) 默认值。

| 传感器类型   | 推荐的默认报表时间间隔内 |
|---------------|-------------------------------------|
| 环境光线 | 5000                                |
| 加速计 | 100                                 |
| 陀螺测试仪     | 100                                 |
| 指南针       | 100                                 |
| 测斜仪  | 50                                  |
| Orientation   | 50                                  |

 

下表列出了建议的更改敏感度 (CS) 默认值。

|  传感器类型  | 建议使用默认变化敏感度 |
|---------------|----------------------------------------|
| 环境光线 | 50                                     |
| 加速计 | 0.02                                   |
| 陀螺测试仪     | 0.50                                   |
| 指南针       | 0.20                                   |
| 测斜仪  | 0.50                                   |
| Orientation   | 0.50                                   |


## <a name="change-sensitivity-cs-for-the-inclinometer-and-orientation-sensors"></a>倾斜仪和方向传感器更改敏感度 (CS)


倾斜仪和方向传感器的变化敏感度计算方式应为两个四元数之间的角度。 从数学上，这表示为：

2\*cos⁻¹(dot product(q1, q2))

此计算确保在不同的平板电脑 （或设备） 方向的一致性。

## <a name="effective-current-report-interval-cri-and-change-sensitivity-cs"></a>有效的当前报告间隔 (CRI) 和变化敏感度 (CS)


当前报表时间间隔 (CRI) 和给定的传感器的更改敏感度 (CS) 属性，可以设置多个应用程序。 它是您的驱动程序以确定哪些请求的属性应用的责任。 驱动程序设置的属性引用作为有效当前报表的时间间隔内 (E CRI) 和有效更改的敏感度 (E-CS)。

## <a name="setting-the-e-cri-and-e-cs-for-client-applications"></a>为客户端应用程序设置 E CRI 和 E CS


每当客户端应用程序建立的连接的传感器，您的驱动程序将需要设置 E CRI 和 E CS 值。 这些值存储在什么被称为客户端容器。 下表列出了六种方法，传感器驱动程序支持，并指定您的驱动程序应使用其客户端容器和 E CRI 和 E CS 属性执行的操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>感兴趣的事件</td>
<td>事件处理程序活动</td>
</tr>
<tr class="even">
<td>ISensorDriver::OnClientConnect</td>
<td><p>将客户端项添加到客户端容器</p>
<p>根据需要，读取默认 CRI 和 CS 值将存储在客户端容器</p></td>
</tr>
<tr class="odd">
<td>ISensorDriver::OnClientDisconnect</td>
<td><p>从客户端容器中删除客户端和根据需要设置 E CRI 和 E CS 根据剩余客户端</p></td>
</tr>
<tr class="even">
<td>ISensorDriver::OnClientSubscribeToEvents</td>
<td><p>"事件订阅"字段 – 更新 （设置为 true） 的所用的传感器。 打开从传感器报告的事件。</p></td>
</tr>
<tr class="odd">
<td>ISensorDriver::OnClientUnSubscribeToEvents</td>
<td><p>更新"事件订阅"字段 – （设置为 false） 所用的传感器。 如果没有订阅服务器保留，请关闭事件报告从设备。</p></td>
</tr>
<tr class="even">
<td>ISensorDriver::OnSetProperties</td>
<td><p>如果设置了 CS 或 CRI 属性，更新相应的客户端容器字段。</p></td>
</tr>
<tr class="odd">
<td>IFileCallbackCleanup::OnCleanupFile</td>
<td><p>客户端已发生故障或停止响应。 客户端应从客户端容器中删除。</p></td>
</tr>
</tbody>
</table>

 

下表显示使用 4 个连接的客户端应用程序 3D 加速感应器的客户端容器。 （对应于第二个和第 4 行） 这些客户端应用程序的两个已订阅事件。

| 客户端的文件句柄 | 订阅事件 | CRI | CS (X) | CX (Y) | CS (Z) |
|--------------------|----------------------|-----|--------|--------|--------|
| FF80A267           | FALSE                | 50  | .001   | .001   | .001   |
| FF802489           | TRUE                 | 70  | .02    | .02    | .02    |
| FF80D345           | FALSE                | 15  | NULL   | NULL   | NULL   |
| FF803287           | TRUE                 | 100 | .005   | .005   | .005   |

 

该驱动程序评估此连接的客户端组后，它为 E CRI 和 E CS 选择以下值：

-   E-CRI:70
-   E CS 值: （无法折叠到使用最小阈值的单个值）
    -   X:.005
    -   Y:.005
    -   Z:.005

由于事件筛选不适用于这些客户端，请注意，在此示例中没有的事件接收器的客户端设置 （第一个和第三个行） 将被忽略。

## <a name="filtering-data-update-events-by-evaluating-the-effective-cri-and-cs-values-e-cri-e-cs"></a>通过计算有效的 CRI 和 CS 值 (电子 CRI，E CS) 的筛选数据更新事件


一旦当前 E CRI 和 E CS 值已被确定和传感器连接状态更改为更新，传感器设备将使用这些值来筛选连接的客户端应用程序引发的事件。 这些值进行比较的"current"的数据值和以前的数据值之间的差异。 如果 E CS 值超出了某个时间段等于或大于电子 CRI，然后，只有在此时，应引发数据事件。 唯一的例外是传感器设备启动时的默认值应用，以便客户端可以接收正确的通知。

下图演示了如何时间筛选的原始传感器数据以确定应引发数据事件时评估。

![时间筛选传感器数据](images/cri-cs.png)

在上图中，关系图的下半部分中的红色数据表示的原始传感器数据。 绿色行的表示将返回到客户端轮询数据 （一个的多种方式实现此行为） 和"X"值数据的代表数据的事件触发时。 蓝线是 E CS 边界 （+ /-相对于最后一个数据事件值 E CS) 的阈值。

通过实现此事件筛选逻辑，可以极大地减少了更新的事件，数据和应用程序可以仍获取有意义发生更改时通知中的传感器数据。

## <a name="device-runtime-optimizations-for-data-filtering"></a>设备运行时优化的数据筛选


本部分介绍开发传感器驱动程序时应考虑的几个运行时优化。

### <a name="support-interrupts"></a>支持中断

您的驱动程序应依赖于中断而不是轮询设备。 这将导致性能和电源管理改进。 这些改进包括以下内容。

1.  你的设备可以输入基于当前的更改敏感度和报告间隔低功率状态。
2.  使用中断会减少驱动程序和传感器固件中的不必要的代码执行。
3.  使用中断会减少总线活动。

**请注意**  如果驱动程序依赖于中断，但该驱动程序中存在的当前报表时间间隔和变化敏感度逻辑，该驱动程序都有可能收到大量的数据更新之间的中断。 因此，该驱动程序可能需要禁用 （或屏蔽） 中断当前报告间隔过期之前。

 

### <a name="move-change-sensitivity-support-to-the-device"></a>将更改敏感度支持移动到设备

如果您的传感器硬件或固件，支持你应使用此功能来支持变化敏感度的阈值检测。 通过将支持移动到该设备，然后对相应中断作出响应，你可以减少在您的驱动程序中的处理开销。

### <a name="move-report-interval-support-to-the-devices"></a>将报表时间间隔内支持移动到设备

如果您的传感器硬件或固件，支持报表时间间隔内的概念应该使用此功能。

如果您的传感器不提供本机报表时间间隔内支持，请考虑禁用对当前报表时间间隔内的子集的中断。 然后，在此时间过后，检索当前的设备数据。

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



