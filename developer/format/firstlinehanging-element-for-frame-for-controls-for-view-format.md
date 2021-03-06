---
title: 用於檢視 （格式） 的控制項的畫面格 FirstLineHanging 項目 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53694f08-57f7-4185-b443-1636a0918afc
caps.latest.revision: 8
ms.openlocfilehash: 387340cd9b0aae2ad0419b187d96ab4fee183d5a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2019
ms.locfileid: "56858714"
---
# <a name="firstlinehanging-element-for-frame-for-controls-for-view-format"></a>檢視之控制項的框架的 FirstLineHanging 元素 (格式)

指定資料的第一行向左移動的字元數。 定義可供檢視的控制項時，會使用這個項目。

組態項目 （格式） ViewDefinitions 項目 （格式） 檢視項目 （格式） 項目 （格式） 控制項的 Controls 項目控制項的檢視 （格式） CustomEntries 項目控制項的控制項的檢視 （格式） CustomControl 項目CustomControl CustomEntries CustomEntry 如 CustomItem 檢視 （格式） FirstLineHanging 項目的控制項的檢視 （格式） 框架項目控制項的檢視 （格式） CustomItem 元素的控制項的檢視 （格式） CustomEntry 元素畫面格的控制項的檢視 （格式）

## <a name="syntax"></a>語法

```xml
<FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
```

## <a name="attributes-and-elements"></a>屬性與元素

下列各節說明屬性、 子項目和父項目`FirstLineHanging`項目。

### <a name="attributes"></a>屬性

無。

### <a name="child-elements"></a>子元素

無。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[用於檢視 （格式） 的控制項 CustomItem 的框架項目](./frame-element-for-customitem-for-controls-for-view-format.md)|定義資料的顯示方式，例如將資料轉移至左邊或右邊。|

## <a name="text-value"></a>文字值

指定您想要移動資料的第一行的字元數。

## <a name="remarks"></a>備註

如果未指定這個項目，您無法指定[FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-view-format.md)項目。

## <a name="see-also"></a>另請參閱

[用於檢視 （格式） 的控制項的畫面格 FirstLineIndent 項目](./firstlineindent-element-for-frame-for-controls-for-view-format.md)

[用於檢視 （格式） 的控制項 CustomItem 的框架項目](./frame-element-for-customitem-for-controls-for-view-format.md)

[撰寫 PowerShell 格式化檔案](./writing-a-powershell-formatting-file.md)
