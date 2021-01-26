---
title: Vytvoření reference
description: Vytvořte nezávislé nebo sdílené odkazy v partnerském rozhraní API.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770332"
---
# <a name="create-a-referral"></a><span data-ttu-id="d3a24-103">Vytvoření reference</span><span class="sxs-lookup"><span data-stu-id="d3a24-103">Create a referral</span></span>

<span data-ttu-id="d3a24-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="d3a24-104">Applies to:</span></span>

- <span data-ttu-id="d3a24-105">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="d3a24-105">Partner API</span></span>

<span data-ttu-id="d3a24-106">V tomto tématu se dozvíte, jak vytvořit odkaz.</span><span class="sxs-lookup"><span data-stu-id="d3a24-106">This topic explains how to create a referral.</span></span> <span data-ttu-id="d3a24-107">Existují dva typy [ReferralType](referral-resources.md#referraltype):</span><span class="sxs-lookup"><span data-stu-id="d3a24-107">There are two types of [ReferralType](referral-resources.md#referraltype):</span></span>

1. <span data-ttu-id="d3a24-108">Nezávislé: kde je odkaz viditelný pro jednoho partnera.</span><span class="sxs-lookup"><span data-stu-id="d3a24-108">Independent: Where a referral is visible to one partner.</span></span>
2. <span data-ttu-id="d3a24-109">Shared: kde je odkaz viditelný pro dvě strany, které pracují společně.</span><span class="sxs-lookup"><span data-stu-id="d3a24-109">Shared: Where a referral is visible to two parties that are working together.</span></span> <span data-ttu-id="d3a24-110">Například pokud společnost Microsoft a partner pracují společně v rámci spoluprodejních operací, může být odkaz sdílen mezi obě strany.</span><span class="sxs-lookup"><span data-stu-id="d3a24-110">For example, if Microsoft and a partner are working together in a co-selling deal, a referral can be shared between both parties.</span></span> <span data-ttu-id="d3a24-111">Další informace najdete v části [Vytvoření sdíleného odkazu](#create-a-shared-referral).</span><span class="sxs-lookup"><span data-stu-id="d3a24-111">For more information, see the section [Creating a shared referral](#create-a-shared-referral).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3a24-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d3a24-112">Prerequisites</span></span>

- <span data-ttu-id="d3a24-113">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d3a24-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="d3a24-114">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="d3a24-114">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d3a24-115">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="d3a24-115">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d3a24-116">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="d3a24-116">Request syntax</span></span>

| <span data-ttu-id="d3a24-117">Metoda</span><span class="sxs-lookup"><span data-stu-id="d3a24-117">Method</span></span>  | <span data-ttu-id="d3a24-118">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="d3a24-118">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="d3a24-119">**SPUŠTĚNÍ**</span><span class="sxs-lookup"><span data-stu-id="d3a24-119">**POST**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a><span data-ttu-id="d3a24-120">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="d3a24-120">Request headers</span></span>

- <span data-ttu-id="d3a24-121">Další informace najdete v tématu [záhlaví REST rozhraní API pro partnery](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="d3a24-121">See [Partner API REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="d3a24-122">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="d3a24-122">Request body</span></span>

<span data-ttu-id="d3a24-123">Tato tabulka popisuje vlastnosti [odkazu](referral-resources.md) v těle žádosti o značku nového odkazu.</span><span class="sxs-lookup"><span data-stu-id="d3a24-123">This table describes the [Referral](referral-resources.md) properties in the request body for a brand new referral.</span></span>

| <span data-ttu-id="d3a24-124">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="d3a24-124">Property</span></span>            | <span data-ttu-id="d3a24-125">Typ</span><span class="sxs-lookup"><span data-stu-id="d3a24-125">Type</span></span>                                                                 | <span data-ttu-id="d3a24-126">Popis</span><span class="sxs-lookup"><span data-stu-id="d3a24-126">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d3a24-127">Název</span><span class="sxs-lookup"><span data-stu-id="d3a24-127">Name</span></span>                | <span data-ttu-id="d3a24-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="d3a24-128">string</span></span>                                                               | <span data-ttu-id="d3a24-129">Název odkazu</span><span class="sxs-lookup"><span data-stu-id="d3a24-129">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="d3a24-130">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="d3a24-130">ExternalReferenceId</span></span> | <span data-ttu-id="d3a24-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="d3a24-131">string</span></span>                                                               | <span data-ttu-id="d3a24-132">Externí identifikátor pro odkaz</span><span class="sxs-lookup"><span data-stu-id="d3a24-132">An external identifier for the referral.</span></span> <span data-ttu-id="d3a24-133">Například vlastní ID zájemce nebo příležitosti pro Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="d3a24-133">For example, your own Dynamics 365 lead or opportunity ID.</span></span>                   |
| <span data-ttu-id="d3a24-134">Status</span><span class="sxs-lookup"><span data-stu-id="d3a24-134">Status</span></span>              | [<span data-ttu-id="d3a24-135">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="d3a24-135">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="d3a24-136">[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu.</span><span class="sxs-lookup"><span data-stu-id="d3a24-136">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="d3a24-137">SubStatus</span><span class="sxs-lookup"><span data-stu-id="d3a24-137">Substatus</span></span>           | [<span data-ttu-id="d3a24-138">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="d3a24-138">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="d3a24-139">[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují dílčí stav odkazu.</span><span class="sxs-lookup"><span data-stu-id="d3a24-139">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral substatus.</span></span>       |
| <span data-ttu-id="d3a24-140">StatusReason</span><span class="sxs-lookup"><span data-stu-id="d3a24-140">StatusReason</span></span>        | <span data-ttu-id="d3a24-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="d3a24-141">string</span></span>                                                               | <span data-ttu-id="d3a24-142">Popisná zpráva o stavu</span><span class="sxs-lookup"><span data-stu-id="d3a24-142">A descriptive message about the status.</span></span> <span data-ttu-id="d3a24-143">Například vysvětlete, proč byl odkaz ztracen.</span><span class="sxs-lookup"><span data-stu-id="d3a24-143">For example, explain why the referral was lost.</span></span>                            |
| <span data-ttu-id="d3a24-144">ReferralType</span><span class="sxs-lookup"><span data-stu-id="d3a24-144">ReferralType</span></span>        | [<span data-ttu-id="d3a24-145">ReferralType</span><span class="sxs-lookup"><span data-stu-id="d3a24-145">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="d3a24-146">Představuje typ odkazu.</span><span class="sxs-lookup"><span data-stu-id="d3a24-146">Represents the referral type.</span></span> <span data-ttu-id="d3a24-147">**Požadovanou.**</span><span class="sxs-lookup"><span data-stu-id="d3a24-147">**Required.**</span></span>                                                                                        |
| <span data-ttu-id="d3a24-148">Qualification</span><span class="sxs-lookup"><span data-stu-id="d3a24-148">Qualification</span></span>       | [<span data-ttu-id="d3a24-149">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="d3a24-149">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="d3a24-150">Představuje kvalitu odkazu.</span><span class="sxs-lookup"><span data-stu-id="d3a24-150">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="d3a24-151">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="d3a24-151">CustomerProfile</span></span>     | [<span data-ttu-id="d3a24-152">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="d3a24-152">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="d3a24-153">Kontaktní údaje zákazníka.</span><span class="sxs-lookup"><span data-stu-id="d3a24-153">Customer contact information.</span></span>  <span data-ttu-id="d3a24-154">**Požadovanou.**</span><span class="sxs-lookup"><span data-stu-id="d3a24-154">**Required.**</span></span>                                                                                      |
| <span data-ttu-id="d3a24-155">Souhlas</span><span class="sxs-lookup"><span data-stu-id="d3a24-155">Consent</span></span>             | [<span data-ttu-id="d3a24-156">Souhlas</span><span class="sxs-lookup"><span data-stu-id="d3a24-156">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="d3a24-157">Příznaky souhlasu týkající se sdílení informací s ostatními organizacemi a jejich umožnění kontaktování uživatelů **Požadováno.**</span><span class="sxs-lookup"><span data-stu-id="d3a24-157">Consent flags around sharing information with other organizations and allowing them to contact users.**Required.**</span></span>               |
| <span data-ttu-id="d3a24-158">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="d3a24-158">Details</span></span>             | [<span data-ttu-id="d3a24-159">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="d3a24-159">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="d3a24-160">Podrobnosti o zákazníkovi, poznámky, hodnota obchodu, datum ukončení měny.</span><span class="sxs-lookup"><span data-stu-id="d3a24-160">Customer details, notes, deal value, currency closing date.</span></span> <span data-ttu-id="d3a24-161">**Požadovanou.**</span><span class="sxs-lookup"><span data-stu-id="d3a24-161">**Required.**</span></span>                                                           |
| <span data-ttu-id="d3a24-162">Tým</span><span class="sxs-lookup"><span data-stu-id="d3a24-162">Team</span></span>                | [<span data-ttu-id="d3a24-163">Člen</span><span class="sxs-lookup"><span data-stu-id="d3a24-163">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="d3a24-164">Představuje uživatele v organizacích, kteří se účastní zapojení partnerů.</span><span class="sxs-lookup"><span data-stu-id="d3a24-164">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="d3a24-165">InviteContext</span><span class="sxs-lookup"><span data-stu-id="d3a24-165">InviteContext</span></span>       | [<span data-ttu-id="d3a24-166">InviteContext</span><span class="sxs-lookup"><span data-stu-id="d3a24-166">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="d3a24-167">Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.</span><span class="sxs-lookup"><span data-stu-id="d3a24-167">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="d3a24-168">Cíl</span><span class="sxs-lookup"><span data-stu-id="d3a24-168">Target</span></span>         | [<span data-ttu-id="d3a24-169">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="d3a24-169">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="d3a24-170">Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.</span><span class="sxs-lookup"><span data-stu-id="d3a24-170">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

#### <a name="status--substatus-transition-states"></a><span data-ttu-id="d3a24-171">Stavový & stav přechodu dílčího stavu</span><span class="sxs-lookup"><span data-stu-id="d3a24-171">Status & Substatus transition states</span></span>

| <span data-ttu-id="d3a24-172">Status</span><span class="sxs-lookup"><span data-stu-id="d3a24-172">Status</span></span> | <span data-ttu-id="d3a24-173">Povolený přechod stavu</span><span class="sxs-lookup"><span data-stu-id="d3a24-173">Allowed status transition</span></span> | <span data-ttu-id="d3a24-174">Povolený dílčí stav</span><span class="sxs-lookup"><span data-stu-id="d3a24-174">Allowed substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="d3a24-175">Nová</span><span class="sxs-lookup"><span data-stu-id="d3a24-175">New</span></span>    | <span data-ttu-id="d3a24-176">Nové, aktivní, uzavřené</span><span class="sxs-lookup"><span data-stu-id="d3a24-176">New, Active, Closed</span></span>       | <span data-ttu-id="d3a24-177">Čeká na vyřízení, přijato</span><span class="sxs-lookup"><span data-stu-id="d3a24-177">Pending, Received</span></span>            |
| <span data-ttu-id="d3a24-178">Aktivní</span><span class="sxs-lookup"><span data-stu-id="d3a24-178">Active</span></span> | <span data-ttu-id="d3a24-179">Aktivní, uzavřeno</span><span class="sxs-lookup"><span data-stu-id="d3a24-179">Active, Closed</span></span>            | <span data-ttu-id="d3a24-180">Přijato</span><span class="sxs-lookup"><span data-stu-id="d3a24-180">Accepted</span></span>                     |
| <span data-ttu-id="d3a24-181">Uzavřeno</span><span class="sxs-lookup"><span data-stu-id="d3a24-181">Closed</span></span> | <span data-ttu-id="d3a24-182">Uzavřeno</span><span class="sxs-lookup"><span data-stu-id="d3a24-182">Closed</span></span>                    | <span data-ttu-id="d3a24-183">Výhra, ztraceno, odmítnuto, vypršela platnost</span><span class="sxs-lookup"><span data-stu-id="d3a24-183">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="d3a24-184">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="d3a24-184">Request example</span></span>

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="d3a24-185">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="d3a24-185">REST Response</span></span>

<span data-ttu-id="d3a24-186">V případě úspěchu vrátí tato metoda v těle odpovědi vyplněný prostředek [reference](referral-resources.md) .</span><span class="sxs-lookup"><span data-stu-id="d3a24-186">If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d3a24-187">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="d3a24-187">Response success and error codes</span></span>

<span data-ttu-id="d3a24-188">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="d3a24-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d3a24-189">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="d3a24-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d3a24-190">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d3a24-190">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d3a24-191">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="d3a24-191">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a><span data-ttu-id="d3a24-192">Vytvoření sdíleného odkazu</span><span class="sxs-lookup"><span data-stu-id="d3a24-192">Create a shared referral</span></span>

<span data-ttu-id="d3a24-193">Existují dva kroky k vytvoření odkazu na **sdílený** [typ odkazu](referral-resources.md#referraltype).</span><span class="sxs-lookup"><span data-stu-id="d3a24-193">There are two steps to create a referral of the **Shared** [referral type](referral-resources.md#referraltype).</span></span>

1. [<span data-ttu-id="d3a24-194">Vytvořit sdílený odkaz</span><span class="sxs-lookup"><span data-stu-id="d3a24-194">Create your shared referral</span></span>](#create-your-referral)
2. [<span data-ttu-id="d3a24-195">Vytvoření propojeného odkazu pro druhou stranu</span><span class="sxs-lookup"><span data-stu-id="d3a24-195">Create a connected referral for the second party</span></span>](#create-a-connected-referral)

<span data-ttu-id="d3a24-196">Následující postup popisuje tyto dva kroky při vytváření sdíleného odkazu.</span><span class="sxs-lookup"><span data-stu-id="d3a24-196">The following flow chart illustrates these two steps in creating a shared referral.</span></span>

![Vývojový diagram znázorňující sdílený odkaz se dvěma odkazy připojenými prostřednictvím rozhraní Microsoft Partner API](../images/SharedReferral.png)

### <a name="create-your-referral"></a><span data-ttu-id="d3a24-198">Vytvoření odkazu</span><span class="sxs-lookup"><span data-stu-id="d3a24-198">Create your referral</span></span>

1. <span data-ttu-id="d3a24-199">Vytvoří odkaz s [ReferralType](referral-resources.md#referraltype) nastavenou na Shared.</span><span class="sxs-lookup"><span data-stu-id="d3a24-199">Create a referral with [ReferralType](referral-resources.md#referraltype) set to shared.</span></span>
2. <span data-ttu-id="d3a24-200">Zkopírujte **engagementId** z odpovědi na vrácení.</span><span class="sxs-lookup"><span data-stu-id="d3a24-200">Copy the **engagementId** from the return response.</span></span>

<span data-ttu-id="d3a24-201">Ukázka [ReferralTarget](referral-resources.md#target) pro referenci</span><span class="sxs-lookup"><span data-stu-id="d3a24-201">[ReferralTarget](referral-resources.md#target) sample for referral</span></span>

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a><span data-ttu-id="d3a24-202">Vytvoření propojeného odkazu</span><span class="sxs-lookup"><span data-stu-id="d3a24-202">Create a connected referral</span></span>

1. <span data-ttu-id="d3a24-203">Vytvořte další odkaz na Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d3a24-203">Create another referral for Microsoft.</span></span>
2. <span data-ttu-id="d3a24-204">Zahrňte **enagementId** z vašeho odkazu, aby byly vzájemně vázané.</span><span class="sxs-lookup"><span data-stu-id="d3a24-204">Include the **enagementId** from your referral so they are tied together.</span></span>

<span data-ttu-id="d3a24-205">Ukázka [ReferralTarget](referral-resources.md#target) pro referenci Microsoftu</span><span class="sxs-lookup"><span data-stu-id="d3a24-205">[ReferralTarget](referral-resources.md#target) sample for Microsoft referral</span></span>

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```