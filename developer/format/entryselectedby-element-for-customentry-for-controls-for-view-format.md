---
title: 用於檢視 （格式） 的控制項 CustomEntry EntrySelectedBy 項目 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b3d80a7d-3797-4c46-ae74-ae5cda79b24f
caps.latest.revision: 8
ms.openlocfilehash: efb20c3f2077547e6eb3cb28240512b444f9c481
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2019
ms.locfileid: "56859534"
---
# <a name="entryselectedby-element-for-customentry-for-controls-for-view-format"></a>檢視之控制項的 CustomEntry 的 EntrySelectedBy 元素 (格式)

定義使用此控制項定義或必須存在於要使用此定義條件的.NET 類型。 定義可供檢視的控制項時，會使用這個項目。

組態項目 （格式） ViewDefinitions 項目 （格式） 檢視項目 （格式） 項目 （格式） 控制項的 Controls 項目控制項的檢視 （格式） CustomEntries 項目控制項的控制項的檢視 （格式） CustomControl 項目CustomControl CustomEntries CustomEntry 用於檢視 （格式） 的控制項的檢視 （格式） EntrySelectedBy 元素的控制項的檢視 （格式） CustomEntry 元素的控制項

## <a name="syntax"></a>語法

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a>屬性與元素

下列各節說明屬性、 子項目和父項目`EntrySelectedBy`項目。 您必須指定至少一個型別、 選取項目集或選擇條件的定義。 沒有任何子項目的，您可以使用數字的最大限制。

### <a name="attributes"></a>屬性

無。

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[用於檢視 （格式） 的控制項 EntrySelectedBy SelectionCondition 項目](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|選擇性的項目。<br /><br /> 定義要使用此定義必須存在的條件。|
|[用於檢視 （格式） 的控制項 EntrySelectedBy SelectionSetName 項目](./selectionsetname-element-for-entryselectedby-for-controls-for-view-format.md)|選擇性的項目。<br /><br /> 指定一組使用這個控制項定義的.NET 型別。|
|[用於檢視 （格式） 的控制項 EntrySelectedBy TypeName 項目](./typename-element-for-entryselectedby-for-controls-for-view-format.md)|選擇性的項目。<br /><br /> 指定使用這個控制項定義的.NET 型別。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[用於檢視 （格式） 的控制項 CustomEntries CustomEntry 項目](./customentry-element-for-customentries-for-controls-for-view-format.md)|提供控制項的定義。|

## <a name="remarks"></a>備註

選擇條件用來定義的條件必須存在於使用定義，例如當物件只有特定的屬性時，或特定的屬性值，或指令碼會評估`true`。 如需有關選擇條件的詳細資訊，請參閱[定義條件時檢視項目或項目用](./defining-conditions-for-displaying-data.md)。

## <a name="see-also"></a>另請參閱

[用於檢視 （格式） 的控制項 CustomEntries CustomEntry 項目](./customentry-element-for-customentries-for-controls-for-view-format.md)

[撰寫 PowerShell 格式化檔案](./writing-a-powershell-formatting-file.md)
