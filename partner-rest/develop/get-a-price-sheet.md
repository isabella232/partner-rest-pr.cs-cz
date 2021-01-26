---
title: Získání ceníku
description: Získání ceníku pro daný trh a zobrazení. Podporuje filtry k získání historie podle měsíců.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5195ebed6559bd71a7832a667e63ee801be1c82f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770352"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="20d51-104">Získání ceníku</span><span class="sxs-lookup"><span data-stu-id="20d51-104">Get a price sheet</span></span>

<span data-ttu-id="20d51-105">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="20d51-105">Applies to:</span></span>

- <span data-ttu-id="20d51-106">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="20d51-106">Partner API</span></span>

<span data-ttu-id="20d51-107">Toto téma vysvětluje, jak získat ceník pro daný trh a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="20d51-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="20d51-108">Tato metoda podporuje filtry k získání historie podle měsíců.</span><span class="sxs-lookup"><span data-stu-id="20d51-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20d51-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="20d51-109">Prerequisites</span></span>

- <span data-ttu-id="20d51-110">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="20d51-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="20d51-111">Tento scénář podporuje pouze ověření uživatele aplikace.</span><span class="sxs-lookup"><span data-stu-id="20d51-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="20d51-112">Application-ony ještě není podporovaná.</span><span class="sxs-lookup"><span data-stu-id="20d51-112">Application-ony is not yet supported.</span></span>
- <span data-ttu-id="20d51-113">Toto rozhraní API aktuálně podporuje jenom přístup uživatelů, kde se partneři musí nacházet v jedné z následujících rolí: globální správce, agent pro správu nebo agent pro prodej.</span><span class="sxs-lookup"><span data-stu-id="20d51-113">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="20d51-114">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="20d51-114">Details</span></span>

- <span data-ttu-id="20d51-115">Aktuální vrátí data jenom pro využití Azure plánů a rezervované produkty.</span><span class="sxs-lookup"><span data-stu-id="20d51-115">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="20d51-116">Aktuální [Cena](pricing.md) zahrnuje všechny měřiče a produkty dostupné během aktuálního měsíce k datu, kdy se rozhraní API volá.</span><span class="sxs-lookup"><span data-stu-id="20d51-116">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="20d51-117">Předchozí měsíce zahrnují všechny měřiče a produkty, které jsou k dispozici pro daný měsíc.</span><span class="sxs-lookup"><span data-stu-id="20d51-117">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="20d51-118">Ceny měření spotřeby se účtují jenom v USD, partneři mají k výpočtu nákladů na místní měnu použít rozhraní API pro cizí kursy.</span><span class="sxs-lookup"><span data-stu-id="20d51-118">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="20d51-119">Ceny za měřič spotřeby jsou odhadované maloobchodní ceny.</span><span class="sxs-lookup"><span data-stu-id="20d51-119">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="20d51-120">Slevy za partnery jsou dostupné prostřednictvím [realizovaného kreditu](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span><span class="sxs-lookup"><span data-stu-id="20d51-120">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="20d51-121">Ceny za měřič rezervací zahrnují slevy partnera CSP.</span><span class="sxs-lookup"><span data-stu-id="20d51-121">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="20d51-122">Odhadované maloobchodní ceny rezervací najdete na stránce ceny a nabídky partnerského centra ke stažení na základě rezervací sdílených služeb.</span><span class="sxs-lookup"><span data-stu-id="20d51-122">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="20d51-123">Další informace o cenách plánu Azure najdete v [dokumentaci k ceníkům Azure Plan](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="20d51-123">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="20d51-124">Ceny partnerů a rozhraní API pro cizí kurz nejsou součástí [sady SDK partnerského centra](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="20d51-124">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="20d51-125">Tato metoda vrátí Ceník jako datový proud souboru.</span><span class="sxs-lookup"><span data-stu-id="20d51-125">This method returns the price list as a file stream.</span></span> <span data-ttu-id="20d51-126">Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv.</span><span class="sxs-lookup"><span data-stu-id="20d51-126">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="20d51-127">Podrobnosti o tom, jak vyžádat komprimované soubory, jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="20d51-127">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="20d51-128">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="20d51-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="20d51-129">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="20d51-129">Request syntax</span></span>

| <span data-ttu-id="20d51-130">Metoda</span><span class="sxs-lookup"><span data-stu-id="20d51-130">Method</span></span>   | <span data-ttu-id="20d51-131">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="20d51-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="20d51-132">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="20d51-132">**GET**</span></span> | <span data-ttu-id="20d51-133"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={Market}, PricesheetView = {View})/$value</span><span class="sxs-lookup"><span data-stu-id="20d51-133">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="20d51-134">Parametry vyžadované identifikátorem URI</span><span class="sxs-lookup"><span data-stu-id="20d51-134">URI required parameters</span></span>

<span data-ttu-id="20d51-135">Pomocí následujících parametrů cesty si vyžádejte, který trh a typ ceníku potřebujete.</span><span class="sxs-lookup"><span data-stu-id="20d51-135">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="20d51-136">Název</span><span class="sxs-lookup"><span data-stu-id="20d51-136">Name</span></span>                   | <span data-ttu-id="20d51-137">Typ</span><span class="sxs-lookup"><span data-stu-id="20d51-137">Type</span></span>     | <span data-ttu-id="20d51-138">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="20d51-138">Required</span></span> | <span data-ttu-id="20d51-139">Popis</span><span class="sxs-lookup"><span data-stu-id="20d51-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="20d51-140">Uvádět</span><span class="sxs-lookup"><span data-stu-id="20d51-140">Market</span></span>                      | <span data-ttu-id="20d51-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="20d51-141">string</span></span>   | <span data-ttu-id="20d51-142">Yes</span><span class="sxs-lookup"><span data-stu-id="20d51-142">Yes</span></span>       | <span data-ttu-id="20d51-143">Pro požadovaný trh se dvěma písmeny kódu země</span><span class="sxs-lookup"><span data-stu-id="20d51-143">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="20d51-144">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="20d51-144">PricesheetView</span></span> | <span data-ttu-id="20d51-145">řetězec</span><span class="sxs-lookup"><span data-stu-id="20d51-145">string</span></span>   | <span data-ttu-id="20d51-146">Yes</span><span class="sxs-lookup"><span data-stu-id="20d51-146">Yes</span></span>       | <span data-ttu-id="20d51-147">Typ požadovaného ceníku, který je možné azure_consumption nebo azure_reservations</span><span class="sxs-lookup"><span data-stu-id="20d51-147">The type of price sheet being requested, this can be azure_consumption or azure_reservations</span></span>       |

### <a name="uri-filter-parameters"></a><span data-ttu-id="20d51-148">Parametry filtru identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="20d51-148">URI filter parameters</span></span>

<span data-ttu-id="20d51-149">Použijte následující parametry filtru.</span><span class="sxs-lookup"><span data-stu-id="20d51-149">Use the following filter parameters.</span></span>

| <span data-ttu-id="20d51-150">Název</span><span class="sxs-lookup"><span data-stu-id="20d51-150">Name</span></span>                   | <span data-ttu-id="20d51-151">Typ</span><span class="sxs-lookup"><span data-stu-id="20d51-151">Type</span></span>     | <span data-ttu-id="20d51-152">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="20d51-152">Required</span></span> | <span data-ttu-id="20d51-153">Popis</span><span class="sxs-lookup"><span data-stu-id="20d51-153">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="20d51-154">Časová osa</span><span class="sxs-lookup"><span data-stu-id="20d51-154">Timeline</span></span>| <span data-ttu-id="20d51-155">řetězec</span><span class="sxs-lookup"><span data-stu-id="20d51-155">string</span></span>   | <span data-ttu-id="20d51-156">No</span><span class="sxs-lookup"><span data-stu-id="20d51-156">No</span></span>| <span data-ttu-id="20d51-157">Výchozí hodnota je Current, pokud nebyla předána.</span><span class="sxs-lookup"><span data-stu-id="20d51-157">Defaults to current if not passed.</span></span> <span data-ttu-id="20d51-158">Možné hodnoty jsou historická, aktuální a budoucí.</span><span class="sxs-lookup"><span data-stu-id="20d51-158">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="20d51-159">Month (Měsíc)</span><span class="sxs-lookup"><span data-stu-id="20d51-159">Month</span></span>| <span data-ttu-id="20d51-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="20d51-160">string</span></span>   | <span data-ttu-id="20d51-161">No</span><span class="sxs-lookup"><span data-stu-id="20d51-161">No</span></span>| <span data-ttu-id="20d51-162">Vyžaduje se pouze v případě, že je požadována historie, musí dodržovat YYYYMM pro požadovaný ceník.</span><span class="sxs-lookup"><span data-stu-id="20d51-162">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="20d51-163">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="20d51-163">Request headers</span></span>

- <span data-ttu-id="20d51-164">Další informace najdete v části [partner – záhlaví REST](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="20d51-164">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="20d51-165">Kromě výše uvedených hlaviček je možné soubory s cenami načíst jako komprimovaný způsob zmenšení šířky pásma a doby stahování.</span><span class="sxs-lookup"><span data-stu-id="20d51-165">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="20d51-166">Ve výchozím nastavení nejsou soubory komprimovány.</span><span class="sxs-lookup"><span data-stu-id="20d51-166">By default the files are not compressed.</span></span> <span data-ttu-id="20d51-167">Chcete-li získat komprimované verze souborů, můžete zahrnout následující hodnotu záhlaví.</span><span class="sxs-lookup"><span data-stu-id="20d51-167">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="20d51-168">Mějte na paměti, že zkomprimované listy jsou k dispozici pouze od dubna 2020. všechny listy starší než 2020. dubna jsou k dispozici pouze jako nekomprimované.</span><span class="sxs-lookup"><span data-stu-id="20d51-168">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="20d51-169">Hlavička</span><span class="sxs-lookup"><span data-stu-id="20d51-169">Header</span></span>                   | <span data-ttu-id="20d51-170">Typ hodnoty</span><span class="sxs-lookup"><span data-stu-id="20d51-170">Value Type</span></span>     | <span data-ttu-id="20d51-171">Hodnota</span><span class="sxs-lookup"><span data-stu-id="20d51-171">Value</span></span> | <span data-ttu-id="20d51-172">Popis</span><span class="sxs-lookup"><span data-stu-id="20d51-172">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="20d51-173">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="20d51-173">Accept-Encoding</span></span>| <span data-ttu-id="20d51-174">řetězec</span><span class="sxs-lookup"><span data-stu-id="20d51-174">string</span></span>   | <span data-ttu-id="20d51-175">Deflate</span><span class="sxs-lookup"><span data-stu-id="20d51-175">deflate</span></span>| <span data-ttu-id="20d51-176">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="20d51-176">Optional.</span></span> <span data-ttu-id="20d51-177">Pokud se vynechaný datový proud souboru nekomprimuje</span><span class="sxs-lookup"><span data-stu-id="20d51-177">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="20d51-178">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="20d51-178">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="20d51-179">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="20d51-179">REST response</span></span>

<span data-ttu-id="20d51-180">V případě úspěchu vrátí tato metoda Ceník jako datový proud souboru.</span><span class="sxs-lookup"><span data-stu-id="20d51-180">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="20d51-181">Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv.</span><span class="sxs-lookup"><span data-stu-id="20d51-181">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="20d51-182">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="20d51-182">Response success and error codes</span></span>

<span data-ttu-id="20d51-183">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="20d51-183">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="20d51-184">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="20d51-184">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="20d51-185">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="20d51-185">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="20d51-186">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="20d51-186">Response example</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```
