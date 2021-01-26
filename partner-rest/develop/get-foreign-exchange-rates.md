---
title: Získání směnných kurzů
description: Získejte devizové sazby za daný měsíc.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770353"
---
# <a name="get-foreign-exchange-rates"></a><span data-ttu-id="528f6-103">Získání směnných kurzů</span><span class="sxs-lookup"><span data-stu-id="528f6-103">Get foreign exchange rates</span></span>

<span data-ttu-id="528f6-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="528f6-104">Applies to:</span></span>

- <span data-ttu-id="528f6-105">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="528f6-105">Partner API</span></span>

<span data-ttu-id="528f6-106">Toto téma vysvětluje, jak získat směnné sazby za daný měsíc.</span><span class="sxs-lookup"><span data-stu-id="528f6-106">This topic explains how to get foreign exchange rates for a given month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="528f6-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="528f6-107">Prerequisites</span></span>

- <span data-ttu-id="528f6-108">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="528f6-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="528f6-109">Tento scénář podporuje pouze ověření uživatele aplikace.</span><span class="sxs-lookup"><span data-stu-id="528f6-109">This scenario only supports application user authentication.</span></span> <span data-ttu-id="528f6-110">Pouze aplikace není zatím podporována.</span><span class="sxs-lookup"><span data-stu-id="528f6-110">Application-only is not yet supported.</span></span>
- <span data-ttu-id="528f6-111">Toto rozhraní API aktuálně podporuje jenom přístup uživatelů, kde se partneři musí nacházet v jedné z následujících rolí: globální správce, agent pro správu nebo agent pro prodej.</span><span class="sxs-lookup"><span data-stu-id="528f6-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>


## <a name="details"></a><span data-ttu-id="528f6-112">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="528f6-112">Details</span></span>

- <span data-ttu-id="528f6-113">V současné době se používá s funkcí [získat cenové ceníek](get-a-price-sheet.md) k výpočtu očekávaných poplatků za místní měny Azure Plan CSP.</span><span class="sxs-lookup"><span data-stu-id="528f6-113">Currently used with [get price sheet API](get-a-price-sheet.md) to calculate expected charges for Azure plan CSP local currencies.</span></span>
- <span data-ttu-id="528f6-114">Sazby za cizí směnky budou platit pro celý měsíc, který je publikovaná.</span><span class="sxs-lookup"><span data-stu-id="528f6-114">Foreign exchange rates hold true for the entire month they are posted.</span></span>
- <span data-ttu-id="528f6-115">Další informace o [cenách](pricing.md) plánu Azure najdete v [dokumentaci k ceníkům Azure Plan](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="528f6-115">More information about Azure plan [pricing](pricing.md) can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="528f6-116">Ceny partnerů a rozhraní API pro cizí kurz nejsou součástí [sady SDK partnerského centra](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="528f6-116">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="528f6-117">Tato metoda vrací výsledky jako datový proud souboru.</span><span class="sxs-lookup"><span data-stu-id="528f6-117">This method returns results as a file stream.</span></span> <span data-ttu-id="528f6-118">Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv.</span><span class="sxs-lookup"><span data-stu-id="528f6-118">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="528f6-119">Podrobnosti o tom, jak vyžádat komprimované soubory, jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="528f6-119">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="528f6-120">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="528f6-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="528f6-121">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="528f6-121">Request syntax</span></span>

| <span data-ttu-id="528f6-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="528f6-122">Method</span></span>   | <span data-ttu-id="528f6-123">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="528f6-123">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="528f6-124">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="528f6-124">**GET**</span></span> | <span data-ttu-id="528f6-125"> https://api.partner.microsoft.com/v1.0/sales/fxrates(Month={month})/$value</span><span class="sxs-lookup"><span data-stu-id="528f6-125">https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='{month}')/$value</span></span>                                  |

### <a name="uri-required-parameters"></a><span data-ttu-id="528f6-126">Parametry vyžadované identifikátorem URI</span><span class="sxs-lookup"><span data-stu-id="528f6-126">URI required parameters</span></span>

<span data-ttu-id="528f6-127">Použijte následující parametry cesty, abyste si vyžádali měsíc cizích devizových sazeb, které chcete.</span><span class="sxs-lookup"><span data-stu-id="528f6-127">Use the following path parameters to request the month of foreign exchange rates you want.</span></span>

| <span data-ttu-id="528f6-128">Název</span><span class="sxs-lookup"><span data-stu-id="528f6-128">Name</span></span>                   | <span data-ttu-id="528f6-129">Typ</span><span class="sxs-lookup"><span data-stu-id="528f6-129">Type</span></span>     | <span data-ttu-id="528f6-130">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="528f6-130">Required</span></span> | <span data-ttu-id="528f6-131">Popis</span><span class="sxs-lookup"><span data-stu-id="528f6-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="528f6-132">Month (Měsíc)</span><span class="sxs-lookup"><span data-stu-id="528f6-132">Month</span></span>                      | <span data-ttu-id="528f6-133">řetězec</span><span class="sxs-lookup"><span data-stu-id="528f6-133">string</span></span>   | <span data-ttu-id="528f6-134">Yes</span><span class="sxs-lookup"><span data-stu-id="528f6-134">Yes</span></span>       | <span data-ttu-id="528f6-135">Musí být ve formátu YYYMM.</span><span class="sxs-lookup"><span data-stu-id="528f6-135">Must be in YYYMM format.</span></span> <span data-ttu-id="528f6-136">Je-li tento parametr vynechán, bude použita výchozí hodnota aktuální měsíc.</span><span class="sxs-lookup"><span data-stu-id="528f6-136">If omitted defaults to current month.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="528f6-137">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="528f6-137">Request headers</span></span>

- <span data-ttu-id="528f6-138">Další informace najdete v části [partner – záhlaví REST](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="528f6-138">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="528f6-139">Kromě výše uvedených hlaviček se soubory dají načíst jako komprimované zmenšení šířky pásma a časy stahování.</span><span class="sxs-lookup"><span data-stu-id="528f6-139">In addition to the above headers, files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="528f6-140">Ve výchozím nastavení nejsou soubory komprimovány.</span><span class="sxs-lookup"><span data-stu-id="528f6-140">By default the files are not compressed.</span></span> <span data-ttu-id="528f6-141">Chcete-li získat komprimované verze souborů, můžete zahrnout následující hodnotu záhlaví.</span><span class="sxs-lookup"><span data-stu-id="528f6-141">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="528f6-142">Mějte na paměti, že zkomprimované listy jsou k dispozici pouze od dubna 2020. všechny požadavky před dubna 2020 jsou k dispozici pouze jako nekomprimované.</span><span class="sxs-lookup"><span data-stu-id="528f6-142">Realize that compressed sheets are only available from April 2020 onward, all requests prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="528f6-143">Hlavička</span><span class="sxs-lookup"><span data-stu-id="528f6-143">Header</span></span>                   | <span data-ttu-id="528f6-144">Typ hodnoty</span><span class="sxs-lookup"><span data-stu-id="528f6-144">Value Type</span></span>     | <span data-ttu-id="528f6-145">Hodnota</span><span class="sxs-lookup"><span data-stu-id="528f6-145">Value</span></span> | <span data-ttu-id="528f6-146">Popis</span><span class="sxs-lookup"><span data-stu-id="528f6-146">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="528f6-147">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="528f6-147">Accept-Encoding</span></span>| <span data-ttu-id="528f6-148">řetězec</span><span class="sxs-lookup"><span data-stu-id="528f6-148">string</span></span>   | <span data-ttu-id="528f6-149">Deflate</span><span class="sxs-lookup"><span data-stu-id="528f6-149">deflate</span></span>| <span data-ttu-id="528f6-150">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="528f6-150">Optional.</span></span> <span data-ttu-id="528f6-151">Pokud se vynechaný datový proud souboru nekomprimuje</span><span class="sxs-lookup"><span data-stu-id="528f6-151">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="528f6-152">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="528f6-152">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="528f6-153">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="528f6-153">REST response</span></span>

<span data-ttu-id="528f6-154">V případě úspěchu tato metoda vrátí cizí kursy jako datový proud souboru.</span><span class="sxs-lookup"><span data-stu-id="528f6-154">If successful, this method returns foreign exchange rates as a file stream.</span></span> <span data-ttu-id="528f6-155">Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv.</span><span class="sxs-lookup"><span data-stu-id="528f6-155">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="528f6-156">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="528f6-156">Response success and error codes</span></span>

<span data-ttu-id="528f6-157">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="528f6-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="528f6-158">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="528f6-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="528f6-159">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="528f6-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="528f6-160">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="528f6-160">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```
