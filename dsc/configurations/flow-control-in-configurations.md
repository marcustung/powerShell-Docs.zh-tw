---
ms.date: 12/12/2018
keywords: dsc,powershell,設定,安裝
title: 設定中的條件陳述式及迴圈
ms.openlocfilehash: 0073d94d28afbb45bb635442129a6cddde4c805a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2018
ms.locfileid: "53400655"
---
# <a name="conditional-statements-and-loops-in-configurations"></a>設定中的條件陳述式及迴圈

您可以讓您[組態](configurations.md)更為動態使用 PowerShell 的流程控制關鍵字。 本文將說明如何使用條件陳述式和迴圈將您的設定更為動態。 結合條件和迴圈[參數](add-parameters-to-a-configuration.md)並[組態資料](configData.md)可讓您更多的彈性和控制編譯您的設定時。

就像函式或指令碼區塊，您可以使用任何 PowerShell 語言設定中。 當您呼叫您的組態來編譯 」.mof"檔案時，才會評估您所使用的陳述式。 下列範例示範簡單的案例來示範概念。 條件會使用參數和設定資料更常使用迴圈。

在此簡單範例中，**服務**資源區塊會擷取服務的目前狀態，在編譯時期產生 「.mof 」 檔案，以維護其目前的狀態。

> [!NOTE]
> 使用動態資源區塊將會優先於 Intellisense 的效能。 PowerShell 剖析器無法判斷指定的值是否可接受之前編譯設定。

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Service Spooler
        {
            Name = "Spooler"
            State = $(Get-Service -Name 'spooler').Status
            StartType = $(Get-Service -Name 'spooler').StartType
        }
    }
}
```

此外，您可以建立**服務**封鎖目前的電腦上的每個服務的資源使用`foreach`迴圈。

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Foreach ($service in $(Get-Service))
        {
            Service $service.Name
            {
                Name = $service.Name
                State = $service.Status
                StartType = $service.StartType
            }
        }
    }
}
```

您可以也只會建立都在線上，使用簡單的機器組態`if`陳述式。

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration

    Foreach ($computer in @('Server01', 'Server02', 'Server03'))
    {
        if (Test-Connection -ComputerName $computer)
        {
            Node $computer
            {
                Service "Spooler"
                {
                    Name = "Spooler"
                    State = "Started"
                }
            }
        }
    }
}
```

> [!NOTE]
> 動態資源會封鎖在上面的範例參考目前的電腦。 在這種情況是您要撰寫組態的機器，不是目標節點。

<!---
Mention Get-DSCConfigurationFromSystem
-->

## <a name="summary"></a>摘要

在 [摘要] 中，您可以使用設定中的任何 PowerShell 語言。

這包括像是：

- 自訂物件
- 雜湊表
- 字串操作
- 遠端
- WMI 和 CIM
- Active Directory 物件
- 及其他...

在組態中定義任何 PowerShell 程式碼將會評估編譯時間，但您也可以將程式碼放在指令碼中包含您的組態。 當您匯入您的設定，將會執行組態區塊之外的任何程式碼。

## <a name="see-also"></a>另請參閱

- [將參數新增至設定](add-parameters-to-a-configuration.md)
- [從設定中分離設定資料](configData.md)
