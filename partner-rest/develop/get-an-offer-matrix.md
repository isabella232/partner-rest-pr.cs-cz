---
title: Získání matice nabídek
description: Získání matice nabídek pro dané datum Podporuje filtry pro získání historie podle měsíce.
ms.date: 02/11/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e53276c1170febab002d35a42c88c1f96f7b7428
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2021
ms.locfileid: "113131297"
---
# <a name="get-an-offer-matrix"></a><span data-ttu-id="ab920-104">Získání matice nabídek</span><span class="sxs-lookup"><span data-stu-id="ab920-104">Get an offer matrix</span></span>

<span data-ttu-id="ab920-105">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="ab920-105">Applies to:</span></span>

- <span data-ttu-id="ab920-106">Partner API</span><span class="sxs-lookup"><span data-stu-id="ab920-106">Partner API</span></span>
- <span data-ttu-id="ab920-107">Prostředí M365/D365 New Commerce technical preview.</span><span class="sxs-lookup"><span data-stu-id="ab920-107">The M365/D365 New Commerce experience technical preview.</span></span> <span data-ttu-id="ab920-108">Níže uvedené změny v novém obchodování jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.</span><span class="sxs-lookup"><span data-stu-id="ab920-108">The below New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

<span data-ttu-id="ab920-109">Toto téma vysvětluje, jak získat matici nabídek pro daný měsíc.</span><span class="sxs-lookup"><span data-stu-id="ab920-109">This topic explains how to get an offer matrix for a given month.</span></span> <span data-ttu-id="ab920-110">Matice nabídek obsahuje vlastnosti a pravidla nákupu produktů a SKU.</span><span class="sxs-lookup"><span data-stu-id="ab920-110">The offer matrix includes properties and purchase rules for the products and skus.</span></span> <span data-ttu-id="ab920-111">Tato metoda podporuje filtry pro získání historie podle měsíce.</span><span class="sxs-lookup"><span data-stu-id="ab920-111">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab920-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ab920-112">Prerequisites</span></span>

- <span data-ttu-id="ab920-113">Přihlašovací údaje, jak je [popsáno Partner API ověřování.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ab920-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="ab920-114">Tento scénář podporuje pouze ověřování uživatelů aplikací.</span><span class="sxs-lookup"><span data-stu-id="ab920-114">This scenario only supports application user authentication.</span></span> <span data-ttu-id="ab920-115">Pouze pro aplikace se zatím nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="ab920-115">Application-only is not yet supported.</span></span> <span data-ttu-id="ab920-116">Partneři, u které dojde **k chybě http:400,** by si měli Partner API [dokumentaci k ověřování.](api-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ab920-116">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="ab920-117">Toto rozhraní API v současné době podporuje pouze uživatelský přístup, kde partneři musí mít jednu z následujících rolí: globální správce, agent pro správu nebo prodejní agent.</span><span class="sxs-lookup"><span data-stu-id="ab920-117">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="ab920-118">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="ab920-118">Details</span></span>

- <span data-ttu-id="ab920-119">Funkce Current vrací data pouze pro aktualizované nové komerční produkty založené na licencích.</span><span class="sxs-lookup"><span data-stu-id="ab920-119">Current returns data only for updated new commerce license-based products.</span></span>
- <span data-ttu-id="ab920-120">Aktuální ceny zahrnují produkty dostupné v aktuálním měsíci do data volání rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="ab920-120">Current pricing includes products available during the current month to the date the API is called.</span></span> <span data-ttu-id="ab920-121">Předchozí měsíce zahrnují datum k poslednímu dni vybraného měsíce.</span><span class="sxs-lookup"><span data-stu-id="ab920-121">Previous months include date as of the last day of the selected month.</span></span>
- <span data-ttu-id="ab920-122">Tato metoda vrátí data jako datový proud souboru.</span><span class="sxs-lookup"><span data-stu-id="ab920-122">This method returns data as a file stream.</span></span> <span data-ttu-id="ab920-123">Stream souboru je buď .csv soubor, nebo komprimovaná verze souboru .csv.</span><span class="sxs-lookup"><span data-stu-id="ab920-123">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="ab920-124">Podrobnosti o tom, jak požádat o komprimované soubory, jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="ab920-124">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ab920-125">Požadavek REST</span><span class="sxs-lookup"><span data-stu-id="ab920-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ab920-126">Syntaxe požadavku</span><span class="sxs-lookup"><span data-stu-id="ab920-126">Request syntax</span></span>

| <span data-ttu-id="ab920-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="ab920-127">Method</span></span>   | <span data-ttu-id="ab920-128">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="ab920-128">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ab920-129">**Dostat**</span><span class="sxs-lookup"><span data-stu-id="ab920-129">**GET**</span></span> | <span data-ttu-id="ab920-130"> https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month={date})/$value</span><span class="sxs-lookup"><span data-stu-id="ab920-130">https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span></span> |

### <a name="uri-filter-parameters"></a><span data-ttu-id="ab920-131">Parametry filtru identifikátorů URI</span><span class="sxs-lookup"><span data-stu-id="ab920-131">URI filter parameters</span></span>

<span data-ttu-id="ab920-132">Použijte následující parametry filtru.</span><span class="sxs-lookup"><span data-stu-id="ab920-132">Use the following filter parameters.</span></span>

| <span data-ttu-id="ab920-133">Název</span><span class="sxs-lookup"><span data-stu-id="ab920-133">Name</span></span>                   | <span data-ttu-id="ab920-134">Typ</span><span class="sxs-lookup"><span data-stu-id="ab920-134">Type</span></span>     | <span data-ttu-id="ab920-135">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="ab920-135">Required</span></span> | <span data-ttu-id="ab920-136">Popis</span><span class="sxs-lookup"><span data-stu-id="ab920-136">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="ab920-137">Month (Měsíc)</span><span class="sxs-lookup"><span data-stu-id="ab920-137">Month</span></span>| <span data-ttu-id="ab920-138">řetězec</span><span class="sxs-lookup"><span data-stu-id="ab920-138">string</span></span>   | <span data-ttu-id="ab920-139">No</span><span class="sxs-lookup"><span data-stu-id="ab920-139">No</span></span> | <span data-ttu-id="ab920-140">Musí splňovat YYYYMM pro požadovaný ceník.</span><span class="sxs-lookup"><span data-stu-id="ab920-140">Must adhere to YYYYMM for the price sheet being requested.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ab920-141">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="ab920-141">Request headers</span></span>

- <span data-ttu-id="ab920-142">Další [informace najdete v tématu Hlavičky REST](headers.md) pro partnery.</span><span class="sxs-lookup"><span data-stu-id="ab920-142">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="ab920-143">Kromě výše uvedených hlaviček je možné soubory s cenami načíst jako komprimované, což snižuje šířku pásma a dobu stahování.</span><span class="sxs-lookup"><span data-stu-id="ab920-143">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="ab920-144">Ve výchozím nastavení nejsou soubory komprimované.</span><span class="sxs-lookup"><span data-stu-id="ab920-144">By default the files are not compressed.</span></span> <span data-ttu-id="ab920-145">Pokud chcete získat komprimované verze souborů, můžete zahrnout následující hodnotu hlavičky.</span><span class="sxs-lookup"><span data-stu-id="ab920-145">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="ab920-146">Uvědomte si, že komprimované listy jsou k dispozici pouze od dubna 2020, ale všechny listy před dubnem 2020 jsou k dispozici pouze jako komprimované.</span><span class="sxs-lookup"><span data-stu-id="ab920-146">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="ab920-147">Hlavička</span><span class="sxs-lookup"><span data-stu-id="ab920-147">Header</span></span>                   | <span data-ttu-id="ab920-148">Typ hodnoty</span><span class="sxs-lookup"><span data-stu-id="ab920-148">Value Type</span></span>     | <span data-ttu-id="ab920-149">Hodnota</span><span class="sxs-lookup"><span data-stu-id="ab920-149">Value</span></span> | <span data-ttu-id="ab920-150">Popis</span><span class="sxs-lookup"><span data-stu-id="ab920-150">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="ab920-151">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="ab920-151">Accept-Encoding</span></span>| <span data-ttu-id="ab920-152">řetězec</span><span class="sxs-lookup"><span data-stu-id="ab920-152">string</span></span>   | <span data-ttu-id="ab920-153">Deflaci</span><span class="sxs-lookup"><span data-stu-id="ab920-153">deflate</span></span>| <span data-ttu-id="ab920-154">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="ab920-154">Optional.</span></span> <span data-ttu-id="ab920-155">Pokud je vynechán datový proud souboru není komprimován.</span><span class="sxs-lookup"><span data-stu-id="ab920-155">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="ab920-156">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="ab920-156">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="ab920-157">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="ab920-157">REST response</span></span>

<span data-ttu-id="ab920-158">V případě úspěchu tato metoda vrátí matici nabídek jako stream souboru.</span><span class="sxs-lookup"><span data-stu-id="ab920-158">If successful, this method returns an offer matrix as a file stream.</span></span> <span data-ttu-id="ab920-159">Stream souboru je buď .csv soubor, nebo komprimovaná verze souboru .csv.</span><span class="sxs-lookup"><span data-stu-id="ab920-159">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ab920-160">Kódy chyb a úspěšné odpovědi</span><span class="sxs-lookup"><span data-stu-id="ab920-160">Response success and error codes</span></span>

<span data-ttu-id="ab920-161">Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="ab920-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ab920-162">K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě.</span><span class="sxs-lookup"><span data-stu-id="ab920-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ab920-163">Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ab920-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ab920-164">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="ab920-164">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=updatedoffice.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","ProvisioningId","ProvisioningString","MinLicenses","MaxLicenses","AssetOwnershipLimit","AssetOwnershipLimitType","ProductSkuPreRequisites","ProductSkuConversion","Description","AllowedCountries" 
"Microsoft 365 Business Basic","CFQ7TTC0LH18","0001","Microsoft 365 Business Basic","3b555118-da6a-4418-894f-7df1e2096870","O365_BUSINESS_ESSENTIALS","1","300","2","ConcurrentCount","","CFQ7TTC0LDPB/0001,CFQ7TTC0LF8Q/0001","Best for businesses that need professional...","AD;AE;AF;AG;AI;AL;AM;AO..."
======= Truncated ==============

```
