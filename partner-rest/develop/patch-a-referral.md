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
# <a name="update-a-lead-or-opportunity"></a>Aktualizace potenciálního zákazníka nebo příležitosti

Platí pro:

- Partnerské rozhraní API

V tomto tématu se dozvíte, jak aktualizovat podrobnosti o zájemcích nebo příležitostech, jako je například hodnota koupě, odhadované datum uzavření nebo Správa fází prodeje mezi další podrobnosti.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.
- Toto rozhraní API aktuálně podporuje jenom přístup uživatelů v případě, že se partneři musí nacházet v jedné z následujících rolí: globální správce, Správce odkazů nebo uživatel s odkazem.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                       |
|---------|-------------------------------------------------------------------|
| **POUŽITA** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a>Parametr URI


| Název                   | Typ     | Vyžadováno | Popis                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | řetězec   | Yes       | Jedinečný identifikátor příležitosti zájemce nebo společného prodeje       |

### <a name="request-headers"></a>Hlavičky požadavku

Další informace najdete v části [partner – záhlaví REST](headers.md) .

### <a name="request-body"></a>Text požadavku

Tělo žádosti následuje po formátu [opravy JSON](https://tools.ietf.org/html/rfc6902) . Dokument opravy JSON má pole operací. Každá operace identifikuje konkrétní typ změny. Příklady takových změn zahrnují přidání prvku pole nebo nahrazení hodnoty vlastnosti.

> [!Important]
> Rozhraní API aktuálně podporuje pouze `replace` operace a `add` .

### <a name="request-example"></a>Příklad požadavku

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
> Pokud je předána hlavička **If-Match** , bude použita pro řízení souběžnosti.

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu obsahuje tělo odpovědi aktualizovaný [zájemce nebo příležitost](referral-resources.md).


### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se [stavovým kódem http](error-codes.md) , který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů.

### <a name="response-example"></a>Příklad odpovědi

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> Tělo odpovědi závisí na hlavičce **preferovat** . Pokud je hodnota hlavičky v požadavku vynechána, text odpovědi je prázdný kódem stavu HTTP 204. Přidejte `Prefer: return=representation` do záhlaví, abyste získali aktualizovaný zájemce nebo příležitost.

## <a name="sample-requests"></a>Ukázkové požadavky

1. Aktualizuje hodnotu obchodu s příležitostí na 10000 a aktualizuje poznámky. Neexistují žádné kontroly souběžnosti z důvodu neexistence `If-Match` hlavičky.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. Aktualizuje stav zájemce nebo příležitosti k získání.
    
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
    > `status`Pole a `substatus` by měly být v souladu s povolenou sadou přechodových hodnot, jak je popsáno [zde](referral-resources.md).

3. Přidá nového člena z vaší organizace do týmu zájemce nebo příležitosti. Odpověď bude obsahovat aktualizovaného zájemce nebo příležitosti z důvodu přítomnosti `Prefer: return=representation` hlavičky.

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
