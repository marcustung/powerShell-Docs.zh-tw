---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: DSC WindowsFeature 資源
ms.openlocfilehash: 7a57f4b2797ab3bb202aea8b2543d1e3f14074e9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047348"
---
# <a name="dsc-windowsfeature-resource"></a><span data-ttu-id="582e5-103">DSC WindowsFeature 資源</span><span class="sxs-lookup"><span data-stu-id="582e5-103">DSC WindowsFeature Resource</span></span>

> <span data-ttu-id="582e5-104">適用於：Windows PowerShell 4.0 中，Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="582e5-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="582e5-105">Windows PowerShell 預期狀態設定 (DSC) 的 **WindowsFeature** 資源提供一個機制，確保可在目標節點上新增或移除角色和功能。</span><span class="sxs-lookup"><span data-stu-id="582e5-105">The **WindowsFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="582e5-106">語法</span><span class="sxs-lookup"><span data-stu-id="582e5-106">Syntax</span></span>

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="582e5-107">Properties</span><span class="sxs-lookup"><span data-stu-id="582e5-107">Properties</span></span>

|  <span data-ttu-id="582e5-108">屬性</span><span class="sxs-lookup"><span data-stu-id="582e5-108">Property</span></span>  |  <span data-ttu-id="582e5-109">描述</span><span class="sxs-lookup"><span data-stu-id="582e5-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="582e5-110">名稱</span><span class="sxs-lookup"><span data-stu-id="582e5-110">Name</span></span>| <span data-ttu-id="582e5-111">表示您想要確保新增或移除的角色或功能名稱。</span><span class="sxs-lookup"><span data-stu-id="582e5-111">Indicates the name of the role or feature that you want to ensure is added or removed.</span></span> <span data-ttu-id="582e5-112">這與來自 [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) Cmdlet 的 __Name__ 屬性相同，不是角色或功能的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="582e5-112">This is the same as the __Name__ property from the [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) cmdlet, and not the display name of the role or feature.</span></span>|
| <span data-ttu-id="582e5-113">認證</span><span class="sxs-lookup"><span data-stu-id="582e5-113">Credential</span></span>| <span data-ttu-id="582e5-114">表示要用以新增或移除角色或功能的認證。</span><span class="sxs-lookup"><span data-stu-id="582e5-114">Indicates the credentials to use to add or remove the role or feature.</span></span>|
| <span data-ttu-id="582e5-115">Ensure</span><span class="sxs-lookup"><span data-stu-id="582e5-115">Ensure</span></span>| <span data-ttu-id="582e5-116">表示角色或功能是否新增。</span><span class="sxs-lookup"><span data-stu-id="582e5-116">Indicates if the role or feature is added.</span></span> <span data-ttu-id="582e5-117">若要確保新增角色或功能，這個屬性請設為 "Present"。若要確保移除角色或功能，請將屬性設定為 "Absent"。</span><span class="sxs-lookup"><span data-stu-id="582e5-117">To ensure that the role or feature is added, set this property to "Present" To ensure that the role or feature is removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="582e5-118">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="582e5-118">IncludeAllSubFeature</span></span>| <span data-ttu-id="582e5-119">這個屬性設為 __$true__ 可讓您使用以 __Name__ 屬性指定的功能狀態來確保所有必要子功能的狀態。</span><span class="sxs-lookup"><span data-stu-id="582e5-119">Set this property to __$true__ to ensure the state of all required subfeatures with the state of the feature you specify with the __Name__ property.</span></span>|
| <span data-ttu-id="582e5-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="582e5-120">LogPath</span></span>| <span data-ttu-id="582e5-121">表示要讓資源提供者記錄作業的記錄檔路徑。</span><span class="sxs-lookup"><span data-stu-id="582e5-121">Indicates the path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="582e5-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="582e5-122">DependsOn</span></span>| <span data-ttu-id="582e5-123">表示必須先執行另一個資源的設定，再設定這個資源。</span><span class="sxs-lookup"><span data-stu-id="582e5-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="582e5-124">例如，如果第一個想要執行的資源設定指令碼區塊的識別碼是 __ResourceName__，而它的類型是 __ResourceType__，則使用這個屬性的語法就是 `DependsOn = "[ResourceType]ResourceName"`。</span><span class="sxs-lookup"><span data-stu-id="582e5-124">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="582e5-125">來源</span><span class="sxs-lookup"><span data-stu-id="582e5-125">Source</span></span>| <span data-ttu-id="582e5-126">如有必要，表示用於安裝的來源檔案位置。</span><span class="sxs-lookup"><span data-stu-id="582e5-126">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="582e5-127">範例</span><span class="sxs-lookup"><span data-stu-id="582e5-127">Example</span></span>
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present"
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature
}
```