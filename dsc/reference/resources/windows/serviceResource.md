---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: DSC Service 資源
ms.openlocfilehash: 09571bd0eaa428e7d0bb7a533d6ad1c0c936e2cf
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2019
ms.locfileid: "55679242"
---
# <a name="dsc-service-resource"></a>DSC Service 資源

> 適用於：Windows PowerShell 4.0、Windows PowerShell 5.0


Windows PowerShell 預期狀態設定 (DSC) 的 **Service** 資源提供了管理目標節點服務的機制。

## <a name="syntax"></a>語法

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## <a name="properties"></a>Properties

|  屬性  |  描述   |
|---|---|
| 名稱| 表示服務名稱。 請注意，有時候和顯示名稱不同。 您可以使用 Get-Service Cmdlet 取得服務清單及其目前狀態。|
| BuiltInAccount| 表示用於服務的登入帳戶。 這個屬性所允許的值如下：**LocalService**， **LocalSystem**，以及**NetworkService**。|
| 認證| 表示執行服務的帳戶認證。 這個屬性與 __BuiltinAccount__ 屬性不能同時使用。|
| DependsOn| 表示必須先執行另一個資源的設定，再設定這個資源。 例如，如果第一個想要執行的資源設定指令碼區塊的識別碼是 __ResourceName__，而它的類型是 __ResourceType__，則使用這個屬性的語法就是 `DependsOn = "[ResourceType]ResourceName"`。|
| StartupType| 表示服務的啟動類型。 這個屬性所允許的值如下：**自動**，**已停用**，和**手動**|
| State| 表示您要確保的服務狀態。|
| 描述 | 表示目標服務的描述。|
| DisplayName | 表示目標服務的顯示名稱。|
| Ensure | 表示系統上是否有目標服務。 請將此屬性設定為**Absent** 以確保目標服務不存在。 屬性設定為 **Present** (預設值)，可確保目標服務存在。|
| 路徑 | 表示新服務的二進位檔路徑。|

## <a name="example"></a>範例

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```