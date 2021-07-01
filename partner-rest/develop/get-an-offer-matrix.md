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
# <a name="get-an-offer-matrix"></a>Získání matice nabídek

Platí pro:

- Partner API
- Prostředí M365/D365 New Commerce technical preview. Níže uvedené změny v novém obchodování jsou aktuálně dostupné jenom pro partnery, kteří jsou součástí nového komerčního prostředí M365/D365 technical preview.

Toto téma vysvětluje, jak získat matici nabídek pro daný měsíc. Matice nabídek obsahuje vlastnosti a pravidla nákupu produktů a SKU. Tato metoda podporuje filtry pro získání historie podle měsíce.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje, jak je [popsáno Partner API ověřování.](api-authentication.md) Tento scénář podporuje pouze ověřování uživatelů aplikací. Pouze pro aplikace se zatím nepodporuje. Partneři, u které dojde **k chybě http:400,** by si měli Partner API [dokumentaci k ověřování.](api-authentication.md)
- Toto rozhraní API v současné době podporuje pouze uživatelský přístup, kde partneři musí mít jednu z následujících rolí: globální správce, agent pro správu nebo prodejní agent.

## <a name="details"></a>Podrobnosti

- Funkce Current vrací data pouze pro aktualizované nové komerční produkty založené na licencích.
- Aktuální ceny zahrnují produkty dostupné v aktuálním měsíci do data volání rozhraní API. Předchozí měsíce zahrnují datum k poslednímu dni vybraného měsíce.
- Tato metoda vrátí data jako datový proud souboru. Stream souboru je buď .csv soubor, nebo komprimovaná verze souboru .csv. Podrobnosti o tom, jak požádat o komprimované soubory, jsou uvedené níže.

## <a name="rest-request"></a>Požadavek REST

### <a name="request-syntax"></a>Syntaxe požadavku

| Metoda   | Identifikátor URI žádosti                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Dostat** | https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month={date})/$value |

### <a name="uri-filter-parameters"></a>Parametry filtru identifikátorů URI

Použijte následující parametry filtru.

| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Month (Měsíc)| řetězec   | No | Musí splňovat YYYYMM pro požadovaný ceník. |

### <a name="request-headers"></a>Hlavičky požadavku

- Další [informace najdete v tématu Hlavičky REST](headers.md) pro partnery.

Kromě výše uvedených hlaviček je možné soubory s cenami načíst jako komprimované, což snižuje šířku pásma a dobu stahování. Ve výchozím nastavení nejsou soubory komprimované. Pokud chcete získat komprimované verze souborů, můžete zahrnout následující hodnotu hlavičky. Uvědomte si, že komprimované listy jsou k dispozici pouze od dubna 2020, ale všechny listy před dubnem 2020 jsou k dispozici pouze jako komprimované.

| Hlavička                   | Typ hodnoty     | Hodnota | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| řetězec   | Deflaci| Nepovinný parametr. Pokud je vynechán datový proud souboru není komprimován.       |

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu tato metoda vrátí matici nabídek jako stream souboru. Stream souboru je buď .csv soubor, nebo komprimovaná verze souboru .csv.

### <a name="response-success-and-error-codes"></a>Kódy chyb a úspěšné odpovědi

Každá odpověď má stavový kód HTTP, který indikuje úspěch nebo neúspěch a další informace o ladění. K přečtení tohoto kódu, typu chyby a dalších parametrů použijte nástroj pro trasování sítě. Úplný seznam najdete v tématu [Kódy chyb.](error-codes.md)

### <a name="response-example"></a>Příklad odpovědi

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
