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
# <a name="get-foreign-exchange-rates"></a>Získání směnných kurzů

Platí pro:

- Partnerské rozhraní API

Toto téma vysvětluje, jak získat směnné sazby za daný měsíc.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md). Tento scénář podporuje pouze ověření uživatele aplikace. Pouze aplikace není zatím podporována.
- Toto rozhraní API aktuálně podporuje jenom přístup uživatelů, kde se partneři musí nacházet v jedné z následujících rolí: globální správce, agent pro správu nebo agent pro prodej.


## <a name="details"></a>Podrobnosti

- V současné době se používá s funkcí [získat cenové ceníek](get-a-price-sheet.md) k výpočtu očekávaných poplatků za místní měny Azure Plan CSP.
- Sazby za cizí směnky budou platit pro celý měsíc, který je publikovaná.
- Další informace o [cenách](pricing.md) plánu Azure najdete v [dokumentaci k ceníkům Azure Plan](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- Ceny partnerů a rozhraní API pro cizí kurz nejsou součástí [sady SDK partnerského centra](https://docs.microsoft.com/partner-center/develop/get-started).
- Tato metoda vrací výsledky jako datový proud souboru. Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv. Podrobnosti o tom, jak vyžádat komprimované soubory, jsou uvedené níže.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Čtěte** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month={month})/$value                                  |

### <a name="uri-required-parameters"></a>Parametry vyžadované identifikátorem URI

Použijte následující parametry cesty, abyste si vyžádali měsíc cizích devizových sazeb, které chcete.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Month (Měsíc)                      | řetězec   | Yes       | Musí být ve formátu YYYMM. Je-li tento parametr vynechán, bude použita výchozí hodnota aktuální měsíc.       |

### <a name="request-headers"></a>Hlavičky požadavku

- Další informace najdete v části [partner – záhlaví REST](headers.md) .

Kromě výše uvedených hlaviček se soubory dají načíst jako komprimované zmenšení šířky pásma a časy stahování. Ve výchozím nastavení nejsou soubory komprimovány. Chcete-li získat komprimované verze souborů, můžete zahrnout následující hodnotu záhlaví. Mějte na paměti, že zkomprimované listy jsou k dispozici pouze od dubna 2020. všechny požadavky před dubna 2020 jsou k dispozici pouze jako nekomprimované.

| Hlavička                   | Typ hodnoty     | Hodnota | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| řetězec   | Deflate| Nepovinný parametr. Pokud se vynechaný datový proud souboru nekomprimuje       |

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí cizí kursy jako datový proud souboru. Datový proud souborů je soubor. csv nebo komprimovaná verze souboru. csv.

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

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
