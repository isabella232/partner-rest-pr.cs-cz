---
title: Aktualizace zájemce nebo příležitosti (zastaralé)
description: Umožňuje aktualizovat podrobnosti o zájemci nebo příležitosti. Tato metoda aktualizace potenciálního zákazníka nebo příležitosti je zastaralá a místo toho jsme recommmendi použití OPRAVNého volání.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770361"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a>Aktualizace zájemce nebo příležitosti (zastaralé)

Platí pro:

- Partnerské rozhraní API

V tomto tématu se dozvíte, jak aktualizovat podrobnosti o zájemcích nebo příležitostech, jako je například hodnota koupě, odhadované datum uzavření nebo Správa fází prodeje mezi další podrobnosti. 


> [!IMPORTANT]
Tato metoda aktualizace potenciálního zákazníka nebo příležitosti je zastaralá a místo toho jsme recommmendi použití [opravného](patch-a-referral.md) volání.

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.
- Toto rozhraní API aktuálně podporuje jenom přístup uživatelů v případě, že se partneři musí nacházet v jedné z následujících rolí: globální správce, Správce odkazů nebo uživatel s odkazem.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                       |
|---------|-------------------------------------------------------------------|
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a>Hlavičky požadavku

- Další informace najdete v tématu [záhlaví REST rozhraní API pro partnery](headers.md).

> [!IMPORTANT]
> Nezapomeňte nastavit hlavičku **If-Match** .

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje vlastnosti [odkazu](referral-resources.md) v těle žádosti.

| Vlastnost            | Typ                                                                 | Description                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Id                  | řetězec                                                               | ID pro tento odkaz.                                                                                            |
| EngagementId        | řetězec                                                               | EngagementID pro tento odkaz. K jednomu EngagementID může být přidruženo několik odkazů.                    |
| Name                | řetězec                                                               | Název odkazu                                                                                            |
| ExternalReferenceId | řetězec                                                               | Externí identifikátor pro odkaz Příklad: Uložte si vlastní ID zájemce nebo příležitosti pro Dynamics 365.                    |
| CreatedDateTime     | řetězec ve formátu data a času UTC                                       | Datum vytvoření odkazu                                                                                   |
| UpdatedDateTime     | řetězec ve formátu data a času UTC                                       | Datum poslední aktualizace odkazu                                                                              |
| ExpirationDateTime  | řetězec ve formátu data a času UTC                                       | Datum, po jehož uplynutí bude platnost odkazu vypršet.                                                                                   |
| Status              | [ReferralStatus](referral-resources.md#referralstatus)               | [Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu.          |
| SubStatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | [Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav dílčího odkazu.      |
| StatusReason        | řetězec                                                               | Popisná zpráva o stavu Například vysvětlete, proč byl odkaz ztracen.                              |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Představuje typ odkazu.                                                                                        |
| Qualification       | [ReferralQualification](referral-resources.md#referralqualification) | Představuje kvalitu odkazu.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Kontaktní údaje zákazníka.                                                                                        |
| Souhlas             | [Souhlas](referral-resources.md#consent)                             | Příznaky souhlasu týkající se sdílení informací s ostatními organizacemi a jejich umožnění kontaktování uživatelů                |
| Podrobnosti             | [ReferralDetails](referral-resources.md#referraldetails)             | Podrobnosti o zákazníkovi, poznámky, hodnota obchodu, datum ukončení měny.                                                          |
| Tým                | [Člen](referral-resources.md#member)                               | Představuje uživatele v organizacích, kteří se účastní zapojení partnerů.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení. |
| Cíl         | [ReferralTarget](referral-resources.md#target)        | Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.  |

### <a name="status-and-substatus-transition-states"></a>Stavy přechodu stavu a dílčího stavu

| Status | Povolený přechod stavu | Povolený dílčí stav            |
|--------|---------------------------|------------------------------|
| Nová    | Nové, aktivní, uzavřené       | Čeká na vyřízení, přijato            |
| Aktivní | Aktivní, uzavřeno            | Přijato                     |
| Uzavřeno | Uzavřeno                    | Výhra, ztraceno, odmítnuto, vypršela platnost |

### <a name="request-example"></a>Příklad požadavku

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> Odeberte `"links": { }` objekt z prostředku PUT.

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v těle odpovědi vyplněný prostředek [reference](referral-resources.md) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```