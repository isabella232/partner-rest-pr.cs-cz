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
# <a name="get-a-price-sheet"></a>Získání ceníku

Platí pro:

- Partnerské rozhraní API

Toto téma vysvětluje, jak získat ceník pro daný trh a zobrazení. Tato metoda podporuje filtry k získání historie podle měsíců.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md). Tento scénář podporuje pouze ověření uživatele aplikace. Application-ony ještě není podporovaná.
- Toto rozhraní API aktuálně podporuje jenom přístup uživatelů, kde se partneři musí nacházet v jedné z následujících rolí: globální správce, agent pro správu nebo agent pro prodej.

## <a name="details"></a>Podrobnosti

- Aktuální vrátí data jenom pro využití Azure plánů a rezervované produkty.
- Aktuální [Cena](pricing.md) zahrnuje všechny měřiče a produkty dostupné během aktuálního měsíce k datu, kdy se rozhraní API volá. Předchozí měsíce zahrnují všechny měřiče a produkty, které jsou k dispozici pro daný měsíc.
- Ceny měření spotřeby se účtují jenom v USD, partneři mají k výpočtu nákladů na místní měnu použít rozhraní API pro cizí kursy.
- Ceny za měřič spotřeby jsou odhadované maloobchodní ceny. Slevy za partnery jsou dostupné prostřednictvím [realizovaného kreditu](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).
- Ceny za měřič rezervací zahrnují slevy partnera CSP. Odhadované maloobchodní ceny rezervací najdete na stránce ceny a nabídky partnerského centra ke stažení na základě rezervací sdílených služeb.
- Další informace o cenách plánu Azure najdete v [dokumentaci k ceníkům Azure Plan](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- Ceny partnerů a rozhraní API pro cizí kurz nejsou součástí [sady SDK partnerského centra](https://docs.microsoft.com/partner-center/develop/get-started).
- Tato metoda vrátí Ceník jako datový proud souboru. Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv. Podrobnosti o tom, jak vyžádat komprimované soubory, jsou uvedené níže.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Čtěte** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={Market}, PricesheetView = {View})/$value                                     |

### <a name="uri-required-parameters"></a>Parametry vyžadované identifikátorem URI

Pomocí následujících parametrů cesty si vyžádejte, který trh a typ ceníku potřebujete.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Uvádět                      | řetězec   | Yes       | Pro požadovaný trh se dvěma písmeny kódu země       |
|PricesheetView | řetězec   | Yes       | Typ požadovaného ceníku, který je možné azure_consumption nebo azure_reservations       |

### <a name="uri-filter-parameters"></a>Parametry filtru identifikátoru URI

Použijte následující parametry filtru.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Časová osa| řetězec   | No| Výchozí hodnota je Current, pokud nebyla předána. Možné hodnoty jsou historická, aktuální a budoucí.       |
|Month (Měsíc)| řetězec   | No| Vyžaduje se pouze v případě, že je požadována historie, musí dodržovat YYYYMM pro požadovaný ceník.       |

### <a name="request-headers"></a>Hlavičky požadavku

- Další informace najdete v části [partner – záhlaví REST](headers.md) .

Kromě výše uvedených hlaviček je možné soubory s cenami načíst jako komprimovaný způsob zmenšení šířky pásma a doby stahování. Ve výchozím nastavení nejsou soubory komprimovány. Chcete-li získat komprimované verze souborů, můžete zahrnout následující hodnotu záhlaví. Mějte na paměti, že zkomprimované listy jsou k dispozici pouze od dubna 2020. všechny listy starší než 2020. dubna jsou k dispozici pouze jako nekomprimované.

| Hlavička                   | Typ hodnoty     | Hodnota | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| řetězec   | Deflate| Nepovinný parametr. Pokud se vynechaný datový proud souboru nekomprimuje       |

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda Ceník jako datový proud souboru. Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

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
