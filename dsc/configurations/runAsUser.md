---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: 搭配使用認證與 DSC 資源
ms.openlocfilehash: af54c286ce744cd7db0b0e2d05087f60cdf1a33c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2018
ms.locfileid: "53400831"
---
# <a name="use-credentials-with-dsc-resources"></a><span data-ttu-id="abe40-103">搭配使用認證與 DSC 資源</span><span class="sxs-lookup"><span data-stu-id="abe40-103">Use Credentials with DSC Resources</span></span>

> <span data-ttu-id="abe40-104">適用於：Windows PowerShell 5.0 中，Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="abe40-104">Applies To: Windows PowerShell 5.0, Windows PowerShell 5.1</span></span>

<span data-ttu-id="abe40-105">您可以在設定中使用自動 **PsDscRunAsCredential** 屬性，以一組指定的認證來執行 DSC 資源。</span><span class="sxs-lookup"><span data-stu-id="abe40-105">You can run a DSC resource under a specified set of credentials by using the automatic **PsDscRunAsCredential** property in the configuration.</span></span>
<span data-ttu-id="abe40-106">DSC 預設會使用系統帳戶執行每項資源，</span><span class="sxs-lookup"><span data-stu-id="abe40-106">By default, DSC runs each resource as the system account.</span></span>
<span data-ttu-id="abe40-107">但有些時候仍須以使用者身分執行，例如在特定使用者內容中安裝 MSI 封裝；設定使用者的登錄機碼；存取使用者的特定本機目錄；或存取網路共用等等。</span><span class="sxs-lookup"><span data-stu-id="abe40-107">There are times when running as a user is necessary, such as installing MSI packages in a specific user context, setting a user's registry keys, accessing a user's specific local directory, or accessing a network share.</span></span>

<span data-ttu-id="abe40-108">每項 DSC 資源都有 **PsDscRunAsCredential** 屬性可設為任何使用者的認證 ([PSCredential](/dotnet/api/system.management.automation.pscredential) 物件)。</span><span class="sxs-lookup"><span data-stu-id="abe40-108">Every DSC resource has a **PsDscRunAsCredential** property that can be set to any user credentials (a [PSCredential](/dotnet/api/system.management.automation.pscredential) object).</span></span>
<span data-ttu-id="abe40-109">此認證可硬式編碼成設定中的屬性值，也可將此值設為 [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential)，如此將會在編譯設定時提示使用者輸入認證 (如需編譯設定的相關資訊，請參閱[設定](configurations.md)。</span><span class="sxs-lookup"><span data-stu-id="abe40-109">The credential can be hard-coded as the value of the property in the configuration, or you can set the value to [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential), which will prompt the user for a credential when the configuration is compiled (for information about compiling configurations, see [Configurations](configurations.md).</span></span>

> [!NOTE]
> <span data-ttu-id="abe40-110">在 PowerShell 5.0 中，不支援在呼叫複合資源的設定中使用 **PsDscRunAsCredential** 屬性。</span><span class="sxs-lookup"><span data-stu-id="abe40-110">In PowerShell 5.0, using the **PsDscRunAsCredential** property in configurations calling composite resources was not supported.</span></span>
> <span data-ttu-id="abe40-111">在 PowerShell 5.1 中，支援在呼叫複合資源的設定中使用 **PsDscRunAsCredential** 屬性。</span><span class="sxs-lookup"><span data-stu-id="abe40-111">In PowerShell 5.1, the **PsDscRunAsCredential** property is supported in configurations calling composite resources.</span></span>
> <span data-ttu-id="abe40-112">PowerShell 4.0 中無法使用 **PsDscRunAsCredential** 屬性。</span><span class="sxs-lookup"><span data-stu-id="abe40-112">The **PsDscRunAsCredential** property is not available in PowerShell 4.0.</span></span>

<span data-ttu-id="abe40-113">下列範例使用了 `Get-Credential` 提示使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="abe40-113">In the following example, `Get-Credential` is used to prompt the user for credentials.</span></span>
<span data-ttu-id="abe40-114">**Registry** 資源可用於變更指定Windows 命令提示字元視窗背景色彩的登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="abe40-114">The **Registry** resource is used to change the registry key that specifies the background color for the Windows command prompt window.</span></span>

```powershell
Configuration ChangeCmdBackGroundColor
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

ChangeCmdBackGroundColor -ConfigurationData $configData
```

> [!NOTE]
> <span data-ttu-id="abe40-115">此範例假設您的 `C:\publicKeys\targetNode.cer` 中包含有效的憑證，且該憑證的指紋為所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="abe40-115">This example assumes that you have a valid certificate at `C:\publicKeys\targetNode.cer`, and that the thumbprint of that certificate is the value shown.</span></span>
> <span data-ttu-id="abe40-116">如需如何在 DSC 設定 MOF 檔案中加密認證的資訊，請參閱[保護 MOF 檔案](../pull-server/secureMOF.md)。</span><span class="sxs-lookup"><span data-stu-id="abe40-116">For information about encrypting credentials in DSC configuration MOF files, see [Securing the MOF file](../pull-server/secureMOF.md).</span></span>