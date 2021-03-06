---
description: 深入了解 Azure 中的 Desired State Configuration (DSC) 版本歷程記錄。
ms.date: 06/21/2018
keywords: dsc, powershell, azure, 延伸模組
title: Azure DSC 延伸模組版本歷程記錄
ms.openlocfilehash: 2c076e3beccc15e99af2327820916d7a4d28da68
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2019
ms.locfileid: "55679169"
---
# <a name="azure-desired-state-configuration-extension-version-history"></a>Azure Desired State Configuration 延伸模組版本歷程記錄

Azure Desired State Configuration (DSC) VM 延伸模組會視需求進行更新，來支援包含 Windows PowerShell 之 Azure、Windows Server 及 Windows Management Framework (WMF) 所帶來的改善與新功能。

本文將提供有關各 Azure DSC VM 延伸模組版本的資訊、其所支援的環境，以及對新功能或變更的註解。

## <a name="latest-version"></a>最新版本

### <a name="version-276"></a>版本 2.76

- **發行日期：**
  - 2018 年 5 月 9 日 (Azure) | 2018 年 6 月 21 日 (Azure 中國、Azure Government)
- **OS 支援：**
  - Windows Server 2016
  - Windows Server 2012 R2
  - Windows Server 2012
  - Windows Server 2008 R2 SP1
  - Windows 用戶端 7/8.1/10
  - Nano 伺服器
- **WMF 支援：**
  - WMF 5.1
  - WMF 5.0 RTM
  - WMF 4.0 Update
  - WMF 4.0
- **環境：**
  - Azure
  - Azure 中國
  - Azure Government
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - 已改進子狀態與其他次要 Bug 修正的延伸模組中繼資料。

## <a name="supported-versions"></a>支援的版本

> [!WARNING]
> 2.4 到 2.13 版均使用 WMF 5.0 公開預覽，其簽署憑證將於 2016 年 8 月到期。  如需有關此問題的詳細資訊，請參閱[部落格文章](https://blogs.msdn.microsoft.com/powershell/2016/05/24/azure-dsc-extension-versions-2-4-up-to-2-13-will-retire-in-august/)。

### <a name="version-275"></a>2.75 版

- **發行日期：** 2018 年 3 月 5 日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Windows 用戶端 7/8.1/10，Nano Server
- **WMF 支援：** WMF 5.1 中，WMF 5.0 RTM、 WMF 4.0 Update、 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - 在 GitHub 最近對 TLS 1.2 進行的變更後，您無法再利用從可從 Azure Marketplace 取得的自製資源管理員範本將 VM 導入 Azure 自動化 DSC，或使用 DSC 延伸模組取得任何託管在 GitHub 上的設定。 當您部署延伸模組時，會看見類似下例的的錯誤：

    ```json
    {
        "code": "DeploymentFailed",
        "message": "At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/arm-debug for usage details.",
        "details": [{
            "code": "Conflict",
            "message": "{
                \"status\": \"Failed\",
                \"error\": {
                    \"code\": \"ResourceDeploymentFailure\",
                    \"message\": \"The resource operation completed with terminal provisioning state 'Failed'.\",
                    \"details\": [ {
                        \"code\": \"VMExtensionProvisioningError\",
                        \"message\": \"VM has reported a failure when processing extension 'Microsoft.Powershell.DSC'.
                        Error message: \\\"The DSC Extension failed to execute: Error downloading
                        https://github.com/Azure/azure-quickstart-templates/raw/master/dsc-extension-azure-automation-pullserver/UpdateLCMforAAPull.zip
                        after 29 attempts: The request was aborted: Could not create SSL/TLS secure channel..\\nMore information about the failure can
                        be found in the logs located under 'C:\\\\WindowsAzure\\\\Logs\\\\Plugins\\\\Microsoft.Powershell.DSC\\\\2.74.0.0' on the VM.\\\".\"
                    } ]
                }
            }"
        }]
    }
    ```

  - 新的延伸模組版本現在會強制實施 TLS 1.2。 在部署延伸模組時，若您已經將資源管理員範本中的 AutoUpgradeMinorVersion 設定為 true，則延伸模組會自動升級為 2.75。 若要進行手動更新，請在資源管理員範本中指定 `TypeHandlerVersion = 2.75`。

### <a name="version-270---272"></a>2.70 - 2.72 版

- **發行日期：** 2017 年 11 月 13 日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Windows 用戶端 7/8.1/10，Nano Server
- **WMF 支援：** WMF 5.1 中，WMF 5.0 RTM、 WMF 4.0 Update、 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - Bug 修正與改善會簡化透過入口網站 UI 與資源管理員範本使用 DSC Azure 自動化的流程。  如需詳細資訊，請參閱 DSC 延伸模組文件中的[預設設定指令碼](/azure/virtual-machines/extensions/dsc-overview)。

### <a name="version-226"></a>2.26 版

- **發行日期：** 2017 年 6 月 9 日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Windows 用戶端 7/8.1/10，Nano Server
- **WMF 支援：** WMF 5.1 中，WMF 5.0 RTM、 WMF 4.0 Update、 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - 遙測改善。

### <a name="version-225"></a>2.25 版

- **發行日期：** 2017 年 6 月 2 日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Windows 用戶端 7/8.1/10，Nano Server
- **WMF 支援：** WMF 5.1 中，WMF 5.0 RTM、 WMF 4.0 Update、 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - 新增多項 Bug 修正與其他小幅改善項目。

### <a name="version-224"></a>2.24 版

- **發行日期：** 2017 年 4 月 13 日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Nano Server
- **WMF 支援：** WMF 5.1 中，WMF 5.0 RTM、 WMF 4.0 Update、 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - 將 VM UUID 與 DSC 代理程式識別碼公開為延伸模組中繼資料。 同時新增其他小幅度改善項目。

### <a name="version-223"></a>2.23 版

- **發行日期：** 2017 年 3 月 15日日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Nano Server
- **WMF 支援：** WMF 5.1 中，WMF 5.0 RTM、 WMF 4.0 Update、 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - 新增大量 Bug 修正與其他改善項目。

### <a name="version-222"></a>2.22 版

- **發行日期：** 2017 年 2 月 8 日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Nano Server
- **WMF 支援：** WMF 5.1 中，WMF 5.0 RTM、 WMF 4.0 Update、 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - DSC 延伸模組現在具備 WMF 5.1 的支援。
  - 同時新增其他小幅度改善項目。

### <a name="version-221"></a>2.21 版

- **發行日期：** 2016 年 12 月 2 日
- **OS 支援：** Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012 中，Windows Server 2008 R2 SP1，Nano Server
- **WMF 支援：** WMF 5.1 Preview、 WMF 5.0 RTM、 WMF 4.0 更新 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。 針對 Nano 伺服器，DSC 角色會安裝到 VM 上。
- **新功能：**
  - DSC 延伸模組現可在 Nano 伺服器上使用。 此版本主要包含在 Nano 伺服器上執行延伸模組的程式碼變更。
  - 同時新增其他小幅度改善項目。

### <a name="version-220"></a>2.20 版

- **發行日期：** 2016 年 8 月 2 日
- **OS 支援：** Windows Server 2016 Technical Preview、 Windows Server 2012 R2 中，Windows Server 2012、 Windows Server 2008 R2 SP1
- **WMF 支援：** WMF 5.1 Preview、 WMF 5.0 RTM、 WMF 4.0 更新 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 Technical Preview 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。
- **新功能：**
  - WMF 5.1 Preview 的支援。 在首次發佈時，此版本是選用升級，且您必須在資源管理員範本中指定 Wmfversion = ‘5.1PP’ 才能安裝 WMF 5.1 Preview。 指定 Wmfversion = ‘latest’ 仍會安裝 [WMF 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/)。 如需 WMF 5.1 Preview 的詳細資訊，請參照[此部落格]( https://blogs.msdn.microsoft.com/powershell/2016/07/16/announcing-windows-management-framework-wmf-5-1-preview/)。
  - 同時新增其他小幅度修正與改善項目。

### <a name="version--219"></a>2.19 版

- **發行日期：** 2016 年 6 月 3 日
- **OS 支援：** Windows Server 2016 Technical Preview、 Windows Server 2012 R2 中，Windows Server 2012、 Windows Server 2008 R2 SP1
- **WMF 支援：** WMF 5.0 RTM、 WMF 4.0 更新 WMF 4.0
- **環境：** Azure、 Azure 中國、 Azure Government
- **備註：** 此版本會使用 Windows Server 2016 Technical Preview 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。
- **新功能：**
  - DSC 延伸模組現已於 Azure 中國上架。 此版本主要包含在 Azure 中國上執行延伸模組的修正。

### <a name="version-218"></a>2.18 版

- **發行日期：** 2016 年 6 月 3 日
- **OS 支援：** Windows Server 2016 Technical Preview、 Windows Server 2012 R2 中，Windows Server 2012、 Windows Server 2008 R2 SP1
- **WMF 支援：** WMF 5.0 RTM、 WMF 4.0 更新 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 Technical Preview 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。
- **新功能：**
  - 在下載遙測 Hotfix (已知的 Azure DNS 問題) 或安裝期間，使遙測在發生錯誤時不進行封鎖。
  - 修正重新開機後，延伸模組停止處理設定的間歇性問題。 這項問題原先會導致 DSC 延伸模組停留在 [轉換中] 狀態。
  - 同時新增其他小幅度修正與改善項目。

### <a name="version-217"></a>2.17 版

- **發行日期：** 2016 年 4 月 26日日
- **OS 支援：** Windows Server 2016 Technical Preview、 Windows Server 2012 R2 中，Windows Server 2012、 Windows Server 2008 R2 SP1
- **WMF 支援：** WMF 5.0 RTM、 WMF 4.0 更新 WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 Technical Preview 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。
- **新功能：**
  - WMF 4.0 Update 的支援。 如需 WMF 4.0 Update 的詳細資訊，請參照[此部落格](https://blogs.msdn.microsoft.com/powershell/2016/01/19/windows-management-framework-wmf-4-0-update-now-available-for-windows-server-2012-windows-server-2008-r2-sp1-and-windows-7-sp1/)。
  - 對在安裝 DSC 延伸模組期間，或在安裝延伸模組後套用 DSC 設定時發生的錯誤重試邏輯。 在本次變更中，若先前的安裝失敗或再次制定先前失敗的 DSC 設定，此延伸模組將會重試安裝最多三次，直到達到完成狀態 (成功/錯誤) 或收到新的要求。 若延伸模組的失敗原因是使用者設定/使用者輸入無效，則不會重試。 在此情況下，您必須以新要求叫用延伸模組並修正使用者設定。 注意：DSC 延伸模組是相依於 Azure VM 代理程式的重試。 Azure VM 代理程式會以上一次失敗的要求叫用延伸模組，直到其達到成功或錯誤狀態。

### <a name="version-216"></a>2.16 版

- **發行日期：** 2016 年 4 月 21日日
- **OS 支援：** Windows Server 2016 Technical Preview、 Windows Server 2012 R2 中，Windows Server 2012、 Windows Server 2008 R2 SP1
- **WMF 支援：** WMF 5.0 RTM、WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 Technical Preview 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。
- **新功能：**
  - 對錯誤處理的改善與其他小幅度 Bug 修正項目。
  - 在 DSC 延伸模組設定中新增屬性。 在 AdvancedOptions 中新增 ‘ForcePullAndApply’，讓 DSC 延伸模組在重新整理模式為 [提取] 時制定 DSC 設定 (與預設的 [推送] 模式相反)。 如需詳細資訊，請參照[此部落格](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/)以取得 DSC 延伸模組設定的詳細資訊。

### <a name="version-215"></a>2.15 版

- **發行日期：** 2016 年 3 月 14日日
- **OS 支援：** Windows Server 2016 Technical Preview、 Windows Server 2012 R2 中，Windows Server 2012、 Windows Server 2008 R2 SP1
- **WMF 支援：** WMF 5.0 RTM、WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 Technical Preview 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。
- **新功能：**
  - 2.14 版的延伸模組包含了安裝 WMF RTM 的變更。 當您將延伸模組版本從 2.13.2.0 升級到 2.14.0.0 時，可能會注意到部分 DSC cmdlet 失敗，或是您的設定失敗，並顯示錯誤：「找不到任何具有指定屬性值的執行個體」。 如需詳細資訊，請參閱 [DSC 版本資訊](https://msdn.microsoft.com/en-us/powershell/wmf/limitation_dsc)。 2.15 版中新增了這些問題的因應措施。
  - 很抱歉，若您已經安裝了 2.14 版且遇到上述兩項問題之一，就必須手動執行這些步驟。  在提升權限的 PowerShell 工作階段：
    - `Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof`
    - `mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof`

### <a name="version-214"></a>2.14 版

- **發行日期：** 2016 年 2 月 25日日
- **OS 支援：** Windows Server 2016 Technical Preview、 Windows Server 2012 R2 中，Windows Server 2012、 Windows Server 2008 R2 SP1
- **WMF 支援：** WMF 5.0 RTM、WMF 4.0
- **環境：** Azure
- **備註：** 此版本會使用 Windows Server 2016 Technical Preview 內附的 DSC；針對其他 Windows OS，則會安裝 [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (安裝 WMF 需要重新開機)。
- **新功能：**
  - 使用 WMF RTM。
  - 啟用資料收集以改善 DSC 延伸模組的品質。 如需詳細資訊，請參照[部落格](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/)。
  - 以資源管理員範本提供延伸模組的更新設定格式。 如需詳細資訊，請參照[部落格](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/)。
  - Bug 修正與其他改善項目。

## <a name="next-steps"></a>接下來的步驟

- 如需有關 PowerShell DSC 的詳細資訊，請前往 [PowerShell 文件中心](../overview/overview.md)。
- 檢查 [DSC 延伸模組的資源管理員範本](/azure/virtual-machines/extensions/dsc-template)。
- 若要取得您可使用 PowerShell DSC 進行管理的功能以及更多 DSC 資源，請瀏覽 [PowerShell 資源庫](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0)。
- 如需將敏感性參數傳遞至設定的詳細資料，請參閱[利用 DSC 延伸模組處理常式安全地管理認證](/azure/virtual-machines/extensions/dsc-credentials)。