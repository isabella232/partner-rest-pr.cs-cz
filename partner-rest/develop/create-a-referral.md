---
title: Vytvoření reference
description: Vytvořte nezávislé nebo sdílené odkazy v partnerském rozhraní API.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770332"
---
# <a name="create-a-referral"></a>Vytvoření reference

Platí pro:

- Partnerské rozhraní API

V tomto tématu se dozvíte, jak vytvořit odkaz. Existují dva typy [ReferralType](referral-resources.md#referraltype):

1. Nezávislé: kde je odkaz viditelný pro jednoho partnera.
2. Shared: kde je odkaz viditelný pro dvě strany, které pracují společně. Například pokud společnost Microsoft a partner pracují společně v rámci spoluprodejních operací, může být odkaz sdílen mezi obě strany. Další informace najdete v části [Vytvoření sdíleného odkazu](#create-a-shared-referral).

## <a name="prerequisites"></a>Požadavky

- Přihlašovací údaje popsané v tématu [ověřování rozhraní API partnera](api-authentication.md). Tento scénář podporuje ověřování pomocí přihlašovacích údajů pro aplikace a uživatele.

## <a name="rest-request"></a>Žádost REST

### <a name="request-syntax"></a>Syntaxe žádosti

| Metoda  | Identifikátor URI žádosti                                                  |
|---------|--------------------------------------------------------------|
| **SPUŠTĚNÍ** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a>Hlavičky požadavku

- Další informace najdete v tématu [záhlaví REST rozhraní API pro partnery](headers.md) .

### <a name="request-body"></a>Text požadavku

Tato tabulka popisuje vlastnosti [odkazu](referral-resources.md) v těle žádosti o značku nového odkazu.

| Vlastnost            | Typ                                                                 | Popis                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Název                | řetězec                                                               | Název odkazu                                                                                            |
| ExternalReferenceId | řetězec                                                               | Externí identifikátor pro odkaz Například vlastní ID zájemce nebo příležitosti pro Dynamics 365.                   |
| Status              | [ReferralStatus](referral-resources.md#referralstatus)               | [Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu.          |
| SubStatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | [Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují dílčí stav odkazu.       |
| StatusReason        | řetězec                                                               | Popisná zpráva o stavu Například vysvětlete, proč byl odkaz ztracen.                            |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Představuje typ odkazu. **Požadovanou.**                                                                                        |
| Qualification       | [ReferralQualification](referral-resources.md#referralqualification) | Představuje kvalitu odkazu.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Kontaktní údaje zákazníka.  **Požadovanou.**                                                                                      |
| Souhlas             | [Souhlas](referral-resources.md#consent)                             | Příznaky souhlasu týkající se sdílení informací s ostatními organizacemi a jejich umožnění kontaktování uživatelů **Požadováno.**               |
| Podrobnosti             | [ReferralDetails](referral-resources.md#referraldetails)             | Podrobnosti o zákazníkovi, poznámky, hodnota obchodu, datum ukončení měny. **Požadovanou.**                                                           |
| Tým                | [Člen](referral-resources.md#member)                               | Představuje uživatele v organizacích, kteří se účastní zapojení partnerů.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení. |
| Cíl         | [ReferralTarget](referral-resources.md#target)        | Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.  |

#### <a name="status--substatus-transition-states"></a>Stavový & stav přechodu dílčího stavu

| Status | Povolený přechod stavu | Povolený dílčí stav            |
|--------|---------------------------|------------------------------|
| Nová    | Nové, aktivní, uzavřené       | Čeká na vyřízení, přijato            |
| Aktivní | Aktivní, uzavřeno            | Přijato                     |
| Uzavřeno | Uzavřeno                    | Výhra, ztraceno, odmítnuto, vypršela platnost |

### <a name="request-example"></a>Příklad požadavku

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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
    }
}
```

## <a name="rest-response"></a>Odpověď REST

V případě úspěchu vrátí tato metoda v těle odpovědi vyplněný prostředek [reference](referral-resources.md) .

### <a name="response-success-and-error-codes"></a>Úspěšné odpovědi a chybové kódy

Každá odpověď je dodávána se stavovým kódem HTTP, který označuje úspěch nebo selhání a další informace o ladění. Použijte nástroj pro trasování sítě ke čtení tohoto kódu, typu chyby a dalších parametrů. Úplný seznam najdete v tématu [kódy chyb](error-codes.md).

### <a name="response-example"></a>Příklad odpovědi

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
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

## <a name="create-a-shared-referral"></a>Vytvoření sdíleného odkazu

Existují dva kroky k vytvoření odkazu na **sdílený** [typ odkazu](referral-resources.md#referraltype).

1. [Vytvořit sdílený odkaz](#create-your-referral)
2. [Vytvoření propojeného odkazu pro druhou stranu](#create-a-connected-referral)

Následující postup popisuje tyto dva kroky při vytváření sdíleného odkazu.

![Vývojový diagram znázorňující sdílený odkaz se dvěma odkazy připojenými prostřednictvím rozhraní Microsoft Partner API](../images/SharedReferral.png)

### <a name="create-your-referral"></a>Vytvoření odkazu

1. Vytvoří odkaz s [ReferralType](referral-resources.md#referraltype) nastavenou na Shared.
2. Zkopírujte **engagementId** z odpovědi na vrácení.

Ukázka [ReferralTarget](referral-resources.md#target) pro referenci

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a>Vytvoření propojeného odkazu

1. Vytvořte další odkaz na Microsoft.
2. Zahrňte **enagementId** z vašeho odkazu, aby byly vzájemně vázané.

Ukázka [ReferralTarget](referral-resources.md#target) pro referenci Microsoftu

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```