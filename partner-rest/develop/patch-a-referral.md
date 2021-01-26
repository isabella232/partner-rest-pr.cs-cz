---
title: Aktualizace potenciálního zákazníka nebo příležitosti
description: Umožňuje aktualizovat podrobnosti o zájemci nebo příležitosti.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770360"
---
# <a name="update-a-lead-or-opportunity"></a><span data-ttu-id="4d9e5-103">Aktualizace potenciálního zákazníka nebo příležitosti</span><span class="sxs-lookup"><span data-stu-id="4d9e5-103">Update a lead or opportunity</span></span>

<span data-ttu-id="4d9e5-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="4d9e5-104">Applies to:</span></span>

- <span data-ttu-id="4d9e5-105">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="4d9e5-105">Partner API</span></span>

<span data-ttu-id="4d9e5-106">V tomto tématu se dozvíte, jak aktualizovat podrobnosti o zájemcích nebo příležitostech, jako je například hodnota koupě, odhadované datum uzavření nebo Správa fází prodeje mezi další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-106">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d9e5-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4d9e5-107">Prerequisites</span></span>

- <span data-ttu-id="4d9e5-108">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="4d9e5-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="4d9e5-109">Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="4d9e5-110">Toto rozhraní API aktuálně podporuje jenom přístup uživatelů v případě, že se partneři musí nacházet v jedné z následujících rolí: globální správce, Správce odkazů nebo uživatel s odkazem.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-110">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="4d9e5-111">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="4d9e5-111">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4d9e5-112">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="4d9e5-112">Request syntax</span></span>

| <span data-ttu-id="4d9e5-113">Metoda</span><span class="sxs-lookup"><span data-stu-id="4d9e5-113">Method</span></span>  | <span data-ttu-id="4d9e5-114">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="4d9e5-114">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="4d9e5-115">**POUŽITA**</span><span class="sxs-lookup"><span data-stu-id="4d9e5-115">**PATCH**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a><span data-ttu-id="4d9e5-116">Parametr URI</span><span class="sxs-lookup"><span data-stu-id="4d9e5-116">URI parameter</span></span>


| <span data-ttu-id="4d9e5-117">Název</span><span class="sxs-lookup"><span data-stu-id="4d9e5-117">Name</span></span>                   | <span data-ttu-id="4d9e5-118">Typ</span><span class="sxs-lookup"><span data-stu-id="4d9e5-118">Type</span></span>     | <span data-ttu-id="4d9e5-119">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="4d9e5-119">Required</span></span> | <span data-ttu-id="4d9e5-120">Popis</span><span class="sxs-lookup"><span data-stu-id="4d9e5-120">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="4d9e5-121">Id</span><span class="sxs-lookup"><span data-stu-id="4d9e5-121">Id</span></span>                      | <span data-ttu-id="4d9e5-122">řetězec</span><span class="sxs-lookup"><span data-stu-id="4d9e5-122">string</span></span>   | <span data-ttu-id="4d9e5-123">Yes</span><span class="sxs-lookup"><span data-stu-id="4d9e5-123">Yes</span></span>       | <span data-ttu-id="4d9e5-124">Jedinečný identifikátor příležitosti zájemce nebo společného prodeje</span><span class="sxs-lookup"><span data-stu-id="4d9e5-124">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="4d9e5-125">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="4d9e5-125">Request headers</span></span>

<span data-ttu-id="4d9e5-126">Další informace najdete v části [partner – záhlaví REST](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="4d9e5-126">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="4d9e5-127">Text požadavku</span><span class="sxs-lookup"><span data-stu-id="4d9e5-127">Request body</span></span>

<span data-ttu-id="4d9e5-128">Tělo žádosti následuje po formátu [opravy JSON](https://tools.ietf.org/html/rfc6902) .</span><span class="sxs-lookup"><span data-stu-id="4d9e5-128">The request body follows the [Json Patch](https://tools.ietf.org/html/rfc6902) format.</span></span> <span data-ttu-id="4d9e5-129">Dokument opravy JSON má pole operací.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-129">A JSON Patch document has an array of operations.</span></span> <span data-ttu-id="4d9e5-130">Každá operace identifikuje konkrétní typ změny.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-130">Each operation identifies a particular type of change.</span></span> <span data-ttu-id="4d9e5-131">Příklady takových změn zahrnují přidání prvku pole nebo nahrazení hodnoty vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-131">Examples of such changes include adding an array element or replacing a property value.</span></span>

> [!Important]
> <span data-ttu-id="4d9e5-132">Rozhraní API aktuálně podporuje pouze `replace` operace a `add` .</span><span class="sxs-lookup"><span data-stu-id="4d9e5-132">The API currently only supports the `replace` and `add` operations.</span></span>

### <a name="request-example"></a><span data-ttu-id="4d9e5-133">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="4d9e5-133">Request example</span></span>

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> <span data-ttu-id="4d9e5-134">Pokud je předána hlavička **If-Match** , bude použita pro řízení souběžnosti.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-134">If the **If-Match** header is passed, it will be used for concurrency control.</span></span>

## <a name="rest-response"></a><span data-ttu-id="4d9e5-135">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="4d9e5-135">REST Response</span></span>

<span data-ttu-id="4d9e5-136">V případě úspěchu obsahuje tělo odpovědi aktualizovaný [zájemce nebo příležitost](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4d9e5-136">If successful, the response body contains the updated [lead or opportunity](referral-resources.md).</span></span>


### <a name="response-success-and-error-codes"></a><span data-ttu-id="4d9e5-137">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="4d9e5-137">Response success and error codes</span></span>

<span data-ttu-id="4d9e5-138">Každá odpověď je dodávána se [stavovým kódem http](error-codes.md) , který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-138">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4d9e5-139">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-139">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="4d9e5-140">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="4d9e5-140">Response example</span></span>

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> <span data-ttu-id="4d9e5-141">Tělo odpovědi závisí na hlavičce **preferovat** .</span><span class="sxs-lookup"><span data-stu-id="4d9e5-141">The response body depends on the **Prefer** header.</span></span> <span data-ttu-id="4d9e5-142">Pokud je hodnota hlavičky v požadavku vynechána, text odpovědi je prázdný kódem stavu HTTP 204.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-142">If the header value is omitted in the request, the response body is empty with a HTTP Status code 204.</span></span> <span data-ttu-id="4d9e5-143">Přidejte `Prefer: return=representation` do záhlaví, abyste získali aktualizovaný zájemce nebo příležitost.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-143">Add `Prefer: return=representation` to the header to get the updated lead or opportunity.</span></span>

## <a name="sample-requests"></a><span data-ttu-id="4d9e5-144">Ukázkové požadavky</span><span class="sxs-lookup"><span data-stu-id="4d9e5-144">Sample requests</span></span>

1. <span data-ttu-id="4d9e5-145">Aktualizuje hodnotu obchodu s příležitostí na 10000 a aktualizuje poznámky.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-145">Updates the deal value for the opportunity to 10000 and updates the notes.</span></span> <span data-ttu-id="4d9e5-146">Neexistují žádné kontroly souběžnosti z důvodu neexistence `If-Match` hlavičky.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-146">There are no concurrency checks because of the absense of the `If-Match` header.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. <span data-ttu-id="4d9e5-147">Aktualizuje stav zájemce nebo příležitosti k získání.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-147">Updates the status of a lead or opportunity to Won.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > <span data-ttu-id="4d9e5-148">`status`Pole a `substatus` by měly být v souladu s povolenou sadou přechodových hodnot, jak je popsáno [zde](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4d9e5-148">The `status` and `substatus` fields should conform to the allowed set of transition values as described [here](referral-resources.md).</span></span>

3. <span data-ttu-id="4d9e5-149">Přidá nového člena z vaší organizace do týmu zájemce nebo příležitosti.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-149">Adds a new member from your organization to the lead or opportunity team.</span></span> <span data-ttu-id="4d9e5-150">Odpověď bude obsahovat aktualizovaného zájemce nebo příležitosti z důvodu přítomnosti `Prefer: return=representation` hlavičky.</span><span class="sxs-lookup"><span data-stu-id="4d9e5-150">The response will contain the updated lead or opportunity because of the presence of the `Prefer: return=representation` header.</span></span>

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```
