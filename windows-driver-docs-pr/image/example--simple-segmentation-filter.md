---
title: 示例简单分段的筛选器
description: 示例简单分段的筛选器
ms.assetid: 9c77fea4-61d9-4bec-8d8d-35436d00c1ed
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ada6abf55e6f324785bf7b85aa862a64015b1e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540419"
---
# <a name="example-simple-segmentation-filter"></a>示例：简单的分段的筛选器





以下代码示例演示如何实现简单的分段筛选器。 在示例中的分段筛选器不使用[ **WIA\_IPS\_反扭曲\_X** ](https://msdn.microsoft.com/library/windows/hardware/ff552581)并[ **WIA\_IP\_反扭曲\_Y** ](https://msdn.microsoft.com/library/windows/hardware/ff552587)属性。 为清楚起见，省略了错误检查代码。

```cpp
typedef struct _SUB_RECT
{
    LONG  xpos;
    LONG  ypos;
    LONG  width;
    LONG  height;
} SUB_RECT;

STDMETHODIMP
SegFilter::DetectRegions(IN IStream  *pInputStream,
                         IN IWiaItem2  *pWiaItem2)
{
    HRESULT   hr = S_OK;
    SUB_RECT  pSubRegions = NULL;
    ULONG     cRegionsFound = 0;
    LONG      parent_xpos, parent_ypos;
    GUID      formatGUID = {0};

    LONG  lItemFlags = WiaItemTypeGenerated |
                       WiaItemTypeTransfer |
                       WiaItemTypeImage |
                       WiaItemTypeFile |
                       WiaItemTypeProgrammableDataSource;

    LONG  lCreationFlags = COPY_PARENTS_PROPERTY_VALUES;

    ReadPropertyGUID(pWiaItem2, WIA_IPA_FORMAT, &formatGUID);

    //
    // The algorithm that performs the actual region
    // detection has been omitted for clarity.
    //
    FindSubRegions(pInputStream,
                   formatGUID,
                   &pSubRegions,
                   &cRegionsFound);

    ReadPropertyLong(pWiaItem2, WIA_IPS_XPOS, &parent_xpos);
    ReadPropertyLong(pWiaItem2, WIA_IPS_YPOS, &parent_ypos);

    //
    // For each subimage that was found, create
    // a child item under pWiaItem2 into which
    // the coordinates for the subimage are set.
    //
    for (int i = 0; i < cRegionsFound; i++)
    {
        BSTR       bstrChildName = NULL;
        BSTR       bstrFullChildName = NULL;
        IWiaItem2  *pChildIWiaItem = NULL;

        GetNamesForChild(i,
                         &bstrChildName,
                         &bstrFullChildName);

        pWiaItem2->CreateChildItem(lItemFlags,
                                   lCreationFlags,
                                   bstrChildName,
                                   &pChildIWiaItem);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_XPOS,
                          parent_xpos + pSubRegions[i].xpos);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_YPOS,
                          parent_ypos + pSubRegions[i].ypos);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_XEXTENT,
                          pSubRegions[i].width);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_YEXTENT,
                          pSubRegions[i].height);

        pChildIWiaItem->Release();
        SysFreeString(bstrChildName);
        SysFreeString(bstrFullChildName);
    }

    if (pSubRegions)
    {
        free(pSubRegions);
    }

    return hr;
}
```

 

 



