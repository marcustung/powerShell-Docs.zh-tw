---
title: 驗證參數輸入 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameters, validation rules
- validation, examples
- validation
ms.assetid: 3f15bf20-a068-4a7d-a170-bc43f755d1fe
caps.latest.revision: 14
ms.openlocfilehash: 171e3e974619e197a0bcc9dfc759297005e34568
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2019
ms.locfileid: "57429834"
---
# <a name="validating-parameter-input"></a>驗證參數輸入

PowerShell 可以驗證傳遞至數種方式中的 cmdlet 參數的引數。
PowerShell 可以在長度、 範圍及引數的字元模式的驗證。
它可以驗證引數可用 （計數） 的數目。
這些驗證規則是由宣告 cmdlet 類別的公用屬性的參數屬性使用的驗證屬性定義。

若要驗證參數的引數，PowerShell 執行階段會使用驗證屬性所提供的資訊來執行此指令程式之前，請確認參數的值。
如果參數輸入不是有效的則使用者會收到一則錯誤訊息。
每個驗證參數定義驗證規則會強制執行 powershell。

PowerShell 會強制執行驗證規則，根據下列屬性。

### <a name="validatecount"></a>ValidateCount

指定最小和最大數目的參數可以接受的引數。
如需詳細資訊，請參閱 < [ValidateCount 屬性宣告](./validatecount-attribute-declaration.md)。

### <a name="validatelength"></a>ValidateLength

參數的引數中指定最小和最大的字元數。
如需詳細資訊，請參閱 < [ValidateLength 屬性宣告](./validatelength-attribute-declaration.md)。

### <a name="validatepattern"></a>ValidatePattern

指定驗證參數的引數的規則運算式。
如需詳細資訊，請參閱 < [ValidatePattern 屬性宣告](./validatepattern-attribute-declaration.md)。

### <a name="validaterange"></a>ValidateRange

指定參數的引數的最小和最大值。
如需詳細資訊，請參閱 < [ValidateRange 屬性宣告](./validaterange-attribute-declaration.md)。

### <a name="validateset"></a>ValidateSet

指定參數的引數的有效值。
如需詳細資訊，請參閱 < [ValidateSet 屬性宣告](./validateset-attribute-declaration.md)。

## <a name="see-also"></a>另請參閱

[如何驗證參數的輸入](./how-to-validate-parameter-input.md)

[撰寫 Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)
