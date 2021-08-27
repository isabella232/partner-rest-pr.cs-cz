---
title: Získání ceníku
description: Získání ceníku pro daný trh a zobrazení Podporuje filtry pro získání historie podle měsíce.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0185a61ef0a3747aee1b06f88a7a8d6f1279f9e3
ms.sourcegitcommit: 1a183f9b37d646be240a48fc60e5902f409e8ac1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2021
ms.locfileid: "122989694"
---
# <a name="get-a-price-sheet"></a>Získání ceníku

Platí pro:

- Partner API

Toto téma vysvětluje, jak získat ceník pro daný trh a zobrazit ho. Tato metoda podporuje filtry pro získání historie podle měsíce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partner API ověřování.](api-authentication.md) Tento scénář podporuje pouze ověřování uživatelů aplikací. Pouze pro aplikace se zatím nepodporuje. Partneři, u které dojde **k chybě http:400,** by si měli Partner API [dokumentaci k ověřování.](api-authentication.md)
- Toto rozhraní API v současné době podporuje pouze uživatelský přístup, kde partneři musí mít jednu z následujících rolí: globální správce, agent pro správu nebo prodejní agent.

## <a name="details"></a>Podrobnosti

- Aktuální vrátí data pouze pro produkty spotřeby plánu Azure a rezervací.
- Aktuální [ceny](pricing.md) zahrnují všechny měřiče a produkty dostupné v aktuálním měsíci do data volání rozhraní API. Předchozí měsíce zahrnují všechny měřiče a produkty dostupné pro daný měsíc.
- Ceny měřičů spotřeby jsou jenom v USD, partneři k výpočtu nákladů na místní měnu používají rozhraní API pro směnné kurzy.
- Ceny měřičů spotřeby jsou odhadované maloobchodní ceny. Slevy partnerů jsou k dispozici prostřednictvím [kreditu získaného partnerem.](/partner-center/partner-earned-credit-explanation)
- Ceny měřičů rezervací zahrnují slevy partnera CSP. Odhadované maloobchodní ceny rezervací najdete ve sdílených službách rezervací ke stažení na Partnerské centrum stránce Ceny a nabídky.
- Další informace o cenách plánu Azure najdete v dokumentaci k cenám [plánu Azure.](/partner-center/azure-plan-price-list)
- Ceny partnerů a rozhraní API pro cizí směnné sazby nejsou součástí SDK pro Partnerské centrum [.](get-started.md)
- Tato metoda vrátí ceník jako datový proud souboru. Stream souboru je buď .csv soubor, nebo komprimovaná verze souboru .csv. Podrobnosti o tom, jak požádat o komprimované soubory, jsou uvedené níže.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **DOSTAT** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value                                     |

### <a name="uri-required-parameters"></a>Požadované parametry identifikátoru URI

Pomocí následujících parametrů cesty můžete vyžádat, který trh a typ ceníku chcete.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Trhu                      | řetězec   | Yes       | Dvou písmeno kódu země pro požadovaný trh       |
|PricesheetView | řetězec   | Yes       | Typ požadovaného ceníku, který je možné azure_consumption, azure_reservations nebo aktualizovanýlicence.  |

> [!Note]
> updatedlicensebased PriceSheetView je v současné době k dispozici pouze pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.

### <a name="uri-filter-parameters"></a>Parametry filtru identifikátorů URI

Použijte následující parametry filtru.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Časová osa| řetězec   | No| Výchozí hodnota je aktuální, pokud není předána. Možné hodnoty jsou historie, aktuální a budoucí.       |
|Month (Měsíc)| řetězec   | No| Vyžaduje se jenom v případě, že se vyžaduje historie, musí se v požadovaném ceníku řídit YYYYMM.       |

### <a name="request-headers"></a>Hlavičky požadavku

- Další [informace najdete v tématu Hlavičky REST](headers.md) pro partnery.

Kromě výše uvedených hlaviček je možné soubory s cenami načíst jako komprimované, což snižuje šířku pásma a dobu stahování. Ve výchozím nastavení nejsou soubory komprimované. Pokud chcete získat komprimované verze souborů, můžete zahrnout následující hodnotu hlavičky. Uvědomte si, že komprimované listy jsou k dispozici pouze od dubna 2020, ale všechny listy před dubnem 2020 jsou dostupné pouze jako komprimované.

| Hlavička                   | Typ hodnoty     | Hodnota | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| řetězec   | Deflaci| Nepovinný parametr. Pokud je vynechán datový proud souboru není komprimován.       |

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a>Příklad žádosti o nové obchodování

> [!Note]
> updatedlicensebased PriceSheetView je v současné době k dispozici pouze pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda ceník jako datový proud souboru. Stream souboru je buď .csv soubor, nebo komprimovaná verze souboru .csv.

### <a name="response-example-for-new-commerce"></a>Příklad odpovědi pro nové obchodování

> [!Note]
> updatedlicensebased PriceSheetView je v současné době k dispozici pouze pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.

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

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)
