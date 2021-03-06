---
ms.date: 06/12/2017
keywords: wmf,powershell,設定
ms.openlocfilehash: 9ca12ad3f0729a2e9595d7ca5ccf9041e47658a3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218088"
---
# <a name="archive-cmdlets"></a>封存 Cmdlet

兩個新的 Cmdlet，**Compress-Archive** 和 **Expand-Archive**，讓您可以壓縮和解壓縮 ZIP 檔案。

## <a name="compress-archive"></a>Compress-Archive
**Compress-Archive** Cmdlet 會從指定的檔案中建立新的封存檔案。 封存檔案可讓多個檔案進行封裝，並可選擇性地壓縮成單一檔案，以方便處理和儲存。 封存檔案可以用 **-CompressionLevel** 參數中指定的壓縮演算法壓縮。
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a>Expand-Archive
**Expand-Archive** Cmdlet 會從指定的封存檔案中解壓縮檔案。 封存檔案可讓多個檔案進行封裝，並可選擇性地壓縮成單一檔案，以方便處理和儲存。
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
