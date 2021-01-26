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
# <a name="get-the-list-of-leads-and-opportunities"></a>Získání seznamu potenciálních zákazníků a příležitostí

Platí pro:

- Partnerské rozhraní API

 V tomto tématu se dozvíte, jak získat seznam zájemců přijatých ze stránky Microsoftu pro poskytovatele řešení a možnosti společného prodeje, které od prodejců Microsoftu nebo jiných partnerů obdrželi. Tím se také načtou seznam příležitostí a příležitostí, které vytvořila vaše organizace, ze společného prodeje.

> [!Note]
> Zájemci přijatý od komerčního tržiště Microsoftu (Azure Marketplace a AppSource) se nepodporují.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.
- Toto rozhraní API aktuálně podporuje jenom přístup uživatelů v případě, že se partneři musí nacházet v jedné z následujících rolí: globální správce, Správce odkazů nebo uživatel s odkazem.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                    |
|:--------|:---------------------------------------------------------------|
| **Čtěte** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a>Podporované operace OData

| Název     | Popis     | Povinné    | Příklad                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| $select  | Vybere pole  | No          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| $filter  | Výsledky filtrů | Doporučeno | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| $orderby | Výsledky objednávek  | Doporučeno | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a>Podporované parametry OrderBy

Seznam potenciálních zákazníků a příležitostí můžete seřadit pomocí následujících parametrů $orderby.

| Název            | Typ     | Description                                       |
|:----------------|:---------|:--------------------------------------------------|
| createdDateTime | DateTime | Datum a čas vytvoření zájemce nebo příležitosti |
| updatedDateTime | DateTime | Aktualizovat datum a čas zájemce nebo příležitosti   |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v části [partner – záhlaví REST](headers.md) .

### <a name="request-body"></a>Text požadavku

Žádné

### <a name="request-example"></a>Příklad požadavku

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi kolekci [zájemců a/nebo příležitostí](referral-resources.md).

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se [stavovým kódem http](error-codes.md) , který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.

### <a name="response-example"></a>Příklad odpovědi

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

`@odata.nextLink`K získání další stránky výsledků použijte.

> [!Note]
> Pole v příkladu illustratration výše nejsou vyčerpávající. Skutečná odpověď rozhraní API obsahuje více polí, jako jsou například týmy zákazníka a partnera. Úplný seznam podporovaných polí najdete v tématu věnovaném [prostředkům reference](referral-resources.md).

## <a name="sample-requests"></a>Ukázkové požadavky

1. Získá prvních 10 nejaktuálnějších příležitostí pro prodej. Požadavek načte příležitosti iniciované obchodním zástupcem Microsoftu nebo jiným partnerem a vyzve organizaci, aby se účastnila aktivity spoluprodeje.
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. Získá nejnovější příchozí zájemce a příležitosti, na které nebyly odpovědi reagovat.  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > Pokud neodpovíte na zájemce nebo příležitost v rámci přiděleného času (v současnosti 14 dnů), archivaci vyprší a upozorněte buď společnost Microsoft, nebo partnera, který vám tuto příležitost poslal.

3. Získá nejnovější aktivní možnosti společného prodeje iniciované vaší organizací a na základě konkrétního prodejce bude pracovat.
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```