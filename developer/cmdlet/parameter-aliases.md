---
title: 參數別名 |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c9096a1-46fa-48ea-9b8a-a583484b9d68
caps.latest.revision: 13
ms.openlocfilehash: 6545e71ea18d10621ee9c203e70f64dece460ef5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2019
ms.locfileid: "56853314"
---
# <a name="parameter-aliases"></a>參數別名

Cmdlet 參數也可以有別名。 當您輸入，或在命令中指定的參數，您可以使用別名而不是參數名稱。

## <a name="benefits-of-using-aliases"></a>使用別名的優點

將別名加入至參數提供下列優點。

- 您可以提供捷徑，讓使用者不必呼叫此指令程式時，請使用完整的參數名稱。 例如，您可以使用"CN"別名，而不是參數名稱的電腦 「 名稱 」。

- 如果您想要提供不同的名稱相同的參數，您可以定義多個別名。 您可以定義多個別名，如果您必須使用不同的方式參考相同資料的多個使用者群組。

- 您可以提供回溯相容性的現有指令碼參數的名稱變更時。

- 藉由使用別名屬性，以及 ValueFromPipelineByName 屬性，您可以定義使用參數，讓您將繫結至不同的物件類型的 cmdlet。 例如，假設您有兩個不同類型的物件和第一個物件擁有寫入器屬性，第二個物件擁有編輯器屬性。 如果您的 cmdlet 的參數，必須接受管線輸入屬性名稱的寫入器和編輯器的別名和 cmdlet，cmdlet 可以將繫結至這兩種使用兩個參數別名的物件。

如需有關可以搭配特定參數的別名的詳細資訊，請參閱[常見的參數名稱](./common-parameter-names.md)。

## <a name="defining-parameter-aliases"></a>定義參數別名

若要定義參數的別名，宣告別名屬性，如下列的參數宣告中所示。 在此範例中，針對相同的參數定義多個別名。 (如需詳細資訊，請參閱 <<c0> [ 如何宣告 Cmdlet 參數](./how-to-declare-cmdlet-parameters.md)。)

```csharp
[Alias("UN","Writer","Editor")]
[Parameter()]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

## <a name="see-also"></a>另請參閱

[常見的參數名稱](./common-parameter-names.md)

[如何宣告 Cmdlet 參數](./how-to-declare-cmdlet-parameters.md)

[撰寫 Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)
