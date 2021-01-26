---
title: Aktualizace zájemce nebo příležitosti (zastaralé)
description: Umožňuje aktualizovat podrobnosti o zájemci nebo příležitosti. Tato metoda aktualizace potenciálního zákazníka nebo příležitosti je zastaralá a místo toho jsme recommmendi použití OPRAVNého volání.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770361"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a><span data-ttu-id="23209-104">Aktualizace zájemce nebo příležitosti (zastaralé)</span><span class="sxs-lookup"><span data-stu-id="23209-104">Update a lead or opportunity (Obsolete)</span></span>

<span data-ttu-id="23209-105">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="23209-105">Applies to:</span></span>

- <span data-ttu-id="23209-106">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="23209-106">Partner API</span></span>

<span data-ttu-id="23209-107">V tomto tématu se dozvíte, jak aktualizovat podrobnosti o zájemcích nebo příležitostech, jako je například hodnota koupě, odhadované datum uzavření nebo Správa fází prodeje mezi další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="23209-107">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span> 


> [!IMPORTANT]
<span data-ttu-id="23209-108">Tato metoda aktualizace potenciálního zákazníka nebo příležitosti je zastaralá a místo toho jsme recommmendi použití [opravného](patch-a-referral.md) volání.</span><span class="sxs-lookup"><span data-stu-id="23209-108">This method of updating a lead or opportunity is obsolete and we recommmend using the [PATCH](patch-a-referral.md) call instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23209-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="23209-109">Prerequisites</span></span>

- <span data-ttu-id="23209-110">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="23209-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="23209-111">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="23209-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="23209-112">Toto rozhraní API aktuálně podporuje jenom přístup uživatelů v případě, že se partneři musí nacházet v jedné z následujících rolí: globální správce, Správce odkazů nebo uživatel s odkazem.</span><span class="sxs-lookup"><span data-stu-id="23209-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="23209-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="23209-113">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="23209-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="23209-114">Request syntax</span></span>

| <span data-ttu-id="23209-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="23209-115">Method</span></span>  | <span data-ttu-id="23209-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="23209-116">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="23209-117">**PUT**</span><span class="sxs-lookup"><span data-stu-id="23209-117">**PUT**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a><span data-ttu-id="23209-118">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="23209-118">Request headers</span></span>

- <span data-ttu-id="23209-119">Další informace najdete v tématu [záhlaví REST rozhraní API pro partnery](headers.md).</span><span class="sxs-lookup"><span data-stu-id="23209-119">For more information, see [Partner API REST headers](headers.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23209-120">Nezapomeňte nastavit hlavičku **If-Match** .</span><span class="sxs-lookup"><span data-stu-id="23209-120">Be sure to set the **If-Match** header.</span></span>

### <a name="request-body"></a><span data-ttu-id="23209-121">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="23209-121">Request body</span></span>

<span data-ttu-id="23209-122">Tato tabulka popisuje vlastnosti [odkazu](referral-resources.md) v těle žádosti.</span><span class="sxs-lookup"><span data-stu-id="23209-122">This table describes the [Referral](referral-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="23209-123">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="23209-123">Property</span></span>            | <span data-ttu-id="23209-124">Typ</span><span class="sxs-lookup"><span data-stu-id="23209-124">Type</span></span>                                                                 | <span data-ttu-id="23209-125">Description</span><span class="sxs-lookup"><span data-stu-id="23209-125">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="23209-126">Id</span><span class="sxs-lookup"><span data-stu-id="23209-126">Id</span></span>                  | <span data-ttu-id="23209-127">řetězec</span><span class="sxs-lookup"><span data-stu-id="23209-127">string</span></span>                                                               | <span data-ttu-id="23209-128">ID pro tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="23209-128">The ID for this Referral.</span></span>                                                                                            |
| <span data-ttu-id="23209-129">EngagementId</span><span class="sxs-lookup"><span data-stu-id="23209-129">EngagementId</span></span>        | <span data-ttu-id="23209-130">řetězec</span><span class="sxs-lookup"><span data-stu-id="23209-130">string</span></span>                                                               | <span data-ttu-id="23209-131">EngagementID pro tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="23209-131">The EngagementID for this Referral.</span></span> <span data-ttu-id="23209-132">K jednomu EngagementID může být přidruženo několik odkazů.</span><span class="sxs-lookup"><span data-stu-id="23209-132">Multiple referrals can be associated to a single EngagementID</span></span>                    |
| <span data-ttu-id="23209-133">Name</span><span class="sxs-lookup"><span data-stu-id="23209-133">Name</span></span>                | <span data-ttu-id="23209-134">řetězec</span><span class="sxs-lookup"><span data-stu-id="23209-134">string</span></span>                                                               | <span data-ttu-id="23209-135">Název odkazu</span><span class="sxs-lookup"><span data-stu-id="23209-135">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="23209-136">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="23209-136">ExternalReferenceId</span></span> | <span data-ttu-id="23209-137">řetězec</span><span class="sxs-lookup"><span data-stu-id="23209-137">string</span></span>                                                               | <span data-ttu-id="23209-138">Externí identifikátor pro odkaz</span><span class="sxs-lookup"><span data-stu-id="23209-138">An external identifier for the referral.</span></span> <span data-ttu-id="23209-139">Příklad: Uložte si vlastní ID zájemce nebo příležitosti pro Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="23209-139">Example: Store your own Dynamics 365 lead/opportunity ID</span></span>                    |
| <span data-ttu-id="23209-140">CreatedDateTime</span><span class="sxs-lookup"><span data-stu-id="23209-140">CreatedDateTime</span></span>     | <span data-ttu-id="23209-141">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="23209-141">string in UTC date time format</span></span>                                       | <span data-ttu-id="23209-142">Datum vytvoření odkazu</span><span class="sxs-lookup"><span data-stu-id="23209-142">The date the referral was created.</span></span>                                                                                   |
| <span data-ttu-id="23209-143">UpdatedDateTime</span><span class="sxs-lookup"><span data-stu-id="23209-143">UpdatedDateTime</span></span>     | <span data-ttu-id="23209-144">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="23209-144">string in UTC date time format</span></span>                                       | <span data-ttu-id="23209-145">Datum poslední aktualizace odkazu</span><span class="sxs-lookup"><span data-stu-id="23209-145">The date the referral was last updated.</span></span>                                                                              |
| <span data-ttu-id="23209-146">ExpirationDateTime</span><span class="sxs-lookup"><span data-stu-id="23209-146">ExpirationDateTime</span></span>  | <span data-ttu-id="23209-147">řetězec ve formátu data a času UTC</span><span class="sxs-lookup"><span data-stu-id="23209-147">string in UTC date time format</span></span>                                       | <span data-ttu-id="23209-148">Datum, po jehož uplynutí bude platnost odkazu vypršet.</span><span class="sxs-lookup"><span data-stu-id="23209-148">The date the referral will expire.</span></span>                                                                                   |
| <span data-ttu-id="23209-149">Status</span><span class="sxs-lookup"><span data-stu-id="23209-149">Status</span></span>              | [<span data-ttu-id="23209-150">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="23209-150">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="23209-151">[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu.</span><span class="sxs-lookup"><span data-stu-id="23209-151">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="23209-152">SubStatus</span><span class="sxs-lookup"><span data-stu-id="23209-152">Substatus</span></span>           | [<span data-ttu-id="23209-153">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="23209-153">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="23209-154">[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav dílčího odkazu.</span><span class="sxs-lookup"><span data-stu-id="23209-154">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status.</span></span>      |
| <span data-ttu-id="23209-155">StatusReason</span><span class="sxs-lookup"><span data-stu-id="23209-155">StatusReason</span></span>        | <span data-ttu-id="23209-156">řetězec</span><span class="sxs-lookup"><span data-stu-id="23209-156">string</span></span>                                                               | <span data-ttu-id="23209-157">Popisná zpráva o stavu</span><span class="sxs-lookup"><span data-stu-id="23209-157">A descriptive message about the status.</span></span> <span data-ttu-id="23209-158">Například vysvětlete, proč byl odkaz ztracen.</span><span class="sxs-lookup"><span data-stu-id="23209-158">For example, explain why the referral was lost.</span></span>                              |
| <span data-ttu-id="23209-159">ReferralType</span><span class="sxs-lookup"><span data-stu-id="23209-159">ReferralType</span></span>        | [<span data-ttu-id="23209-160">ReferralType</span><span class="sxs-lookup"><span data-stu-id="23209-160">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="23209-161">Představuje typ odkazu.</span><span class="sxs-lookup"><span data-stu-id="23209-161">Represents the referral type.</span></span>                                                                                        |
| <span data-ttu-id="23209-162">Qualification</span><span class="sxs-lookup"><span data-stu-id="23209-162">Qualification</span></span>       | [<span data-ttu-id="23209-163">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="23209-163">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="23209-164">Představuje kvalitu odkazu.</span><span class="sxs-lookup"><span data-stu-id="23209-164">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="23209-165">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="23209-165">CustomerProfile</span></span>     | [<span data-ttu-id="23209-166">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="23209-166">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="23209-167">Kontaktní údaje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="23209-167">Customer contact information.</span></span>                                                                                        |
| <span data-ttu-id="23209-168">Souhlas</span><span class="sxs-lookup"><span data-stu-id="23209-168">Consent</span></span>             | [<span data-ttu-id="23209-169">Souhlas</span><span class="sxs-lookup"><span data-stu-id="23209-169">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="23209-170">Příznaky souhlasu týkající se sdílení informací s ostatními organizacemi a jejich umožnění kontaktování uživatelů</span><span class="sxs-lookup"><span data-stu-id="23209-170">Consent flags around sharing information with other organizations and allowing them to contact users.</span></span>                |
| <span data-ttu-id="23209-171">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="23209-171">Details</span></span>             | [<span data-ttu-id="23209-172">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="23209-172">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="23209-173">Podrobnosti o zákazníkovi, poznámky, hodnota obchodu, datum ukončení měny.</span><span class="sxs-lookup"><span data-stu-id="23209-173">Customer details, notes, deal value, currency closing date.</span></span>                                                          |
| <span data-ttu-id="23209-174">Tým</span><span class="sxs-lookup"><span data-stu-id="23209-174">Team</span></span>                | [<span data-ttu-id="23209-175">Člen</span><span class="sxs-lookup"><span data-stu-id="23209-175">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="23209-176">Představuje uživatele v organizacích, kteří se účastní zapojení partnerů.</span><span class="sxs-lookup"><span data-stu-id="23209-176">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="23209-177">InviteContext</span><span class="sxs-lookup"><span data-stu-id="23209-177">InviteContext</span></span>       | [<span data-ttu-id="23209-178">InviteContext</span><span class="sxs-lookup"><span data-stu-id="23209-178">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="23209-179">Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.</span><span class="sxs-lookup"><span data-stu-id="23209-179">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="23209-180">Cíl</span><span class="sxs-lookup"><span data-stu-id="23209-180">Target</span></span>         | [<span data-ttu-id="23209-181">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="23209-181">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="23209-182">Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.</span><span class="sxs-lookup"><span data-stu-id="23209-182">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

### <a name="status-and-substatus-transition-states"></a><span data-ttu-id="23209-183">Stavy přechodu stavu a dílčího stavu</span><span class="sxs-lookup"><span data-stu-id="23209-183">Status and substatus transition states</span></span>

| <span data-ttu-id="23209-184">Status</span><span class="sxs-lookup"><span data-stu-id="23209-184">Status</span></span> | <span data-ttu-id="23209-185">Povolený přechod stavu</span><span class="sxs-lookup"><span data-stu-id="23209-185">Allowed Status Transition</span></span> | <span data-ttu-id="23209-186">Povolený dílčí stav</span><span class="sxs-lookup"><span data-stu-id="23209-186">Allowed Substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="23209-187">Nová</span><span class="sxs-lookup"><span data-stu-id="23209-187">New</span></span>    | <span data-ttu-id="23209-188">Nové, aktivní, uzavřené</span><span class="sxs-lookup"><span data-stu-id="23209-188">New, Active, Closed</span></span>       | <span data-ttu-id="23209-189">Čeká na vyřízení, přijato</span><span class="sxs-lookup"><span data-stu-id="23209-189">Pending, Received</span></span>            |
| <span data-ttu-id="23209-190">Aktivní</span><span class="sxs-lookup"><span data-stu-id="23209-190">Active</span></span> | <span data-ttu-id="23209-191">Aktivní, uzavřeno</span><span class="sxs-lookup"><span data-stu-id="23209-191">Active, Closed</span></span>            | <span data-ttu-id="23209-192">Přijato</span><span class="sxs-lookup"><span data-stu-id="23209-192">Accepted</span></span>                     |
| <span data-ttu-id="23209-193">Uzavřeno</span><span class="sxs-lookup"><span data-stu-id="23209-193">Closed</span></span> | <span data-ttu-id="23209-194">Uzavřeno</span><span class="sxs-lookup"><span data-stu-id="23209-194">Closed</span></span>                    | <span data-ttu-id="23209-195">Výhra, ztraceno, odmítnuto, vypršela platnost</span><span class="sxs-lookup"><span data-stu-id="23209-195">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="23209-196">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="23209-196">Request example</span></span>

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> <span data-ttu-id="23209-197">Odeberte `"links": { }` objekt z prostředku PUT.</span><span class="sxs-lookup"><span data-stu-id="23209-197">Remove the `"links": { }` object from the PUT resource.</span></span>

## <a name="rest-response"></a><span data-ttu-id="23209-198">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="23209-198">REST Response</span></span>

<span data-ttu-id="23209-199">V případě úspěchu vrátí tato metoda v těle odpovědi vyplněný prostředek [reference](referral-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="23209-199">If successful, this method returns the populated [referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="23209-200">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="23209-200">Response success and error codes</span></span>

<span data-ttu-id="23209-201">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="23209-201">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="23209-202">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="23209-202">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="23209-203">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="23209-203">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="23209-204">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="23209-204">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```