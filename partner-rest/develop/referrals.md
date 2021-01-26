---
title: Programová správa zájemců a příležitostí společného prodeje v partnerském centru
description: V této části se dozvíte, jak můžou partneři používat rozhraní API partnerů k programové správě potenciálních zákazníků a příležitostí společného prodeje.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0da725c9b2459a6c5631b7cc7e21b46e9a7191b8
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770358"
---
# <a name="programmatically-manage-leads-and-co-sell-opportunities-in-partner-center"></a><span data-ttu-id="f910a-103">Programová správa zájemců a příležitostí společného prodeje v partnerském centru</span><span class="sxs-lookup"><span data-stu-id="f910a-103">Programmatically manage leads and co-sell opportunities in Partner Center</span></span>

<span data-ttu-id="f910a-104">Tento článek vám pomůže pochopit, jak programově spravovat zájemce, které obdržíte na stránce poskytovatele řešení Microsoftu, a příležitosti společného prodeje, které obdržíte od prodejního zástupce Microsoftu nebo jiných partnerů.</span><span class="sxs-lookup"><span data-stu-id="f910a-104">This article will help you understand how you can programmatically manage the leads that you receive from Microsoft solution provider page and the co-sell opportunities that you receive from Microsoft sales representative or other partners.</span></span> <span data-ttu-id="f910a-105">Pomocí těchto rozhraní API můžete také programově sdílet obchodní kanál vaší společnosti nebo pozvat prodejní zástupce Microsoftu, aby mohli spolupracovat na potenciálních příležitostech.</span><span class="sxs-lookup"><span data-stu-id="f910a-105">You can also use these api's to programmatically share your company's sales pipeline or invite Microsoft sales representatives to collaborate on potential opportunities.</span></span> 

## <a name="manage-leads-and-opportunities"></a><span data-ttu-id="f910a-106">Správa zájemců a příležitostí</span><span class="sxs-lookup"><span data-stu-id="f910a-106">Manage leads and opportunities</span></span>

- <span data-ttu-id="f910a-107">[Získání seznamu zájemců a příležitostí](get-a-list-of-referrals.md) – načte seznam zájemců ze strany Microsoftu pro poskytovatele řešení a příležitosti pro společný prodej od prodejců Microsoftu nebo jiných partnerů.</span><span class="sxs-lookup"><span data-stu-id="f910a-107">[Get the list of leads and opportunities](get-a-list-of-referrals.md) - Gets the list of leads from Microsoft solution provider page and co-sell opportunities from Microsoft sellers or other partners.</span></span> <span data-ttu-id="f910a-108">Bude obsahovat také seznam příležitostí vytvořených vaší organizací.</span><span class="sxs-lookup"><span data-stu-id="f910a-108">This will also contain the list of opportunities created by your organization.</span></span>
- <span data-ttu-id="f910a-109">[Získat zájemce nebo příležitost podle ID](get-a-referral-by-Id.md) – získá zájemce nebo příležitost podle ID.</span><span class="sxs-lookup"><span data-stu-id="f910a-109">[Get a lead or opportunity by Id](get-a-referral-by-Id.md) - Gets a lead or opportunity by Id.</span></span>
- <span data-ttu-id="f910a-110">[Aktualizace zájemce nebo příležitosti](patch-a-referral.md) – umožňuje aktualizovat podrobnosti o zájemci nebo příležitostech, jako je například hodnota kouposti, odhadované datum uzavření nebo spravovat fáze prodeje mimo jiné podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="f910a-110">[Update a lead or opportunity](patch-a-referral.md) - Allows you to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>
- <span data-ttu-id="f910a-111">[Vytvoření nové příležitosti](create-a-referral.md) – umožňuje vytvořit novou příležitost a soukromou práci na společném prodeji.</span><span class="sxs-lookup"><span data-stu-id="f910a-111">[Create a new opportunity](create-a-referral.md) - Enables you to create a new co-sell opportunity or private deal.</span></span>
- [<span data-ttu-id="f910a-112">Zdroje informací o referenčních seznamech</span><span class="sxs-lookup"><span data-stu-id="f910a-112">Referral resources</span></span>](referral-resources.md)

> [!Note]
> <span data-ttu-id="f910a-113">Potenciální zákazníky přijaté z komerčního tržiště Microsoftu (Azure Marketplace a AppSource) se nedají spravovat pomocí rozhraní API partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="f910a-113">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) cannot be managed using Partner Center api's.</span></span>