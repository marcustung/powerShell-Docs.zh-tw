---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: 適合決策者的預期狀態設定概觀
ms.openlocfilehash: ce554d4bb994d4b1816d9d9c24599e4ef0e1c593
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2018
ms.locfileid: "53400688"
---
# <a name="desired-state-configuration-overview-for-decision-makers"></a>適合決策者的預期狀態設定概觀

本文件說明使用 Windows PowerShell Desired State Configuration (DSC) 的商務優勢。 這不是技術指南。

## <a name="what-is-desired-state-configuration"></a>什麼是預期狀態設定？

PowerShell Desired State Configuration 是 Windows 內建的開放式標準設定管理平台。 DSC 的彈性足以因應部署生命週期 (開發、測試、生產階段前，生產環境) 各階段穩定且一致的運作，向外延展時亦然。

DSC 的中心概念是[設定](../configurations/configurations.md)。
設定是容易讀取的文件，描述由特定特性的電腦 (「節點」) 組成的環境。
這些特性可以簡單到像是確保已啟用特定的 Windows 功能，也可以複雜到像是部署 SharePoint。

DSC 也有內建的監視和報告。
如果系統不再相容，DSC 會引發警示，採取動作更正系統。

## <a name="benefits-of-using-desired-state-configuration"></a>使用預期狀態設定的優勢

設定應設計為易於讀取、儲存及更新。
設定會宣告目標裝置應有的狀態，不需要撰寫如何成就裝置狀態的指示。
這可讓您以更經濟的成本透過 DSC 了解、採用、實作和維護設定。

建立設定即表示，已在單一位置將複雜的部署步驟擷取為「單一事實來源」。
這讓特定電腦集合的重複部署更不容易出錯。
也因此可讓部署更快速且更可靠，藉此縮短複雜部署的完成時間。

設定也可透過 [PowerShell 資源庫](https://powershellgallery.com)來分享，亦即對於要完成的工作，可能已經有共通案例與最佳做法。


## <a name="desired-state-configuration-and-devops"></a>預期狀態設定和 DevOps

DSC 的設計過程納入了 [DevOps](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx) 考量，是人員、流程和工具的組合，可允許快速建置與反覆開發週期，為內部或外部的終端使用者創造價值。
讓單一設定定義環境即表示，開發人員可以將需求編碼成設定、將該設定簽入原始檔控制，而維運小組可以輕鬆部署程式碼，不必進行可能會出錯的手動程序。

設定也[以資料為動力](../configurations/configData.md)，讓維運小組更容易識別及變更環境，而不必開發人員介入。

## <a name="desired-state-configuration-on-premises-and-off-premises"></a>Desired State Configuration 的內部和外部部署
DSC 可以用來管理內部部署及外部部署的部署。
在內部部署解決方案方面，DSC 有[提取伺服器](../pull-server/pullServer.md)可集中管理電腦，並報告其狀態。
在雲端解決方案方面，只要能夠使用 Windows 的地方都可以使用 DSC。
建置在預期狀態設定之上的 Azure 也有特定供應項目，例如能集中 DSC 報告的 [Azure 自動化](https://azure.microsoft.com/en-us/documentation/services/automation/)。

## <a name="dsc-and-compatibility"></a>DSC 和相容性

DSC 雖是在 Windows Server 2012 R2 引進，卻是透過 Windows Management Framework (WMF) 套件供低階的作業系統使用。
WMF 詳細資訊請參閱 [PowerShell 首頁](/powershell/)。

DSC 也可用來管理 Linux。 如需詳細資訊，請參閱[開始使用 DSC for Linux](../getting-started/lnxGettingStarted.md)。
