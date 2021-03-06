---
title: Bug 检查 0x139 KERNEL_SECURITY_CHECK_FAILURE
description: KERNEL_SECURITY_CHECK_FAILURE bug 检查具有 0x00000139 值。 检查此错误指示在内核检测到的关键数据结构损坏。
ms.assetid: C0E5C625-13DB-4B3A-8080-69CEB963A299
keywords:
- Bug 检查 0x139 KERNEL_SECURITY_CHECK_FAILURE
- Bug 检查 0x139 KERNEL_SECURITY_CHECK_FAILURE
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- Bug Check 0x139 KERNEL_SECURITY_CHECK_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7bf5a483ddc7a396a4676ba640b7209e68a6fd5b
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520288"
---
# <a name="bug-check-0x139-kernelsecuritycheckfailure"></a>Bug 检查 0x139：内核\_安全\_检查\_失败


内核\_安全\_检查\_故障错误检查的值为 0x00000139。 检查此错误指示在内核检测到的关键数据结构损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="bug-check-0x139-kernelsecuritycheckfailure-parameters"></a>Bug 检查 0x139 内核\_安全\_检查\_失败参数


| 参数 | 描述                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 损坏的类型。 有关详细信息，请参阅下表。      |
| 2         | 导致异常的 bug 检查陷阱帧的地址       |
| 3         | 导致错误检查的异常的异常记录的地址 |
| 4         | 保留                                                                    |

 

下表介绍参数 1 可能的值。

| 参数 1 | 描述                                                                                                                                                                                                                                                                                                       |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0 | 已基于堆栈的缓冲区溢出 （旧 /GS 冲突）。                                                                                                                                                                                                                                                     |
| 1  |  VTGuard 检测代码检测到尝试使用非法虚函数表。 通常情况下，C++对象已损坏，，然后调用虚拟方法已尝试使用损坏的对象**这**指针。                                                                                     |
| 2  |  堆栈 cookie 检测代码检测到基于堆栈的缓冲区溢出 （/GS 冲突）。                                                                                                                                                                                                                          |
| 3  |  列表\_条目已损坏 （例如，重复移除）。 有关详细信息，请参阅以下原因部分。                                                                                                                                                                                                |
| 4  |  保留                                                                                                                                                                                                                                                                                                          |
| 5  |  将无效参数视为严重的函数传递的参数无效。                                                                                                                                                                                                                            |
| 6  |  加载程序未正确初始化堆栈 cookie 安全性 cookie。 这可能引起生成仅在 Windows 8 上运行的驱动程序并尝试加载早期版本的 Windows 上的驱动程序映像。 若要避免此问题，必须生成要在早期版本的 Windows 上运行的驱动程序。 |
| 7  |  已请求严重的程序退出。                                                                                                                                                                                                                                                                               |
| 8  |  由编译器插入的数组边界检查检测到非法数组索引操作。                                                                                                                                                                                                                       |
| 9  |  调用**RtlQueryRegistryValues**已指定 RTL\_查询\_注册表\_直接而无需 RTL\_查询\_注册表\_一次，并目标值当时不处于受信任的系统配置单元。                                                                                                                             |
|   10 |  间接调用防护检查检测到无效的控制传输。 |
|   11 | 写入防护检查检测到无效内存写入。 |
|   12 | 尝试切换到无效的纤程上下文。 |
|   13 | 尝试分配一个无效的寄存器上下文。 |
|   14 | 一个对象的引用计数无效。 |
|   18 | 尝试切换到无效 jmp_buf 上下文。 |
|   19 | 对只读数据进行不安全的修改。 |
|   20 | 一个加密自我测试失败。 |
|   21 | 检测到无效的异常链。 |
|   22 | 发生了加密库错误。 |
|   23 | 无效的调用已从 DllMain 中进行。 |
|   24 | 检测到无效的映像基址。 |
|   25 | 保护延迟加载导入时遇到无法恢复的错误。 |
|   26 | 调用了不安全的扩展。 |
|   27 | 调用不推荐使用的服务。 |
|   28 | 检测到的边界缓冲区访问权限进行查看。 |
|   29 | RTL_BALANCED_NODE RBTree 条目已损坏。 |
|   37 | 范围切换 jumptable 条目的情况下调用。 |
|   38 | Longjmp 尝试访问无效的目标。 |
|   39 | 取消导出调用目标无法进行有效的调用目标。 |
 

<a name="cause"></a>原因
-----

使用参数 1 表和转储文件，就可以以缩小此类型的许多 bug 检查的原因。

列表\_条目损坏可能很难跟踪和检查，指示为双向链接列表 （各列表项元素添加到时检测到或从列表中删除） 引入了不一致此 bug。 遗憾的是，不一致的问题是不一定在检测到损坏发生的时间以便做一些探查工作可能有必要确定根本原因。

列表项损坏的常见原因包括：

-   驱动程序损坏了内核同步对象，如 KEVENT （例如双时在线程仍然等待在该相同 KEVENT 上初始化 KEVENT 或允许基于堆栈的 KEVENT，而另一个线程正在使用该 KEVENT 超出范围）。 在 nt 通常会发生这种类型的 bug 检查 ！Ke\*或 nt ！Ki\*代码。 它可能在当线程完成等待同步对象或当代码尝试将同步的对象处于已发出信号状态。 通常情况下，被发送信号的同步对象是一个已损坏。 有时，驱动程序验证程序特殊池可帮助跟踪问题所在，（如果已释放的池块中已损坏的同步对象）。
-   驱动程序损坏了定期 KTIMER。 在 nt 通常会发生这种类型的 bug 检查 ！Ke\*或 nt ！Ki\*代码，并涉及到信号一个计时器，或插入或从计时器表中删除一个计时器。 计时器操作可能是已损坏，但它可能需要检查与计时器表[ **！ 计时器**](-timer.md) （或手动遍历计时器列表链接） 来标识的计时器已已损坏。 有时，驱动程序验证程序特殊池可帮助跟踪问题所在，（如果已释放的池块中已损坏的 KTIMER）。
-   驱动程序具有错误的内部列表管理\_条目样式链接的列表。 一个典型的示例会在调用**RemoveEntryList**两次上而无需重新插入两者之间的列表项相同的列表条目**RemoveEntryList**调用。 其他变体是可能的如双插入到同一列表中的条目。
-   驱动程序释放包含列表的数据结构\_导致损坏，无法检测到更高版本时重新使用旧的池块后检查列表不会从其相应的列表，删除的数据结构的条目。
-   驱动程序已使用列表\_以并发方式不正确的同步，从而导致撕裂更新到列表项的形式列出。

在大多数情况下，可以确定损坏的数据结构，同时向前和向后的每个步骤的链接的列表 ( [ **dl** ](dl--display-linked-list-.md)并**dlb**命令可用于此目的），并比较结果。 该列表是不一致之间向前和向后遍历通常是损坏的位置。 由于链接的列表更新操作可以修改的相邻元素的列表链接，您应查看损坏的列表项的邻居密切，因为它们可能是基础的罪魁祸首。

因为许多系统组件在内部使用列表\_项列出了，由驱动程序使用 Api 可能会导致系统管理的链接列表中的链接的列表损坏的系统资源管理不善的各种类型。

<a name="resolution"></a>分辨率
----------

确定导致此问题通常需要使用调试器以收集其他信息。 应检查多个转储文件，以查看此停止代码是否具有类似特征，例如停止代码出现时运行的代码。

有关详细信息，请参阅[使用 Windows 调试器 (WinDbg) 的故障转储分析](crash-dump-files.md)， [Using ！ 分析扩展](using-the--analyze-extension.md)并[！ 分析](-analyze.md)。

使用事件日志以查看是否存在此停止代码导致发生的更高级别事件。

这些常规故障排除提示可能会有所帮助。

-   如果你最近添加到系统中，请尝试删除或替换它的硬件。 或者，请与制造商联系，以了解是否有任何修补程序。

-   如果最近，添加新设备驱动程序或系统服务尝试删除或更新它们。 尝试确定导致新的错误检查代码才会显示在系统中更改的内容。

-   检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

-   查找范围**设备管理器**若要查看的任何设备都带有感叹号 （！）。 查看任何错误的驱动程序的驱动程序属性中显示的事件日志。 请尝试更新相关的驱动程序。

-   运行病毒检测程序。 病毒可能会感染所有类型的 for Windows，格式化的硬盘，并生成磁盘损坏可生成系统 bug 检查代码。 请确保病毒检测程序会检查存在感染主启动记录。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

 

 




