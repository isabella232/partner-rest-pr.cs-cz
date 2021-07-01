---
title: Získání ceníku
description: Získání ceníku pro daný trh a zobrazení. Podporuje filtry k získání historie podle měsíců.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7571e8fce861dbfe463000a1ac4094115af08ffa
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2021
ms.locfileid: "113125512"
---
# <a name="get-a-price-sheet"></a><span data-ttu-id="98726-104">Získání ceníku</span><span class="sxs-lookup"><span data-stu-id="98726-104">Get a price sheet</span></span>

<span data-ttu-id="98726-105">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="98726-105">Applies to:</span></span>

- <span data-ttu-id="98726-106">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="98726-106">Partner API</span></span>

<span data-ttu-id="98726-107">Toto téma vysvětluje, jak získat ceník pro daný trh a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="98726-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="98726-108">Tato metoda podporuje filtry k získání historie podle měsíců.</span><span class="sxs-lookup"><span data-stu-id="98726-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98726-109">Požadavky</span><span class="sxs-lookup"><span data-stu-id="98726-109">Prerequisites</span></span>

- <span data-ttu-id="98726-110">Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="98726-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="98726-111">Tento scénář podporuje pouze ověření uživatele aplikace.</span><span class="sxs-lookup"><span data-stu-id="98726-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="98726-112">Pouze aplikace není zatím podporována.</span><span class="sxs-lookup"><span data-stu-id="98726-112">Application-only is not yet supported.</span></span> <span data-ttu-id="98726-113">Partneři, kteří mají zkušenosti s **chybou http: 400** , by si měli v dokumentaci k [ověřování rozhraní API partnerů](api-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="98726-113">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="98726-114">Toto rozhraní API aktuálně podporuje jenom přístup uživatelů, kde se partneři musí nacházet v jedné z následujících rolí: globální správce, agent pro správu nebo agent pro prodej.</span><span class="sxs-lookup"><span data-stu-id="98726-114">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="98726-115">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="98726-115">Details</span></span>

- <span data-ttu-id="98726-116">Aktuální vrátí data jenom pro využití Azure plánů a rezervované produkty.</span><span class="sxs-lookup"><span data-stu-id="98726-116">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="98726-117">Aktuální [Cena](pricing.md) zahrnuje všechny měřiče a produkty dostupné během aktuálního měsíce k datu, kdy se rozhraní API volá.</span><span class="sxs-lookup"><span data-stu-id="98726-117">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="98726-118">Předchozí měsíce zahrnují všechny měřiče a produkty, které jsou k dispozici pro daný měsíc.</span><span class="sxs-lookup"><span data-stu-id="98726-118">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="98726-119">Ceny měření spotřeby se účtují jenom v USD, partneři mají k výpočtu nákladů na místní měnu použít rozhraní API pro cizí kursy.</span><span class="sxs-lookup"><span data-stu-id="98726-119">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="98726-120">Ceny za měřič spotřeby jsou odhadované maloobchodní ceny.</span><span class="sxs-lookup"><span data-stu-id="98726-120">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="98726-121">Slevy za partnery jsou dostupné prostřednictvím [realizovaného kreditu](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span><span class="sxs-lookup"><span data-stu-id="98726-121">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="98726-122">Ceny za měřič rezervací zahrnují slevy partnera CSP.</span><span class="sxs-lookup"><span data-stu-id="98726-122">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="98726-123">Odhadované maloobchodní ceny rezervací najdete na stránce ceny a nabídky partnerského centra ke stažení na základě rezervací sdílených služeb.</span><span class="sxs-lookup"><span data-stu-id="98726-123">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="98726-124">Další informace o cenách plánu Azure najdete v [dokumentaci k ceníkům Azure Plan](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="98726-124">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="98726-125">Ceny partnerů a rozhraní API pro cizí kurz nejsou součástí [sady SDK partnerského centra](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="98726-125">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="98726-126">Tato metoda vrátí Ceník jako datový proud souboru.</span><span class="sxs-lookup"><span data-stu-id="98726-126">This method returns the price list as a file stream.</span></span> <span data-ttu-id="98726-127">Datový proud souboru je .csv soubor nebo zip komprimovaná verze .csv.</span><span class="sxs-lookup"><span data-stu-id="98726-127">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="98726-128">Podrobnosti o tom, jak vyžádat komprimované soubory, jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="98726-128">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="98726-129">Žádost REST</span><span class="sxs-lookup"><span data-stu-id="98726-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="98726-130">Syntaxe žádosti</span><span class="sxs-lookup"><span data-stu-id="98726-130">Request syntax</span></span>

| <span data-ttu-id="98726-131">Metoda</span><span class="sxs-lookup"><span data-stu-id="98726-131">Method</span></span>   | <span data-ttu-id="98726-132">Identifikátor URI žádosti</span><span class="sxs-lookup"><span data-stu-id="98726-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="98726-133">**Čtěte**</span><span class="sxs-lookup"><span data-stu-id="98726-133">**GET**</span></span> | <span data-ttu-id="98726-134"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={Market}, PricesheetView = {View})/$value</span><span class="sxs-lookup"><span data-stu-id="98726-134">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="98726-135">Parametry vyžadované identifikátorem URI</span><span class="sxs-lookup"><span data-stu-id="98726-135">URI required parameters</span></span>

<span data-ttu-id="98726-136">Pomocí následujících parametrů cesty si vyžádejte, který trh a typ ceníku potřebujete.</span><span class="sxs-lookup"><span data-stu-id="98726-136">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="98726-137">Název</span><span class="sxs-lookup"><span data-stu-id="98726-137">Name</span></span>                   | <span data-ttu-id="98726-138">Typ</span><span class="sxs-lookup"><span data-stu-id="98726-138">Type</span></span>     | <span data-ttu-id="98726-139">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="98726-139">Required</span></span> | <span data-ttu-id="98726-140">Popis</span><span class="sxs-lookup"><span data-stu-id="98726-140">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="98726-141">Uvádět</span><span class="sxs-lookup"><span data-stu-id="98726-141">Market</span></span>                      | <span data-ttu-id="98726-142">řetězec</span><span class="sxs-lookup"><span data-stu-id="98726-142">string</span></span>   | <span data-ttu-id="98726-143">Yes</span><span class="sxs-lookup"><span data-stu-id="98726-143">Yes</span></span>       | <span data-ttu-id="98726-144">Pro požadovaný trh se dvěma písmeny kódu země</span><span class="sxs-lookup"><span data-stu-id="98726-144">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="98726-145">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="98726-145">PricesheetView</span></span> | <span data-ttu-id="98726-146">řetězec</span><span class="sxs-lookup"><span data-stu-id="98726-146">string</span></span>   | <span data-ttu-id="98726-147">Yes</span><span class="sxs-lookup"><span data-stu-id="98726-147">Yes</span></span>       | <span data-ttu-id="98726-148">Typ požadovaného ceníku, který lze azure_consumption, azure_reservations nebo updatedlicensebased.</span><span class="sxs-lookup"><span data-stu-id="98726-148">The type of price sheet being requested, this can be azure_consumption, azure_reservations or updatedlicensebased.</span></span>  |

> [!Note]
> <span data-ttu-id="98726-149">updatedlicensebased PriceSheetView je teď k dispozici jenom pro partnery, kteří jsou součástí M365/D365 nové obchodní zkušenosti Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="98726-149">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

### <a name="uri-filter-parameters"></a><span data-ttu-id="98726-150">Parametry filtru identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="98726-150">URI filter parameters</span></span>

<span data-ttu-id="98726-151">Použijte následující parametry filtru.</span><span class="sxs-lookup"><span data-stu-id="98726-151">Use the following filter parameters.</span></span>

| <span data-ttu-id="98726-152">Název</span><span class="sxs-lookup"><span data-stu-id="98726-152">Name</span></span>                   | <span data-ttu-id="98726-153">Typ</span><span class="sxs-lookup"><span data-stu-id="98726-153">Type</span></span>     | <span data-ttu-id="98726-154">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="98726-154">Required</span></span> | <span data-ttu-id="98726-155">Popis</span><span class="sxs-lookup"><span data-stu-id="98726-155">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="98726-156">Časová osa</span><span class="sxs-lookup"><span data-stu-id="98726-156">Timeline</span></span>| <span data-ttu-id="98726-157">řetězec</span><span class="sxs-lookup"><span data-stu-id="98726-157">string</span></span>   | <span data-ttu-id="98726-158">No</span><span class="sxs-lookup"><span data-stu-id="98726-158">No</span></span>| <span data-ttu-id="98726-159">Výchozí hodnota je Current, pokud nebyla předána.</span><span class="sxs-lookup"><span data-stu-id="98726-159">Defaults to current if not passed.</span></span> <span data-ttu-id="98726-160">Možné hodnoty jsou historická, aktuální a budoucí.</span><span class="sxs-lookup"><span data-stu-id="98726-160">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="98726-161">Month (Měsíc)</span><span class="sxs-lookup"><span data-stu-id="98726-161">Month</span></span>| <span data-ttu-id="98726-162">řetězec</span><span class="sxs-lookup"><span data-stu-id="98726-162">string</span></span>   | <span data-ttu-id="98726-163">No</span><span class="sxs-lookup"><span data-stu-id="98726-163">No</span></span>| <span data-ttu-id="98726-164">Vyžaduje se pouze v případě, že je požadována historie, musí dodržovat YYYYMM pro požadovaný ceník.</span><span class="sxs-lookup"><span data-stu-id="98726-164">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="98726-165">Hlavičky požadavku</span><span class="sxs-lookup"><span data-stu-id="98726-165">Request headers</span></span>

- <span data-ttu-id="98726-166">Další informace najdete v části [partner – záhlaví REST](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="98726-166">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="98726-167">Kromě výše uvedených hlaviček je možné soubory s cenami načíst jako komprimovaný způsob zmenšení šířky pásma a doby stahování.</span><span class="sxs-lookup"><span data-stu-id="98726-167">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="98726-168">Ve výchozím nastavení nejsou soubory komprimovány.</span><span class="sxs-lookup"><span data-stu-id="98726-168">By default the files are not compressed.</span></span> <span data-ttu-id="98726-169">Chcete-li získat komprimované verze souborů, můžete zahrnout následující hodnotu záhlaví.</span><span class="sxs-lookup"><span data-stu-id="98726-169">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="98726-170">Mějte na paměti, že zkomprimované listy jsou k dispozici pouze od dubna 2020. všechny listy starší než 2020. dubna jsou k dispozici pouze jako nekomprimované.</span><span class="sxs-lookup"><span data-stu-id="98726-170">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="98726-171">Hlavička</span><span class="sxs-lookup"><span data-stu-id="98726-171">Header</span></span>                   | <span data-ttu-id="98726-172">Typ hodnoty</span><span class="sxs-lookup"><span data-stu-id="98726-172">Value Type</span></span>     | <span data-ttu-id="98726-173">Hodnota</span><span class="sxs-lookup"><span data-stu-id="98726-173">Value</span></span> | <span data-ttu-id="98726-174">Popis</span><span class="sxs-lookup"><span data-stu-id="98726-174">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="98726-175">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="98726-175">Accept-Encoding</span></span>| <span data-ttu-id="98726-176">řetězec</span><span class="sxs-lookup"><span data-stu-id="98726-176">string</span></span>   | <span data-ttu-id="98726-177">Deflate</span><span class="sxs-lookup"><span data-stu-id="98726-177">deflate</span></span>| <span data-ttu-id="98726-178">Nepovinný parametr.</span><span class="sxs-lookup"><span data-stu-id="98726-178">Optional.</span></span> <span data-ttu-id="98726-179">Pokud se vynechaný datový proud souboru nekomprimuje</span><span class="sxs-lookup"><span data-stu-id="98726-179">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="98726-180">Příklad požadavku</span><span class="sxs-lookup"><span data-stu-id="98726-180">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a><span data-ttu-id="98726-181">Příklad žádosti o nový obchod</span><span class="sxs-lookup"><span data-stu-id="98726-181">Request example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="98726-182">updatedlicensebased PriceSheetView je teď k dispozici jenom pro partnery, kteří jsou součástí M365/D365 nové obchodní zkušenosti Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="98726-182">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="98726-183">Odpověď REST</span><span class="sxs-lookup"><span data-stu-id="98726-183">REST response</span></span>

<span data-ttu-id="98726-184">V případě úspěchu vrátí tato metoda Ceník jako datový proud souboru.</span><span class="sxs-lookup"><span data-stu-id="98726-184">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="98726-185">Datový proud souboru je .csv soubor nebo zip komprimovaná verze .csv.</span><span class="sxs-lookup"><span data-stu-id="98726-185">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="98726-186">Úspěšné odpovědi a chybové kódy</span><span class="sxs-lookup"><span data-stu-id="98726-186">Response success and error codes</span></span>

<span data-ttu-id="98726-187">Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění.</span><span class="sxs-lookup"><span data-stu-id="98726-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="98726-188">Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.</span><span class="sxs-lookup"><span data-stu-id="98726-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="98726-189">Úplný seznam najdete v tématu [kódy chyb](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="98726-189">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="98726-190">Příklad odpovědi</span><span class="sxs-lookup"><span data-stu-id="98726-190">Response example</span></span>

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

### <a name="response-example-for-new-commerce"></a><span data-ttu-id="98726-191">Příklad odpovědi pro nový obchod</span><span class="sxs-lookup"><span data-stu-id="98726-191">Response example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="98726-192">updatedlicensebased PriceSheetView je teď k dispozici jenom pro partnery, kteří jsou součástí M365/D365 nové obchodní zkušenosti Technical Preview.</span><span class="sxs-lookup"><span data-stu-id="98726-192">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```
