---
title: Kódy chyb REST rozhraní API partnerů
description: Rozhraní REST API partnerského serveru vrátí objekt JSON se stavovým kódem informací o úspěchu nebo selhání vaší žádosti.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0829f48e5028b4a19e8a6f7b89fbb41d83a50cab
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770346"
---
# <a name="partner-api-rest-error-codes"></a>Kódy chyb REST rozhraní API partnerů

Platí pro:

- Partnerské rozhraní API

Chyby v partnerských rozhraních REST API se vracejí pomocí standardních stavových kódů HTTP a také objektu odpovědi na chybu JSON.

## <a name="http-status-codes"></a>Stavové kódy HTTP

Následující tabulka uvádí a popisuje stavové kódy HTTP, které mohou být vráceny.

| Stavový kód | Zpráva o stavu                  | Description                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | Chybný požadavek                     | Požadavek nelze zpracovat, protože je poškozený nebo není správný.                                                                       |
| 401         | Neautorizováno                    | Požadované ověřovací údaje buď chybí, nebo nejsou pro prostředek platné.                                                   |
| 403         | Forbidden                       | K požadovanému prostředku byl odepřen přístup. Uživatel možná nemá dostatečná oprávnění. **Důležité: Pokud se pro prostředek použijí zásady podmíněného přístupu, `HTTP 403; Forbidden error=insufficent_claims` může se vrátit.** Další podrobnosti o Microsoft Graph a podmíněném přístupu najdete v tématu [pokyny pro vývojáře pro Azure Active Directory podmíněný přístup](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer) .  |
| 404         | Nenalezeno                       | Požadovaný prostředek neexistuje.                                                                                                  |
| 405         | Metoda není povolená.              | Metoda HTTP v požadavku není u prostředku povolena.                                                                         |
| 406         | Nepřijatelný                  | Tato služba nepodporuje formát požadovaný v hlavičce Accept.                                                                |
| 409         | Konflikt                        | Aktuální stav koliduje s tím, co požadavek očekává. Například zadaná nadřazená složka pravděpodobně neexistuje.                   |
| 410         | Doručen                            | Požadovaný prostředek už na serveru není dostupný.                                               |
| 411         | Požadovaná délka                 | Požadavek vyžaduje hlavičku Content-Length.                                                                                    |
| 412         | Předběžná podmínka se nezdařila.             | Předběžná podmínka poskytnutá v žádosti (například hlavička If-Match) se neshoduje s aktuálním stavem prostředku.                       |
| 413         | Entita požadavku je příliš velká.        | Velikost požadavku překračuje maximální limit.                                                                                            |
| 415         | Nepodporovaný typ média          | Typ obsahu požadavku je formát, který služba nepodporuje.                                                      |
| 416         | Požadovaný rozsah nesplňuje požadavky. | Zadaný rozsah bajtů je neplatný nebo není k dispozici.                                                                                    |
| 422         | Nezpracované entity            | Požadavek nelze zpracovat, protože je sémanticky nesprávným.                                                                        |
| 423         | Uzamčeno                          | Prostředek, ke kterému se přistupuje, je zamčený.                                                                                          |
| 429         | Příliš mnoho žádostí               | Klientská aplikace byla omezená a neměla by se pokoušet o opakování žádosti, dokud neuplyne časový limit.                |
| 500         | Vnitřní chyba serveru           | Při zpracování požadavku došlo k vnitřní chybě serveru.                                                                       |
| 501         | Neimplementováno                 | Požadovaná funkce není implementovaná.                                                                                               |
| 503         | Služba není k dispozici             | Služba je dočasně nedostupná pro údržbu nebo je přetížená. Žádost můžete po uplynutí zpoždění zopakovat, což je délka, kterou lze zadat v hlavičce Retry-After.|
| 504         | Časový limit brány                 | Server, který funguje jako proxy, nedostal včas odpověď od nadřazeného serveru, ke kterému je potřebný pro přístup při pokusu o dokončení žádosti. Může nastat společně s 503. |
| 507         | Nedostatek úložiště            | Byla dosažena maximální kvóta úložiště.                                                                                            |
| 509         | Překročil se limit šířky pásma.        | Vaše aplikace byla omezena na překročení maximální šířky pásma. Aplikace může požadavek opakovat znovu po uplynutí delší doby. |

Chybová odpověď je jeden objekt JSON, který obsahuje jedinou vlastnost s názvem **Error**. Tento objekt obsahuje všechny podrobnosti o chybě. Namísto stavového kódu HTTP můžete použít informace, které jsou zde vráceny. Následuje příklad úplné chybové zprávy JSON.

## <a name="error-resource-type"></a>Typ prostředku chyby

Chybová odpověď je jeden objekt JSON, který obsahuje jedinou vlastnost s názvem **Error**. Tento objekt obsahuje všechny podrobnosti o chybě. Namísto stavového kódu HTTP můžete použít informace, které jsou zde vráceny. Následuje příklad úplné chybové zprávy JSON.

Následující ukázka tabulky a kódu popisuje schéma chybové odpovědi.

| Název        | Typ   | Description                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| kód        | řetězec | Vždy vráceno. Označuje typ chyby, ke které došlo. Není null.                          |
| zpráva | řetězec | Vždy vráceno. Podrobně popisuje chybu a obsahuje další informace o ladění. Neprázdná hodnota, která není null. Maximální délka je 1024 znaků. |
| innerError        | object  | Nepovinný parametr. Další objekt Error, který může být konkrétnější než chyba nejvyšší úrovně.                                   |
| cílové      | řetězec | Cíl, kde chyba vznikla.                                                      |

### <a name="code-property"></a>Vlastnost Code

`code`Vlastnost obsahuje jednu z následujících možných hodnot. Vaše aplikace by měly být připravené k manipulaci s některou z těchto chyb.

| Kód                      | Description
|:--------------------------|:--------------
| **accessDenied**          | Volající nemá oprávnění k provedení této akce.
| **generalException**      | Došlo k neurčené chybě.
| **invalidRequest**        | Požadavek je poškozený nebo nesprávný.
| **itemNotFound**          | Prostředek se nepovedlo najít.
|**preconditionFailed**     | Předběžná podmínka poskytnutá v žádosti (například hlavička If-Match) se neshoduje s aktuálním stavem prostředku.
| **resourceModified**      | Aktualizovaný prostředek se od posledního čtení změnil, obvykle se neshoduje s eTag.
| **serviceNotAvailable**   | Služba není k dispozici. Opakujte pokus o zadání po prodlevě. Může se jednat o Retry-After záhlaví.
| **neověřené**       | Volající není ověřen.

### <a name="message-property"></a>Message – vlastnost

`message`Vlastnost v kořenu obsahuje chybovou zprávu určenou vývojářům ke čtení. Chybové zprávy nejsou lokalizovány a neměly by být zobrazeny přímo uživateli. Při zpracování chyb by váš kód neměl kontrolovat hodnoty proti `message` hodnotám, protože se mohou kdykoli změnit a často obsahují dynamické informace specifické pro neúspěšný požadavek. Měli byste pouze kód s kódy chyb vrácenými ve `code` vlastnostech.

### <a name="innererror-object"></a>Objekt InnerError

`innererror`Objekt může rekurzivně obsahovat více `innererror` objektů s dalšími, konkrétnější kódy chyb. Při zpracování chyby by aplikace měly projít všemi dostupnými kódy chyb a používat nejpodrobnější informace, které jsou k dispozici.

V rámci vnořených objektů jsou k dispozici některé další chyby, ke kterým může aplikace dojít `innererror` . Aplikace se nevyžadují k tomu, aby je bylo možné zpracovat, ale v případě jejich výběru. Služba může přidat nové chybové kódy nebo přestat vracet staré položky, takže je důležité, aby všechny aplikace dokázaly zpracovat [základní kódy chyb].

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```
