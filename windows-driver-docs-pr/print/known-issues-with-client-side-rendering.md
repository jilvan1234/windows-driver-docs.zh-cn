---
title: 客户端呈现的已知问题
description: 客户端呈现的已知问题
ms.assetid: ad17639d-6671-466b-8f72-e635e79fd1cc
keywords:
- 客户端呈现 WDK 打印、 已知问题
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5341cd48c106547511308f8abb532bb59540ad15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388131"
---
# <a name="known-issues-with-client-side-rendering"></a>客户端呈现的已知问题

客户端呈现为启用，所有驱动程序默认情况下，因为它对大多数打印机驱动程序是透明的并向用户提供明确的权益。 大多数打印机驱动程序不会启用此功能的任何问题。

如果打印机驱动程序遇到问题，但是，你可以禁用客户端呈现功能，并且打印机驱动程序将呈现等与以前版本的 Windows 操作系统的打印服务器上的打印作业。 系统管理员还可以通过在始终呈现打印作业上的服务器组策略禁用客户端呈现。

> [!NOTE]
> 如果禁用客户端呈现功能，打印作业呈现会转到打印服务器，可以对打印服务器性能产生负面影响。

安装驱动程序包中的打印机驱动程序不会与客户端呈现的问题。

以下列表介绍了一些客户端呈现的已知问题：

- 如果打印机驱动程序使用自定义打印处理器，但客户端计算机上未安装打印处理器，会自动禁用客户端呈现。

  在某些情况下，未配置为驱动程序包的打印机驱动程序的打印处理器可能未安装客户端计算机上在指向并打印过程。 如果打印后台处理程序检测到问题，它将禁用该打印队列的客户端呈现。 若要避免此问题，创建的打印机驱动程序的驱动程序包。

- 如果打印处理器将返回错误，则将禁用打印队列的客户端呈现。

  打印队列禁用客户端呈现后，打印后台处理程序会通过使用服务器端呈现重试打印作业。 请注意，客户端呈现禁用打印队列后，打印队列将不再具有任何如脱机打印的客户端呈现优势。

- 打印机配置数据可能不完整的打印机驱动程序，使用非标准配置数据。

  指向并打印可能不传输使用专有方法进行存储和通信此数据的打印机驱动程序的完整打印机配置数据。 可以通过使用解决此问题**SetPrinterData**或**SetPrinterDataEx**函数来存储打印机配置数据和使用**GetPrinterData**或**GetPrinterDataEx**函数可用于召回打印机配置数据。 有关这些函数的详细信息，请参阅 Microsoft Windows SDK 文档。

- 客户端呈现与驱动程序不匹配。

  当客户端计算机具有不同版本的打印机驱动程序，不是服务器已存在打印机驱动程序不匹配。 通常情况下，打印机驱动程序不匹配时，指向并打印会更新以匹配服务器上的打印机驱动程序的客户端计算机上的打印机驱动程序。 在某些情况下，你可能想要使用与打印服务器上的打印机驱动程序版本不匹配的打印驱动程序版本的客户端计算机上的打印队列。 例如，您可能不希望指向并打印来更新客户端计算机上的打印机驱动程序：

  - 如果客户端计算机上运行时间的打印服务器上的打印机驱动程序的兼容性问题。
  - 若要减少网络流量的结果时指向并打印下载新的打印机驱动程序。
  - 调试或测试时。

  指向并打印可以阻止下载的打印机驱动程序和强制客户端计算机使用最好取而代之的已安装客户端计算机的驱动程序。 若要选择这种行为的值设置为 HKLM\\系统\\CurrentControlSet\\控件\\打印\\*PrinterName*\\PrinterDriverData\\DriverPolicy 注册表项的打印机驱动程序的名称。 替换*PrinterName*而不是可从打印服务器的打印机驱动程序使用的本地可用的打印机驱动程序的打印队列的名称。 在此注册表项中输入的驱动程序名称必须是客户端计算机上的已安装或可用于安装兼容的打印机驱动程序的名称。

  您还可以创建的打印机连接的打印机驱动程序不匹配以编程方式通过调用**AddPrinterConnection2**，设置打印机\_连接\_不匹配标志并指定的名称打印机的打印机驱动程序\_连接\_信息\_1 结构*pConnectionInfo*自变量的引用。 **AddPrinterConnection2** Windows SDK 文档中所述。

- 从 Windows 8 开始，客户端呈现会自动禁用如果 EMFDespoolingSetting 值不是在注册表中存在并且客户端计算机配置文件是移动平台。

  如果客户端，如笔记本电脑或平板电脑设备的移动平台以启用自动保存对功率消耗，后台处理程序时将禁用客户端呈现在注册表中没有此值。 通过调用 SetPrinterData 将打印队列的 EMFDespoolingSetting 值设置为 0，可以启用驱动程序中显式移动平台的客户端的呈现。

  你可以确认是否在计算机配置为移动或桌面的配置文件使用 msinfo32.exe:

  ![msinfo32.exe 配置文件的屏幕截图](images/emfdespoolingsetting.png)

如果在测试期间，你检测到问题时您的打印机驱动程序可能会导致客户端呈现功能，可以为您的驱动程序禁用客户端呈现。 您可以通过调用来禁用驱动程序中的客户端呈现**SetPrinterData**将打印队列的 EMFDespoolingSetting 值设置为 1。 此值将导致连接到要呈现在服务器上的打印作业的打印队列的任何客户端。