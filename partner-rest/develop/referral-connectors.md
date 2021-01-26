---
title: Konektory odkazů.
description: Synchronizace partnerských odkazů s Dynamics 365 CRM zájemce pomocí Microsoft Flow.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a62023feb03114bb7ba1136b7700875f24c2e01
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770324"
---
# <a name="referral-connectors"></a>Konektory odkazů

Konektory odkazů můžete použít k synchronizaci odkazů partnerů se zájemci pro řízení vztahů se zákazníky (CRM). Konektor odkazů můžete vytvořit pomocí [Microsoft Flow](https://flow.microsoft.com) jako koncový bod HTTPS pro příjem odkazů na partnery. Pak můžete napsat odkaz přijatý tokem do systému CRM jako zájemce.

## <a name="prerequisites"></a>Požadavky

* Předplatné Microsoft Flow
  * Účet s přístupem správce k tomuto předplatnému
* ID aplikace Azure Active Directory (Azure AD), ID uživatele, heslo a ID tenanta (používá se pro přístup k partnerskému rozhraní API). Pokyny k instalaci najdete v tématu [ověřování partnerů](api-authentication.md).
* Předplatné [Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal)
* Odběr [událostí Webhooku partnerského centra](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) pro [Vytvoření odkazu](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) a [aktualizované události odkazu](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event)
* Předplatné [Microsoft Dynamics 365](https://dynamics.microsoft.com)
  * Modul prodeje povolen
  * Účet s přístupem správce k tomuto předplatnému

## <a name="flow-overview"></a>Přehled toku

Odkazy se importují do CRM pomocí následujícího toku:

1. Partner nastaví Webhook pro příjem referenčních oznámení.
2. Partner registruje Webhook v partnerském centru. Partner se při vytváření nebo aktualizaci odkazů přihlašuje také k odběru událostí Webhooku.
3. Referenční klient vytvoří nebo aktualizuje odkaz.
4. Systém Webhooku partnerského centra kontroluje registraci partnera a pošle oznámení Webhooku.
5. Webhook obdrží oznámení.
6. Dokument flow v Microsoft Flow používá token k volání rozhraní API pro odkazování partnerského centra.
7. Koncový bod toku získá odkaz.
8. Koncový bod toku vytvoří zájemce CRM.

![Vývojový diagram znázorňující kroky v této části pro import odkazů partnerů do CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a>Proces dokumentu toku

Dokument toku pro konektor odkazů synchronizuje odkaz na partnera s zájemcem CRM z Dynamics 365.

1. Konektor získá token, ke kterému se má připojit `https://api.partner.microsoft.com/v1.0/engagements/referrals` .
2. Konektor získá odkaz, který aktivoval konektor pomocí `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .
3. Konektor se připojuje k Dynamics 365.
4. Konektor vytvoří nového zájemce nebo aktualizuje stávajícího zájemce s nejnovějšími informacemi o tomto odkazu.
5. Konektor aktualizuje odkazy s nejnovějšími aktualizacemi od zájemce CRM.

![Flowový diagram znázorňující kroky v této části pro proces dokumentu toku.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a>Vzorový konektor odkazů

Následující *ukázkový konektor odkazů* ukazuje, jak synchronizovat odkazy partnerského centra s zájemci CRM v Dynamics 365.

> [!IMPORTANT]
> Můžete zapisovat do různých CRMs nahrazením [konektorů toků](https://flow.microsoft.com/en-us/connectors/) v ukázkovém kódu.

### <a name="import-flow-synchronization-package"></a>Importovat balíček synchronizace toků

Stáhněte a importujte *vzorový balíček kódu* do Microsoft Flow a připojte se k Dynamics 365:

1. Stáhněte [balíček synchronizace toků](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) z [úložiště GitHub](https://github.com/microsoft/Partner-Center-Referrals).
2. Přihlaste se k [Microsoft Flow](https://flow.microsoft.com) pomocí příslušných přihlašovacích údajů.
3. V navigační nabídce vyberte **Moje toky** . Pak zvolte **importovat**.
4. Na stránce **importovat balíček** vyberte balíček synchronizace toků, který jste stáhli. Pak zvolte **nahrát**.

    ![Importovat obrazovku balíčku pro soubory balíčku](../images/importPackage.png)

5. Po dokončení nahrávání balíčku Najděte balíček, který jste nahráli v **obsahu revize balíčku** .

    ![Podrobnosti obrazovky pro Import balíčku](../images/importPackageDetails.png)

6. Klikněte na tlačítko **Akce** (ikona tužky) pro nahraný balíček. Otevře se okno **Nastavení importu** .
7. Vyberte typ **instalace** .

    * Pokud chcete vytvořit nový tok, vyberte **vytvořit jako nové** a zadejte nový **název prostředku**.
    * Pokud chcete aktualizovat existující tok se stejným názvem, vyberte **aktualizovat**.

    ![Vytvořit nebo aktualizovat novou obrazovku Manageru balíček s](../images/CreateNewConnection.png)

8. Na stránce **importovat balíček** Najděte připojení k Dynamics 365 v části **Revize obsahu balíčku** v části **související prostředky**.
9. Klikněte na tlačítko **Akce** (ikona tužky) pro připojení k Dynamics 365. Tím se otevře okno **Nastavení importu** pro tento související prostředek.
10. Zvolte **vytvořit nový** a vytvořte nové připojení k Dynamics 365 nebo vyberte existující připojení.
11. Ověřte, že stránka **Import balíčku** nyní zobrazuje vybraný typ nastavení toku a připojení k produktu Dynamics 365. Pak zvolte **importovat**.

    ![Obrazovka pro import stavu balíčku](../images/importStatus.png)

12. Ověřte, že je váš prostředek toku teď vytvořený nebo aktualizovaný.

### <a name="configure-flow-parameters"></a>Konfigurace parametrů toku

Nakonfigurujte parametry prostředku Flow:

1. V [Microsoft Flow](https://flow.microsoft.com)v navigační nabídce vyberte **Moje toky** .
2. Vyberte prostředek toku, který jste vytvořili nebo aktualizovali v předchozí části.
3. Na stránce flow (tok) vyberte **Upravit tok**.
4. Vyberte proměnnou **ID aplikace AAD-(klienta)** a zadejte ID vaší aplikace služby Azure AD.
5. Vyberte proměnnou **UserID** a zadejte své ID uživatele.
6. Vyberte proměnnou **UserPassword** a zadejte uživatelské heslo.
7. Vyberte proměnnou **ID služby AAD-adresář (tenant)** . Zadejte ID tenanta vaší aplikace Azure AD.
8. Kliknutím na **Uložit** uložte tok.

    ![Obrazovka nastavení proměnných toků](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a>Ověření zpětného volání

Ověření události zpětného volání z partnerského centra:

> [!TIP]
> Příklad najdete v [ukázce kódu aplikace Function App](#sample-function-app-code) v následující části.

1. [Vytvořte aplikaci funkcí Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) , která [ověří událost zpětného volání z partnerského centra](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).

    1. Ověřte, zda jsou k dispozici požadovaná záhlaví (**autorizace**, **x-MS-Certificate-URL** a **x-MS-Signature-Algorithm**).
    2. Stáhněte si certifikát použitý k podepsání obsahu (**x-MS-Certificate-URL**).
    3. Ověřte řetěz certifikátů.
    4. Ověřte **organizaci** certifikátu.
    5. Přečtěte si obsah s kódováním UTF-8 do vyrovnávací paměti.
    6. Vytvořte poskytovatele kryptografických služeb RSA.
    7. [Ověřte, že signatura odpovídá](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) hodnotám, které byly podepsány zadaným algoritmem hash (například SHA256).
    8. Pokud je ověření úspěšné, vrátí se zpráva **OK** .

2. Všimněte si vygenerovaného identifikátoru URI zpětného volání pro koncový bod HTTP aplikace Function App. Tento identifikátor URI se zobrazí při vytváření aplikace Function App. Tento identifikátor URI můžete najít také na stránce prostředků Azure vaší aplikace Function App.
3. V [Microsoft Flow](https://flow.microsoft.com)upravte tok "odkaz na partnera pro Microsoft Dynamics CRM zájemce", který jste naimportovali v oddílu *[Import toku synchronizace toků](#import-flow-synchronization-package)*.

    1. Přidejte hodnotu identifikátoru URI aplikace Function App do kroku ověření certifikátu webového zavěšení.
    2. Zkopírujte identifikátor URI zpětného volání aplikace Function App do dokumentu toku a vložte ho do něj.
    3. Uložte dokument Flow.

#### <a name="sample-function-app-code"></a>Ukázka kódu aplikace Function App

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a>Registrovat tok v partnerském centru

Zaregistrujte svůj prostředek toku pomocí partnerského centra, aby se aktivoval tok a přijímaly události Webhooku:

1. V [Microsoft Flow](https://flow.microsoft.com)v navigační nabídce vyberte **Moje toky** .
2. Vyberte tok, který jste vytvořili nebo aktualizovali.
3. Na stránce flow (tok) vyberte **Upravit tok**.
4. Zkopírujte a uložte **adresu URL příspěvku http** daného toku. K aktivaci toku budete muset použít tuto adresu URL.
5. [Zaregistrujte se, pokud chcete přijímat události Webhooku](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) při vytváření nebo aktualizaci odkazů. Použijte následující formát textu:

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```
