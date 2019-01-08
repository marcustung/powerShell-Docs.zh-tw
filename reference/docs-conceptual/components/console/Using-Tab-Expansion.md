---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: 使用 Tab 鍵擴充
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 3d047bf0691c8a304d7637aa50fba6ae99709a82
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2018
ms.locfileid: "53402092"
---
# <a name="using-tab-expansion"></a><span data-ttu-id="3669a-103">使用 Tab 鍵擴充</span><span class="sxs-lookup"><span data-stu-id="3669a-103">Using Tab Expansion</span></span>

<span data-ttu-id="3669a-104">命令列殼層通常會提供方法，透過加速命令輸入以及提供，來自動完成長檔案或命令的名稱。</span><span class="sxs-lookup"><span data-stu-id="3669a-104">Command-line shells often provide a way to complete the names of long files or commands automatically, speeding up command entry and providing .</span></span> <span data-ttu-id="3669a-105">Windows PowerShell 可讓您按 **Tab** 鍵來填入檔案名稱和 Cmdlet 名稱。</span><span class="sxs-lookup"><span data-stu-id="3669a-105">Windows PowerShell allows you to fill in file names and cmdlet names by pressing the **Tab** key.</span></span>

> [!NOTE]
> <span data-ttu-id="3669a-106">Tab 鍵擴充由內部函式 TabExpansion 或 TabExpansion2 所控制。</span><span class="sxs-lookup"><span data-stu-id="3669a-106">Tab expansion is controlled by the internal function TabExpansion or TabExpansion2.</span></span> <span data-ttu-id="3669a-107">因為可以修改或覆寫這個函式，所以這項討論只是預設 PowerShell 設定行為的指南。</span><span class="sxs-lookup"><span data-stu-id="3669a-107">Since this function can be modified or overridden, this discussion is a guide to the behavior of the default PowerShell configuration.</span></span>

<span data-ttu-id="3669a-108">若要自動從可用的選項中填入檔案名稱或路徑，請輸入部分名稱，然後按 **Tab** 鍵。</span><span class="sxs-lookup"><span data-stu-id="3669a-108">To fill in a filename or path from the available choices automatically, type part of the name and press the **Tab** key.</span></span> <span data-ttu-id="3669a-109">PowerShell 會自動將名稱擴充到找到的第一個相符項目。</span><span class="sxs-lookup"><span data-stu-id="3669a-109">PowerShell will automatically expand the name to the first match that it finds.</span></span> <span data-ttu-id="3669a-110">重複按 **Tab** 鍵，會循環顯示所有可用選項。</span><span class="sxs-lookup"><span data-stu-id="3669a-110">Pressing the **Tab** key repeatedly will cycle through all of the available choices.</span></span>

<span data-ttu-id="3669a-111">Cmdlet 名稱的 Tab 鍵擴充略有不同。</span><span class="sxs-lookup"><span data-stu-id="3669a-111">The tab expansion of cmdlet names is slightly different.</span></span> <span data-ttu-id="3669a-112">若要對 Cmdlet 名稱使用 Tab 鍵擴充，請輸入名稱的完整第一個部分 (動詞) 和後面的連字號。</span><span class="sxs-lookup"><span data-stu-id="3669a-112">To use tab expansion on a cmdlet name, type the entire first part of the name (the verb) and the hyphen that follows it.</span></span> <span data-ttu-id="3669a-113">您可以填入名稱的更多部分來進行局部比對。</span><span class="sxs-lookup"><span data-stu-id="3669a-113">You can fill in more of the name for a partial match.</span></span> <span data-ttu-id="3669a-114">例如，如果您鍵入 **get-co**，然後按 **Tab** 鍵，則 PowerShell 會自動將此項目擴充到 **Get-Command** Cmdlet (請注意，這也會將字母的大小寫變更為其標準形式)。</span><span class="sxs-lookup"><span data-stu-id="3669a-114">For example, if you type **get-co** and then press the **Tab** key, PowerShell will automatically expand this to the **Get-Command** cmdlet (notice that it also changes the case of letters to their standard form).</span></span> <span data-ttu-id="3669a-115">如果您再次按下 **Tab** 鍵，PowerShell 會以僅有的其他相符 Cmdlet 名稱 (**Get-Content**) 取代此項目。</span><span class="sxs-lookup"><span data-stu-id="3669a-115">If you press **Tab** key again, PowerShell replaces this with the only other matching cmdlet name, **Get-Content**.</span></span>

<span data-ttu-id="3669a-116">您可以對同一行重複使用 Tab 鍵擴充。</span><span class="sxs-lookup"><span data-stu-id="3669a-116">You can use tab expansion repeatedly on the same line.</span></span> <span data-ttu-id="3669a-117">例如，您可以對 **Get-Content** Cmdlet 的名稱使用 Tab 鍵擴充，方法是輸入：</span><span class="sxs-lookup"><span data-stu-id="3669a-117">For example, you can use tab expansion on the name of the **Get-Content** cmdlet by entering:</span></span>

```
PS> Get-Con<Tab>
```

<span data-ttu-id="3669a-118">按 **Tab** 鍵時，命令會擴充到︰</span><span class="sxs-lookup"><span data-stu-id="3669a-118">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content
```

<span data-ttu-id="3669a-119">您接著可以局部指定 Active Setup 記錄檔的路徑，並再次使用 Tab 鍵擴充︰</span><span class="sxs-lookup"><span data-stu-id="3669a-119">You can then partially specify the path to the Active Setup log file and use tab expansion again:</span></span>

```
PS> Get-Content c:\windows\acts<Tab>
```

<span data-ttu-id="3669a-120">按 **Tab** 鍵時，命令會擴充到︰</span><span class="sxs-lookup"><span data-stu-id="3669a-120">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> <span data-ttu-id="3669a-121">Tab 鍵擴充處理程序的一個限制是一律會將 Tab 鍵解譯為嘗試完成文字。</span><span class="sxs-lookup"><span data-stu-id="3669a-121">One limitation of the tab expansion process is that tabs are always interpreted as attempts to complete a word.</span></span> <span data-ttu-id="3669a-122">若您將命令範例複製並貼上 PowerShell 主控台，請確認未在該範例使用 Tab 鍵，如果有的話將無法預測結果，而且幾乎可以肯定不是您所預期的結果。</span><span class="sxs-lookup"><span data-stu-id="3669a-122">If you copy and paste command examples into a PowerShell console, make sure that the sample does not contain tabs; if it does, the results will be unpredictable and will almost certainly not be what you intended.</span></span>