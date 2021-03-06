---
title: 在 Windows 上安裝 PowerShell Core
description: 在 Windows 上安裝 PowerShell Core 的相關資訊
ms.date: 08/06/2018
ms.openlocfilehash: 910ee5a653fc1703bfddaf6367225f3b654d600f
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293005"
---
# <a name="installing-powershell-core-on-windows"></a>在 Windows 上安裝 PowerShell Core

有多種方法可以在 Windows 中安裝 PowerShell Core。

## <a name="prerequisites"></a>必要條件

若要透過 WSMan 啟用 PowerShell 遠端執行功能，必須符合下列必要條件：

- 在 Windows 10 以下的 Windows 版本中安裝[通用 C 執行階段](https://www.microsoft.com/download/details.aspx?id=50410)。 透過直接下載或 Windows Update 即可取得。 完整修補 (包括選擇性的套件) 的受支援系統已安裝此項目。
- 在 Windows 7 和 Windows Server 2008 R2 上安裝 Windows Management Framework (WMF) 4.0 或更新版本。

## <a name="a-idmsi-installing-the-msi-package"></a><a id="msi" />安裝 MSI 套件

若要在 Windows 用戶端或 Windows Server 上安裝 PowerShell (適用於 Windows 7 SP1、Server 2008 R2 和更新版本)，請從我們的 GitHub [版本][]頁面下載 MSI 套件。 向下捲動至想安裝版本的 [資產] 區段。 [資產] 區段可能會摺疊，因此您可能需要按一下以展開它。

MSI 檔案看起來像這樣 - `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well -->

下載後，按兩下安裝程式，並依提示操作。

安裝程式會在 Windows [開始] 功能表中建立捷徑。

- 套件預設安裝在 `$env:ProgramFiles\PowerShell\<version>`
- 您可以透過 [開始] 功能表或下列命令啟動 PowerShell： `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`

### <a name="administrative-install-from-the-command-line"></a>從命令列進行系統管理安裝

可以從命令列安裝 MSI 套件。 這允許系統管理員無需使用者互動即可部署套件。 適用於 PowerShell 的 MSI 套件包含下列屬性以控制安裝選項：

- **ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL** - 此屬性控制將 [開啟 PowerShell] 項目新增至 Windows 檔案總管中的內容功能表的選項。
- **ENABLE_PSREMOTING** - 此屬性控制在安裝期間啟用 PowerShell 遠端執行功能的選項。
- **REGISTER_MANIFEST** - 此屬性控制用於註冊 Windows 事件記錄資訊清單的選項。

下列範例示範如何在啟用所有安裝選項的情況下，以無訊息方式安裝 PowerShell Core。

```powershell
msiexec.exe /package PowerShell-<version>-win-<os-arch>.msi /quiet ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL=1 ENABLE_PSREMOTING=1 REGISTER_MANIFEST=1
```

如需 Msiexec.exe 的命令列選項完整清單，請參閱[命令列選項](/windows/desktop/Msi/command-line-options)。

## <a name="a-idzip-installing-the-zip-package"></a><a id="zip" />安裝 ZIP 套件

我們提供 PowerShell 二進位 ZIP 封存以啟用進階部署案例。 請注意，當使用 ZIP 封存時，不會像 MSI 套件一樣檢查必要條件。 要使遠端執行功能透過 WSMan 正常運作，請確定您已符合[必要條件](#prerequisites)。

## <a name="deploying-on-windows-iot"></a>在 Windows IoT 上部署

Windows IoT 附帶提供 Windows PowerShell， 我們就是用它來部署 PowerShell Core 6。

1. 針對目標裝置建立 `PSSession`

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. 將 ZIP 套件複製到裝置

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-<version>-win-<os-arch>.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. 連接到裝置並展開封存

   ```powershell
   Enter-PSSession $s
   Set-Location u:\users\administrator\downloads
   Expand-Archive .\PowerShell-<version>-win-<os-arch>.zip
   ```

4. 設定 PowerShell Core 6 的遠端處理

   ```powershell
   Set-Location .\PowerShell-<version>-win-<os-arch>
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. 連接到裝置上的 PowerShell 核心 6 端點

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.<version>
   ```

## <a name="deploying-on-nano-server"></a>在 Nano Server 上部署

這些指示假設某個 PowerShell 版本已在 Nano Server 映像中執行，而且此映像是由 [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server) 產生。
Nano Server 是一種「無周邊」作業系統。 目前有兩種方法可以部署核心二進位檔。

1. 離線 - 掛接 Nano Server VHD，並將 ZIP 檔案內容解壓縮至您在掛接映像中選擇的位置。
2. 線上 - 透過 PowerShell 工作階段傳輸 ZIP 檔案，並將它解壓縮至您選擇的位置。

這兩種情況都需要 Windows 10 x64 ZIP 版套件，還需要在「系統管理員」PowerShell 執行個體中執行命令。

### <a name="offline-deployment-of-powershell-core"></a>PowerShell Core 的離線部署

1. 使用您最愛的 ZIP 公用程式將套件解壓縮至已掛接 Nano Server 映像的目錄。
2. 取消掛接映像和開機映像。
3. 連線到 Windows PowerShell 的收件匣執行個體。
4. 請遵循下列指示來建立使用[另一個執行個體技術](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register)的遠端端點。

### <a name="online-deployment-of-powershell-core"></a>PowerShell Core 的線上部署

下列步驟會引導您從部署 PowerShell Core 到執行 Nano Server 執行個體及其遠端端點的設定。

- 連線到 Windows PowerShell 的收件匣執行個體

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- 將檔案複製到 Nano Server 執行個體

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- 輸入工作階段

  ```powershell
  Enter-PSSession $session
  ```

- 壓縮檔 ZIP 檔案

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- 如需 WSMan 型的遠端功能，請遵循下列指示來建立使用[另一個執行個體技術](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register)的遠端端點。

## <a name="how-to-create-a-remoting-endpoint"></a>如何建立遠端端點

PowerShell Core 支援 WSMan 和 SSH 上的 PowerShell 遠端通訊協定 (PSRP)。 如需詳細資訊，請參閱：

- [PowerShell Core 中的 SSH 遠端][ssh-remoting]
- [PowerShell Core 中的 WSMan 遠端處理][wsman-remoting]

<!-- [download-center]: TODO -->
[releases]: https://github.com/PowerShell/PowerShell/releases [ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md [wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md [AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
