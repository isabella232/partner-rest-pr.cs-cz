---
title: Získání potencionálního zákazníka nebo příležitosti podle ID
description: Získejte zájemce nebo příležitost podle ID.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcfaea393afc6a9d09946b4c31b7168ba26aa255
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770357"
---
# <a name="get-a-lead-or-opportunity-by-id"></a><span data-ttu-id="670bd-103">Získání potencionálního zákazníka nebo příležitosti podle ID</span><span class="sxs-lookup"><span data-stu-id="670bd-103">Get a lead or opportunity by Id</span></span>

<span data-ttu-id="670bd-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="670bd-104">Applies to:</span></span>

- <span data-ttu-id="670bd-105">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="670bd-105">Partner API</span></span>

<span data-ttu-id="670bd-106">V tomto tématu se dozvíte, jak získat příležitost zájemce nebo společný prodej podle ID.</span><span class="sxs-lookup"><span data-stu-id="670bd-106">This topic explains how to get a lead or co-sell opportunity by Id.</span></span>

> [!Note]
> <span data-ttu-id="670bd-107">Zájemci přijatý od komerčního tržiště Microsoftu (Azure Marketplace a AppSource) se nepodporují.</span><span class="sxs-lookup"><span data-stu-id="670bd-107">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="670bd-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="670bd-108">Prerequisites</span></span>

- <span data-ttu-id="670bd-109">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="670bd-109">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="670bd-110">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="670bd-110">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="670bd-111">Toto rozhraní API aktuálně podporuje jenom přístup uživatelů v případě, že se partneři musí nacházet v jedné z následujících rolí: globální správce, Správce odkazů nebo uživatel s odkazem.</span><span class="sxs-lookup"><span data-stu-id="670bd-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="670bd-112">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="670bd-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="670bd-113">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="670bd-113">Request syntax</span></span>

| <span data-ttu-id="670bd-114">Metoda</span><span class="sxs-lookup"><span data-stu-id="670bd-114">Method</span></span>   | <span data-ttu-id="670bd-115">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="670bd-115">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="670bd-116">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="670bd-116">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a><span data-ttu-id="670bd-117">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="670bd-117">URI parameter</span></span>


| <span data-ttu-id="670bd-118">Název</span><span class="sxs-lookup"><span data-stu-id="670bd-118">Name</span></span>                   | <span data-ttu-id="670bd-119">Typ</span><span class="sxs-lookup"><span data-stu-id="670bd-119">Type</span></span>     | <span data-ttu-id="670bd-120">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="670bd-120">Required</span></span> | <span data-ttu-id="670bd-121">Popis</span><span class="sxs-lookup"><span data-stu-id="670bd-121">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="670bd-122">Id</span><span class="sxs-lookup"><span data-stu-id="670bd-122">Id</span></span>                      | <span data-ttu-id="670bd-123">řetězec</span><span class="sxs-lookup"><span data-stu-id="670bd-123">string</span></span>   | <span data-ttu-id="670bd-124">Yes</span><span class="sxs-lookup"><span data-stu-id="670bd-124">Yes</span></span>       | <span data-ttu-id="670bd-125">Jedinečný identifikátor příležitosti zájemce nebo společného prodeje</span><span class="sxs-lookup"><span data-stu-id="670bd-125">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="670bd-126">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="670bd-126">Request headers</span></span>

<span data-ttu-id="670bd-127">Další informace najdete v části [partner – záhlaví REST](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="670bd-127">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="670bd-128">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="670bd-128">Request body</span></span>

<span data-ttu-id="670bd-129">Žádné</span><span class="sxs-lookup"><span data-stu-id="670bd-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="670bd-130">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="670bd-130">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="670bd-131">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="670bd-131">REST response</span></span>

<span data-ttu-id="670bd-132">V případě úspěchu text odpovědi obsahuje [zájemce nebo příležitost](referral-resources.md) , které odpovídají ID.</span><span class="sxs-lookup"><span data-stu-id="670bd-132">If successful, the response body contains the [lead or opportunity](referral-resources.md) matching the Id.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="670bd-133">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="670bd-133">Response success and error codes</span></span>

<span data-ttu-id="670bd-134">Každá odpověď je dodávána se [stavovým kódem http](error-codes.md) , který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="670bd-134">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="670bd-135">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="670bd-135">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="670bd-136">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="670bd-136">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
    "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
    "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "createdDateTime": "2020-10-30T21:03:00.0000000Z",
    "updatedDateTime": "2020-10-30T21:03:00.0000000Z",
    "status": "New",
    "substatus": "Pending",
    "qualification": "Direct",
    "type": "Independent",
    "direction": "Incoming",
    "customerProfile": {
      "name": "Fabrikam Customer Inc",
      "address": {
        "addressLine1": "One Microsoft Way",
        "addressLine2": "",
        "city": "Redmond",
        "state": "WA",
        "postalCode": "98052",
        "country": "US"
      }
    },
    "details": {
      "notes": "We are interested in deploying Microsoft 365 and are looking forsupport in training our employees. Can you help?",
      "dealValue": 10000,
      "currency": "USD",
      "closingDateTime": "2020-12-01T00:00:00Z",
      "requirements": {
          "industries": [ { "id": "Education" } ],
          "products": [ { "id": "Microsoft365" } ],
          "services": [ { "id": "LearningAndCertification" } ],
          "solutions": [ { "id": "SOL-Microsoft365", "name": "Microsoft365" }
        ]
      }
    },
    "links": {
      "relatedReferrals": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
        "method": "GET"
      },
      "self": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referralsc5fbb3b6-be74-4795-9fb5-4324c73fed37",
        "method": "GET"
      }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```

> [!Note]
> <span data-ttu-id="670bd-137">Pole v příkladu illustratration výše nejsou vyčerpávající.</span><span class="sxs-lookup"><span data-stu-id="670bd-137">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="670bd-138">Skutečná odpověď rozhraní API obsahuje více polí, jako jsou například týmy zákazníka a partnera.</span><span class="sxs-lookup"><span data-stu-id="670bd-138">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="670bd-139">Úplný seznam podporovaných polí najdete v tématu věnovaném [prostředkům reference](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="670bd-139">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>