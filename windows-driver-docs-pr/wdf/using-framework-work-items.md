---
title: 使用框架工作项
description: 使用框架工作项
ms.assetid: d7e6d187-bed4-4071-a50b-90f32c4f0d5a
keywords:
- 工作项 WDK KMDF
- 队列 WDK KMDF，框架工作项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cb0ebea7d4dd3bc2afeb064c3058aa9c1a130f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843079"
---
# <a name="using-framework-work-items"></a>使用框架工作项





*工作项*是驱动程序在[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)事件回调函数中执行的任务。 在系统工作线程的上下文中，这些函数在 IRQL = 被动\_级别上以异步方式运行。

基于框架的驱动程序通常使用工作项（如果[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[*EVTDPCFUNC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)函数以 IRQL = 调度\_级别运行），则必须在 IRQL = 被动\_级别执行额外的处理。

换句话说，如果运行于 IRQL = 调度的函数\_级别，则驱动程序可以使用工作项必须调用只能在 IRQL = 被动\_级别调用的函数。

通常，驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数会创建一个工作项对象，并将其添加到系统的工作项队列中。 然后，系统工作线程取消排队对象并调用工作项的[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数。

### <a name="sample-drivers-that-use-work-items"></a>使用工作项的示例驱动程序

使用工作项的[基于框架的示例驱动程序](sample-kmdf-drivers.md)包括1394、AMCC5933、PCIDRV 和 Toaster。

### <a href="" id="ddk-setting-up-a-work-item-df"></a>设置工作项

若要设置工作项，驱动程序必须：

1.  创建工作项。

    驱动程序调用[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)来创建工作项对象，并标识将处理该工作项的[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数。

2.  存储有关工作项的信息。

    通常，驱动程序使用工作项对象的上下文内存来存储有关[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数应执行的任务的信息。 调用*EvtWorkItem*回调函数时，它可以通过访问此上下文内存来检索信息。 有关如何分配和访问上下文内存的信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

3.  将工作项添加到系统的工作项队列中。

    驱动程序调用[**WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，这会将驱动程序的工作项添加到工作项队列。

当驱动程序调用[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)时，它必须提供框架设备对象或框架队列对象的句柄。 当系统删除该对象时，它还会删除与该对象关联的任何现有工作项。 将释放工作项对象，并在调用父对象的[*EvtCleanupCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)回调之前清除其关联的工作项回调。

有关框架对象层次结构的清理规则的详细信息，请参阅[框架对象生命周期](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)。

### <a href="" id="ddk-using-the-work-item-callback-function-df"></a>使用工作项回调函数

在将工作项添加到工作项队列后，它将保留在队列中，直到系统工作线程变为可用。 系统工作线程将从队列中删除工作项，然后调用驱动程序的[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数，并将工作项对象作为输入传递。

通常， [*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数执行以下步骤：

1.  通过访问工作项对象的上下文内存获取有关工作项的驱动程序提供的信息。

2.  执行指定的任务。 如有必要，回调函数可以调用[**WdfWorkItemGetParentObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemgetparentobject)来确定工作项的父对象。

3.  调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，以删除工作项对象; 或者，如果驱动程序将重新排队工作项，则指示工作项的句柄现在可重复使用。

每个工作项的回调函数执行的任务必须相对较短。 操作系统提供有限数量的系统工作线程，因此，如果您的驱动程序使用工作项回调函数来执行耗时的任务，则您的驱动程序会影响系统性能。

### <a href="" id="ddk-creating-and-deleting-work-items-df"></a>创建和删除工作项

驱动程序可以使用以下两种方法之一来创建和删除工作项：

-   每个工作项一次：在需要时创建工作项，并在使用后立即将其删除。

    此方法对于需要少量工作项（每分钟不超过一次）的驱动程序很有用。

    例如，驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数可以调用[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate) ，然后调用[**WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，工作项的[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数可以调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。

    如果你的驱动程序遵循这种情况，并且其[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数收到的状态\_\_资源从[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)中返回值不足，则驱动程序必须能够推迟所需的工作，直到系统资源（通常为内存）变得可用。

-   根据需要创建一个或多个驱动程序会的工作项。

    此方法对于经常使用工作项的驱动程序很有用（每分钟更多次），或者如果驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数无法轻松地处理状态\_\_资源返回值[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)。

    在驱动程序调用[**WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)之前，系统不会将工作线程分配给工作项。 因此，尽管系统工作线程是有限的资源，但在初始化设备时创建工作项会消耗少量的内存，但不会影响系统性能。

    以下步骤描述了可能的方案：

    1.  驱动程序的[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用[**WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)来获取工作项句柄。
    2.  驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数使用步骤1中的句柄创建[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数必须执行的操作的列表，然后调用[**WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)。
    3.  驱动程序的[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数执行操作列表，并设置标志以指示回调函数已运行。

    接下来，每次调用驱动程序的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数时，它必须确定[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数是否已运行。 如果*EvtWorkItem*回调函数尚未运行， *EvtInterruptDpc*回调函数将不会调用[**WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，因为工作项仍处于排队。 在这种情况下， *EvtInterruptDpc*回调函数仅更新*EvtWorkItem*回调函数的操作列表。

    每个工作项都与设备或队列关联。 删除关联的设备或队列后，框架会删除所有关联的工作项，因此，如果使用此方法，则驱动程序不必调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。

几个驱动程序可能需要调用[**WdfWorkItemFlush**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemflush)以从工作项队列中刷新其工作项。 有关使用**WdfWorkItemFlush**的示例，请参阅该方法的参考页。

如果驱动程序在未完成的工作项上调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) ，则结果取决于工作项的状态：

|工作项状态|结果|
|-|-|
|已创建但未排队|立即清理工作项。|
|Ddr|对[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)的调用将等待，直到工作项完成执行，然后清理工作项|
|运行|如果驱动程序从[*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)内调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) （在同一线程上），则[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)将立即返回。 [*EvtWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)完成后，将清理工作项。  否则， [**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)将等待 EvtWorkItem 完成。|

 





