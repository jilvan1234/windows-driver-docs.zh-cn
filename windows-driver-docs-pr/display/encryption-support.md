---
title: 加密支持
description: 加密支持
ms.assetid: d5ce9c02-7126-4775-bb87-dae45b93b652
keywords:
- 视频解码 WDK DirectX VA，加密
- 解码视频 WDK DirectX VA，加密
- 图片解码 WDK DirectX VA，加密
- 加密 WDK DirectX VA
- 加密 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe5243f7c23db8ab9a16b914be54faa2f4bd77e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838952"
---
# <a name="encryption-support"></a>加密支持


## <span id="ddk_encryption_support_gg"></span><span id="DDK_ENCRYPTION_SUPPORT_GG"></span>


对于以下结构和数据类型，可以对视频解码中使用的数据进行加密：

-   宏块控件命令结构

-   残留差异块结构

-   位流缓冲区

为了使主机解码器使用加密，必须确定加速器支持的加密类型。 有关加速器支持的加密类型的信息包含在作为视频加速器格式 Guid 提供给主机的加密类型 Guid 列表中。 有关视频加速器格式 Guid 的详细信息，请参阅 Microsoft Windows SDK 文档。

**请注意**   所有 DirectX VA 加速器都必须能够在不使用加密的情况下运行。 支持不加密，因此不需要声明，并且不能在视频加速器格式 GUID 列表中发送 DXVA\_NoEncrypt "无加密" GUID。

 

主机选择要应用的加密协议类型，并通过将 GUID 发送到加速器来指示此选择。 在典型的加密方案中，需要执行两个步骤，然后才能成功传输加密数据：

1.  主机解码器可能要求验证加速器是否有权接收数据。 可以通过将已签名的结构传递到主机来提供此验证，以证明它持有授权的公钥/私钥对。

2.  然后，主机解码器向加速器发送加密内容密钥。

初始化加密协议的准确步骤数取决于所使用的加密类型和实现方式。

要传递所需的加密初始化参数的主机和快捷键之间交换的每个数据集都必须以加密协议类型 GUID 为前缀。 此 GUID 将一种类型的加密的数据从另一种类型的数据中区分开来。 这是必需的，因为一种类型的加密可用于一个 DirectX VA 缓冲区，另一种类型的加密可用于另一个 DirectX VA 缓冲区。

[**DXVA\_EncryptProtocolHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)结构用于指示正在使用加密协议以及所使用的加密类型。

 

 





