---
title: Získání seznamu potenciálních zákazníků a příležitostí
description: Jak získat seznam potenciálních zákazníků a příležitostí pomocí partnerského rozhraní API.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 46243f8484a8068827e24e1d03f39ffddade1dbf
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770356"
---
# <a name="get-the-list-of-leads-and-opportunities"></a><span data-ttu-id="4df2c-103">Získání seznamu potenciálních zákazníků a příležitostí</span><span class="sxs-lookup"><span data-stu-id="4df2c-103">Get the list of leads and opportunities</span></span>

<span data-ttu-id="4df2c-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="4df2c-104">Applies to:</span></span>

- <span data-ttu-id="4df2c-105">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="4df2c-105">Partner API</span></span>

 <span data-ttu-id="4df2c-106">V tomto tématu se dozvíte, jak získat seznam zájemců přijatých ze stránky Microsoftu pro poskytovatele řešení a možnosti společného prodeje, které od prodejců Microsoftu nebo jiných partnerů obdrželi.</span><span class="sxs-lookup"><span data-stu-id="4df2c-106">This topic explains how to get the list of leads received from Microsoft solution provider page and co-sell opportunities received from Microsoft sellers or other partners.</span></span> <span data-ttu-id="4df2c-107">Tím se také načtou seznam příležitostí a příležitostí, které vytvořila vaše organizace, ze společného prodeje.</span><span class="sxs-lookup"><span data-stu-id="4df2c-107">This will also fetch the list of co-sell opportunities or pipeline deals created by your organization.</span></span>

> [!Note]
> <span data-ttu-id="4df2c-108">Zájemci přijatý od komerčního tržiště Microsoftu (Azure Marketplace a AppSource) se nepodporují.</span><span class="sxs-lookup"><span data-stu-id="4df2c-108">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4df2c-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4df2c-109">Prerequisites</span></span>

- <span data-ttu-id="4df2c-110">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4df2c-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="4df2c-111">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="4df2c-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="4df2c-112">Toto rozhraní API aktuálně podporuje jenom přístup uživatelů v případě, že se partneři musí nacházet v jedné z následujících rolí: globální správce, Správce odkazů nebo uživatel s odkazem.</span><span class="sxs-lookup"><span data-stu-id="4df2c-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="4df2c-113">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="4df2c-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4df2c-114">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="4df2c-114">Request syntax</span></span>

| <span data-ttu-id="4df2c-115">Metoda</span><span class="sxs-lookup"><span data-stu-id="4df2c-115">Method</span></span>  | <span data-ttu-id="4df2c-116">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="4df2c-116">Request URI</span></span>                                                    |
|:--------|:---------------------------------------------------------------|
| <span data-ttu-id="4df2c-117">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="4df2c-117">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a><span data-ttu-id="4df2c-118">Podporované operace OData</span><span class="sxs-lookup"><span data-stu-id="4df2c-118">Supported OData operations</span></span>

| <span data-ttu-id="4df2c-119">Název</span><span class="sxs-lookup"><span data-stu-id="4df2c-119">Name</span></span>     | <span data-ttu-id="4df2c-120">Popis</span><span class="sxs-lookup"><span data-stu-id="4df2c-120">Description</span></span>     | <span data-ttu-id="4df2c-121">Povinné</span><span class="sxs-lookup"><span data-stu-id="4df2c-121">Required</span></span>    | <span data-ttu-id="4df2c-122">Příklad</span><span class="sxs-lookup"><span data-stu-id="4df2c-122">Example</span></span>                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4df2c-123">$select</span><span class="sxs-lookup"><span data-stu-id="4df2c-123">$select</span></span>  | <span data-ttu-id="4df2c-124">Vybere pole</span><span class="sxs-lookup"><span data-stu-id="4df2c-124">Selects fields</span></span>  | <span data-ttu-id="4df2c-125">No</span><span class="sxs-lookup"><span data-stu-id="4df2c-125">No</span></span>          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| <span data-ttu-id="4df2c-126">$filter</span><span class="sxs-lookup"><span data-stu-id="4df2c-126">$filter</span></span>  | <span data-ttu-id="4df2c-127">Výsledky filtrů</span><span class="sxs-lookup"><span data-stu-id="4df2c-127">Filters results</span></span> | <span data-ttu-id="4df2c-128">Doporučeno</span><span class="sxs-lookup"><span data-stu-id="4df2c-128">Recommended</span></span> | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| <span data-ttu-id="4df2c-129">$orderby</span><span class="sxs-lookup"><span data-stu-id="4df2c-129">$orderby</span></span> | <span data-ttu-id="4df2c-130">Výsledky objednávek</span><span class="sxs-lookup"><span data-stu-id="4df2c-130">Orders results</span></span>  | <span data-ttu-id="4df2c-131">Doporučeno</span><span class="sxs-lookup"><span data-stu-id="4df2c-131">Recommended</span></span> | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a><span data-ttu-id="4df2c-132">Podporované parametry OrderBy</span><span class="sxs-lookup"><span data-stu-id="4df2c-132">Supported orderby parameters</span></span>

<span data-ttu-id="4df2c-133">Seznam potenciálních zákazníků a příležitostí můžete seřadit pomocí následujících parametrů $orderby.</span><span class="sxs-lookup"><span data-stu-id="4df2c-133">Use the following $orderby parameters to sort the list of leads and opportunities</span></span>

| <span data-ttu-id="4df2c-134">Název</span><span class="sxs-lookup"><span data-stu-id="4df2c-134">Name</span></span>            | <span data-ttu-id="4df2c-135">Typ</span><span class="sxs-lookup"><span data-stu-id="4df2c-135">Type</span></span>     | <span data-ttu-id="4df2c-136">Description</span><span class="sxs-lookup"><span data-stu-id="4df2c-136">Description</span></span>                                       |
|:----------------|:---------|:--------------------------------------------------|
| <span data-ttu-id="4df2c-137">createdDateTime</span><span class="sxs-lookup"><span data-stu-id="4df2c-137">createdDateTime</span></span> | <span data-ttu-id="4df2c-138">DateTime</span><span class="sxs-lookup"><span data-stu-id="4df2c-138">DateTime</span></span> | <span data-ttu-id="4df2c-139">Datum a čas vytvoření zájemce nebo příležitosti</span><span class="sxs-lookup"><span data-stu-id="4df2c-139">Creation date and time of the lead or opportunity</span></span> |
| <span data-ttu-id="4df2c-140">updatedDateTime</span><span class="sxs-lookup"><span data-stu-id="4df2c-140">updatedDateTime</span></span> | <span data-ttu-id="4df2c-141">DateTime</span><span class="sxs-lookup"><span data-stu-id="4df2c-141">DateTime</span></span> | <span data-ttu-id="4df2c-142">Aktualizovat datum a čas zájemce nebo příležitosti</span><span class="sxs-lookup"><span data-stu-id="4df2c-142">Update date and time of the lead or opportunity</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="4df2c-143">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="4df2c-143">Request headers</span></span>

<span data-ttu-id="4df2c-144">Další informace najdete v části [partner – záhlaví REST](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="4df2c-144">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="4df2c-145">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="4df2c-145">Request body</span></span>

<span data-ttu-id="4df2c-146">Žádné</span><span class="sxs-lookup"><span data-stu-id="4df2c-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4df2c-147">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="4df2c-147">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="4df2c-148">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="4df2c-148">REST response</span></span>

<span data-ttu-id="4df2c-149">V případě úspěchu obsahuje tělo odpovědi kolekci [zájemců a/nebo příležitostí](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4df2c-149">If successful, the response body contains a collection of [leads and/or opportunities](referral-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4df2c-150">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="4df2c-150">Response success and error codes</span></span>

<span data-ttu-id="4df2c-151">Každá odpověď je dodávána se [stavovým kódem http](error-codes.md) , který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="4df2c-151">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4df2c-152">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="4df2c-152">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="4df2c-153">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="4df2c-153">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
  "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
  "@odata.count": 1,
  "value": [
    {
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
        "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
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
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
          "method": "GET"
        },
        "self": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
          "method": "GET"
        }
      }
    }
  ],
  "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxX"
}
```

<span data-ttu-id="4df2c-154">`@odata.nextLink`K získání další stránky výsledků použijte.</span><span class="sxs-lookup"><span data-stu-id="4df2c-154">Use the `@odata.nextLink` to get the next page of results.</span></span>

> [!Note]
> <span data-ttu-id="4df2c-155">Pole v příkladu illustratration výše nejsou vyčerpávající.</span><span class="sxs-lookup"><span data-stu-id="4df2c-155">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="4df2c-156">Skutečná odpověď rozhraní API obsahuje více polí, jako jsou například týmy zákazníka a partnera.</span><span class="sxs-lookup"><span data-stu-id="4df2c-156">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="4df2c-157">Úplný seznam podporovaných polí najdete v tématu věnovaném [prostředkům reference](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4df2c-157">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>

## <a name="sample-requests"></a><span data-ttu-id="4df2c-158">Ukázkové požadavky</span><span class="sxs-lookup"><span data-stu-id="4df2c-158">Sample requests</span></span>

1. <span data-ttu-id="4df2c-159">Získá prvních 10 nejaktuálnějších příležitostí pro prodej.</span><span class="sxs-lookup"><span data-stu-id="4df2c-159">Gets the top 10 most recent inbound co-sell opportunities.</span></span> <span data-ttu-id="4df2c-160">Požadavek načte příležitosti iniciované obchodním zástupcem Microsoftu nebo jiným partnerem a vyzve organizaci, aby se účastnila aktivity spoluprodeje.</span><span class="sxs-lookup"><span data-stu-id="4df2c-160">The request will fetch opportunities initiated by a Microsoft sales representative or another partner, inviting your organization to participate in a co-selling activity.</span></span>
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. <span data-ttu-id="4df2c-161">Získá nejnovější příchozí zájemce a příležitosti, na které nebyly odpovědi reagovat.</span><span class="sxs-lookup"><span data-stu-id="4df2c-161">Gets the most recent inbound leads and opportunities that have not been responded to.</span></span>  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > <span data-ttu-id="4df2c-162">Pokud neodpovíte na zájemce nebo příležitost v rámci přiděleného času (v současnosti 14 dnů), archivaci vyprší a upozorněte buď společnost Microsoft, nebo partnera, který vám tuto příležitost poslal.</span><span class="sxs-lookup"><span data-stu-id="4df2c-162">If you don't respond to a lead or opportunity within the allotted time (currently 14 days), we'll archive it as Expired and notify either Microsoft or the partner who sent you this opportunity.</span></span>

3. <span data-ttu-id="4df2c-163">Získá nejnovější aktivní možnosti společného prodeje iniciované vaší organizací a na základě konkrétního prodejce bude pracovat.</span><span class="sxs-lookup"><span data-stu-id="4df2c-163">Gets the most recent active co-sell opportunities initiated by your organization and being worked on by a specific seller.</span></span>
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```