---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: PowerShellTabCollection 物件
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2018
ms.locfileid: "53400956"
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="3bbbe-103">PowerShellTabCollection 物件</span><span class="sxs-lookup"><span data-stu-id="3bbbe-103">The PowerShellTabCollection Object</span></span>

<span data-ttu-id="3bbbe-104">**PowerShellTab** 集合物件是 **PowerShellTab** 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="3bbbe-105">每個 **PowerShellTab** 物件功能都可做為個別的執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="3bbbe-106">它是 Microsoft.PowerShell.Host.ISE.PowerShellTabs 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="3bbbe-107">範例是 **$psISE.PowerShellTabs** 物件。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="3bbbe-108">Methods</span><span class="sxs-lookup"><span data-stu-id="3bbbe-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="3bbbe-109">Add\(\)</span><span class="sxs-lookup"><span data-stu-id="3bbbe-109">Add\(\)</span></span>

<span data-ttu-id="3bbbe-110">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bbbe-111">將新的 PowerShell 索引標籤新增到集合。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="3bbbe-112">它會傳回新加入的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-112">It returns the newly added tab.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="3bbbe-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="3bbbe-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="3bbbe-114">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bbbe-115">移除 **psTab** 參數指定的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

<span data-ttu-id="3bbbe-116">**psTab** 要移除的 PowerShell 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-116">**psTab** The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="3bbbe-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="3bbbe-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="3bbbe-118">在 Windows PowerShell ISE 2.0 與更新的版本中支援。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bbbe-119">選取 **psTab** 參數指定的 PowerShell 索引標籤，使其成為目前作用中的 PowerShell 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

<span data-ttu-id="3bbbe-120">**psTab** 要選取的 PowerShell 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3bbbe-120">**psTab** The PowerShell tab to select.</span></span>

```powershell
# Save the current tab in a variable and rename it
$oldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName = 'Old Tab'
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab = $oldTab
```

## <a name="see-also"></a><span data-ttu-id="3bbbe-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3bbbe-121">See Also</span></span>

- [<span data-ttu-id="3bbbe-122">PowerShellTab 物件</span><span class="sxs-lookup"><span data-stu-id="3bbbe-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="3bbbe-123">Windows PowerShell ISE 指令碼物件模型的用途</span><span class="sxs-lookup"><span data-stu-id="3bbbe-123">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="3bbbe-124">ISE 物件模型階層</span><span class="sxs-lookup"><span data-stu-id="3bbbe-124">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)