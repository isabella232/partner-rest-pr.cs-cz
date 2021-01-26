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
# <a name="referral-connectors"></a><span data-ttu-id="33b5d-103">Konektory odkazů</span><span class="sxs-lookup"><span data-stu-id="33b5d-103">Referral connectors</span></span>

<span data-ttu-id="33b5d-104">Konektory odkazů můžete použít k synchronizaci odkazů partnerů se zájemci pro řízení vztahů se zákazníky (CRM).</span><span class="sxs-lookup"><span data-stu-id="33b5d-104">You can use referral connectors to synchronize partner referrals with customer relationship management (CRM) leads.</span></span> <span data-ttu-id="33b5d-105">Konektor odkazů můžete vytvořit pomocí [Microsoft Flow](https://flow.microsoft.com) jako koncový bod HTTPS pro příjem odkazů na partnery.</span><span class="sxs-lookup"><span data-stu-id="33b5d-105">You can create a referral connector using [Microsoft Flow](https://flow.microsoft.com) as the HTTPS endpoint to receive partner referrals.</span></span> <span data-ttu-id="33b5d-106">Pak můžete napsat odkaz přijatý tokem do systému CRM jako zájemce.</span><span class="sxs-lookup"><span data-stu-id="33b5d-106">You can then write the referral received by the flow to a CRM system as a lead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33b5d-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="33b5d-107">Prerequisites</span></span>

* <span data-ttu-id="33b5d-108">Předplatné Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="33b5d-108">Microsoft Flow subscription</span></span>
  * <span data-ttu-id="33b5d-109">Účet s přístupem správce k tomuto předplatnému</span><span class="sxs-lookup"><span data-stu-id="33b5d-109">Account with administrator access to this subscription</span></span>
* <span data-ttu-id="33b5d-110">ID aplikace Azure Active Directory (Azure AD), ID uživatele, heslo a ID tenanta (používá se pro přístup k partnerskému rozhraní API).</span><span class="sxs-lookup"><span data-stu-id="33b5d-110">Azure Active Directory (Azure AD) application ID, user id, password and tenant ID (used to access the Partner API).</span></span> <span data-ttu-id="33b5d-111">Pokyny k instalaci najdete v tématu [ověřování partnerů](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="33b5d-111">For setup instructions, see [Partner authentication](api-authentication.md).</span></span>
* <span data-ttu-id="33b5d-112">Předplatné [Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal)</span><span class="sxs-lookup"><span data-stu-id="33b5d-112">[Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) subscription.</span></span>
* <span data-ttu-id="33b5d-113">Odběr [událostí Webhooku partnerského centra](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) pro [Vytvoření odkazu](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) a [aktualizované události odkazu](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event)</span><span class="sxs-lookup"><span data-stu-id="33b5d-113">[Partner Center webhook event](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) events.</span></span>
* <span data-ttu-id="33b5d-114">Předplatné [Microsoft Dynamics 365](https://dynamics.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="33b5d-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) subscription</span></span>
  * <span data-ttu-id="33b5d-115">Modul prodeje povolen</span><span class="sxs-lookup"><span data-stu-id="33b5d-115">Sales module enabled</span></span>
  * <span data-ttu-id="33b5d-116">Účet s přístupem správce k tomuto předplatnému</span><span class="sxs-lookup"><span data-stu-id="33b5d-116">Account with administrator access to this subscription</span></span>

## <a name="flow-overview"></a><span data-ttu-id="33b5d-117">Přehled toku</span><span class="sxs-lookup"><span data-stu-id="33b5d-117">Flow overview</span></span>

<span data-ttu-id="33b5d-118">Odkazy se importují do CRM pomocí následujícího toku:</span><span class="sxs-lookup"><span data-stu-id="33b5d-118">Referrals are imported into the CRM using the following flow:</span></span>

1. <span data-ttu-id="33b5d-119">Partner nastaví Webhook pro příjem referenčních oznámení.</span><span class="sxs-lookup"><span data-stu-id="33b5d-119">Partner sets up a webhook to receive referral notifications.</span></span>
2. <span data-ttu-id="33b5d-120">Partner registruje Webhook v partnerském centru.</span><span class="sxs-lookup"><span data-stu-id="33b5d-120">Partner registers the webhook with Partner Center.</span></span> <span data-ttu-id="33b5d-121">Partner se při vytváření nebo aktualizaci odkazů přihlašuje také k odběru událostí Webhooku.</span><span class="sxs-lookup"><span data-stu-id="33b5d-121">The partner also subscribes to webhook events for when referrals are created or updated.</span></span>
3. <span data-ttu-id="33b5d-122">Referenční klient vytvoří nebo aktualizuje odkaz.</span><span class="sxs-lookup"><span data-stu-id="33b5d-122">Referral client creates or updates a referral.</span></span>
4. <span data-ttu-id="33b5d-123">Systém Webhooku partnerského centra kontroluje registraci partnera a pošle oznámení Webhooku.</span><span class="sxs-lookup"><span data-stu-id="33b5d-123">Partner Center webhook system checks for the partner's registration and sends a notification to the webhook.</span></span>
5. <span data-ttu-id="33b5d-124">Webhook obdrží oznámení.</span><span class="sxs-lookup"><span data-stu-id="33b5d-124">Webhook receives the notification.</span></span>
6. <span data-ttu-id="33b5d-125">Dokument flow v Microsoft Flow používá token k volání rozhraní API pro odkazování partnerského centra.</span><span class="sxs-lookup"><span data-stu-id="33b5d-125">Flow document in Microsoft flow uses a token to make a call to the Partner Center referral API.</span></span>
7. <span data-ttu-id="33b5d-126">Koncový bod toku získá odkaz.</span><span class="sxs-lookup"><span data-stu-id="33b5d-126">Flow endpoint gets the referral.</span></span>
8. <span data-ttu-id="33b5d-127">Koncový bod toku vytvoří zájemce CRM.</span><span class="sxs-lookup"><span data-stu-id="33b5d-127">Flow endpoint creates the CRM lead.</span></span>

![Vývojový diagram znázorňující kroky v této části pro import odkazů partnerů do CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a><span data-ttu-id="33b5d-129">Proces dokumentu toku</span><span class="sxs-lookup"><span data-stu-id="33b5d-129">Flow document process</span></span>

<span data-ttu-id="33b5d-130">Dokument toku pro konektor odkazů synchronizuje odkaz na partnera s zájemcem CRM z Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="33b5d-130">The flow document for a referral connector synchronizes a partner referral with a CRM lead from Dynamics 365.</span></span>

1. <span data-ttu-id="33b5d-131">Konektor získá token, ke kterému se má připojit `https://api.partner.microsoft.com/v1.0/engagements/referrals` .</span><span class="sxs-lookup"><span data-stu-id="33b5d-131">Connector gets a token to connect to `https://api.partner.microsoft.com/v1.0/engagements/referrals`.</span></span>
2. <span data-ttu-id="33b5d-132">Konektor získá odkaz, který aktivoval konektor pomocí `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .</span><span class="sxs-lookup"><span data-stu-id="33b5d-132">Connector obtains referral that triggered the connector using `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}`.</span></span>
3. <span data-ttu-id="33b5d-133">Konektor se připojuje k Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="33b5d-133">Connector connects to Dynamics 365.</span></span>
4. <span data-ttu-id="33b5d-134">Konektor vytvoří nového zájemce nebo aktualizuje stávajícího zájemce s nejnovějšími informacemi o tomto odkazu.</span><span class="sxs-lookup"><span data-stu-id="33b5d-134">Connector creates a new lead or updates an existing lead with the latest information on the referral.</span></span>
5. <span data-ttu-id="33b5d-135">Konektor aktualizuje odkazy s nejnovějšími aktualizacemi od zájemce CRM.</span><span class="sxs-lookup"><span data-stu-id="33b5d-135">Connector updates referral with the latest updates from the CRM lead.</span></span>

![Flowový diagram znázorňující kroky v této části pro proces dokumentu toku.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a><span data-ttu-id="33b5d-137">Vzorový konektor odkazů</span><span class="sxs-lookup"><span data-stu-id="33b5d-137">Sample referral connector</span></span>

<span data-ttu-id="33b5d-138">Následující *ukázkový konektor odkazů* ukazuje, jak synchronizovat odkazy partnerského centra s zájemci CRM v Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="33b5d-138">The following *sample referral connector* shows how to synchronize Partner Center referrals to CRM leads in Dynamics 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33b5d-139">Můžete zapisovat do různých CRMs nahrazením [konektorů toků](https://flow.microsoft.com/en-us/connectors/) v ukázkovém kódu.</span><span class="sxs-lookup"><span data-stu-id="33b5d-139">You can write to different CRMs by replacing the [flow connectors](https://flow.microsoft.com/en-us/connectors/) in the sample code.</span></span>

### <a name="import-flow-synchronization-package"></a><span data-ttu-id="33b5d-140">Importovat balíček synchronizace toků</span><span class="sxs-lookup"><span data-stu-id="33b5d-140">Import flow synchronization package</span></span>

<span data-ttu-id="33b5d-141">Stáhněte a importujte *vzorový balíček kódu* do Microsoft Flow a připojte se k Dynamics 365:</span><span class="sxs-lookup"><span data-stu-id="33b5d-141">Download and import the *sample code package* into Microsoft Flow and connect to Dynamics 365:</span></span>

1. <span data-ttu-id="33b5d-142">Stáhněte [balíček synchronizace toků](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) z [úložiště GitHub](https://github.com/microsoft/Partner-Center-Referrals).</span><span class="sxs-lookup"><span data-stu-id="33b5d-142">Download the [flow synchronization package](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) from the [GitHub repo](https://github.com/microsoft/Partner-Center-Referrals).</span></span>
2. <span data-ttu-id="33b5d-143">Přihlaste se k [Microsoft Flow](https://flow.microsoft.com) pomocí příslušných přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="33b5d-143">Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.</span></span>
3. <span data-ttu-id="33b5d-144">V navigační nabídce vyberte **Moje toky** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-144">Choose **My Flows** in the navigation menu.</span></span> <span data-ttu-id="33b5d-145">Pak zvolte **importovat**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-145">Then choose **Import**.</span></span>
4. <span data-ttu-id="33b5d-146">Na stránce **importovat balíček** vyberte balíček synchronizace toků, který jste stáhli.</span><span class="sxs-lookup"><span data-stu-id="33b5d-146">On the **Import package** page, select the flow synchronization package that you downloaded.</span></span> <span data-ttu-id="33b5d-147">Pak zvolte **nahrát**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-147">Then choose **Upload**.</span></span>

    ![Importovat obrazovku balíčku pro soubory balíčku](../images/importPackage.png)

5. <span data-ttu-id="33b5d-149">Po dokončení nahrávání balíčku Najděte balíček, který jste nahráli v **obsahu revize balíčku** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-149">After the package upload is complete, find the package you uploaded in the **Review Package Content** .</span></span>

    ![Podrobnosti obrazovky pro Import balíčku](../images/importPackageDetails.png)

6. <span data-ttu-id="33b5d-151">Klikněte na tlačítko **Akce** (ikona tužky) pro nahraný balíček.</span><span class="sxs-lookup"><span data-stu-id="33b5d-151">Choose the **Action** button (pencil icon) for your uploaded package.</span></span> <span data-ttu-id="33b5d-152">Otevře se okno **Nastavení importu** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-152">This opens the **Import setup** blade.</span></span>
7. <span data-ttu-id="33b5d-153">Vyberte typ **instalace** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-153">Choose your **Setup** type.</span></span>

    * <span data-ttu-id="33b5d-154">Pokud chcete vytvořit nový tok, vyberte **vytvořit jako nové** a zadejte nový **název prostředku**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-154">To create a new flow, select **Create as new**, and enter a new **Resource name**.</span></span>
    * <span data-ttu-id="33b5d-155">Pokud chcete aktualizovat existující tok se stejným názvem, vyberte **aktualizovat**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-155">To update an existing flow with the same name, select **Update**.</span></span>

    ![Vytvořit nebo aktualizovat novou obrazovku Manageru balíček s](../images/CreateNewConnection.png)

8. <span data-ttu-id="33b5d-157">Na stránce **importovat balíček** Najděte připojení k Dynamics 365 v části **Revize obsahu balíčku** v části **související prostředky**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-157">On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.</span></span>
9. <span data-ttu-id="33b5d-158">Klikněte na tlačítko **Akce** (ikona tužky) pro připojení k Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="33b5d-158">Choose the **Action** button (pencil icon) for your Dynamics 365 connection.</span></span> <span data-ttu-id="33b5d-159">Tím se otevře okno **Nastavení importu** pro tento související prostředek.</span><span class="sxs-lookup"><span data-stu-id="33b5d-159">This opens the **Import setup** blade for this related resource.</span></span>
10. <span data-ttu-id="33b5d-160">Zvolte **vytvořit nový** a vytvořte nové připojení k Dynamics 365 nebo vyberte existující připojení.</span><span class="sxs-lookup"><span data-stu-id="33b5d-160">Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection.</span></span>
11. <span data-ttu-id="33b5d-161">Ověřte, že stránka **Import balíčku** nyní zobrazuje vybraný typ nastavení toku a připojení k produktu Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="33b5d-161">Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection.</span></span> <span data-ttu-id="33b5d-162">Pak zvolte **importovat**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-162">Then choose **Import**.</span></span>

    ![Obrazovka pro import stavu balíčku](../images/importStatus.png)

12. <span data-ttu-id="33b5d-164">Ověřte, že je váš prostředek toku teď vytvořený nebo aktualizovaný.</span><span class="sxs-lookup"><span data-stu-id="33b5d-164">Verify that your flow resource is now created or updated.</span></span>

### <a name="configure-flow-parameters"></a><span data-ttu-id="33b5d-165">Konfigurace parametrů toku</span><span class="sxs-lookup"><span data-stu-id="33b5d-165">Configure flow parameters</span></span>

<span data-ttu-id="33b5d-166">Nakonfigurujte parametry prostředku Flow:</span><span class="sxs-lookup"><span data-stu-id="33b5d-166">Configure the parameters of your flow resource:</span></span>

1. <span data-ttu-id="33b5d-167">V [Microsoft Flow](https://flow.microsoft.com)v navigační nabídce vyberte **Moje toky** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-167">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="33b5d-168">Vyberte prostředek toku, který jste vytvořili nebo aktualizovali v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="33b5d-168">Choose the flow resource you created or updated in the previous section.</span></span>
3. <span data-ttu-id="33b5d-169">Na stránce flow (tok) vyberte **Upravit tok**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-169">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="33b5d-170">Vyberte proměnnou **ID aplikace AAD-(klienta)** a zadejte ID vaší aplikace služby Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33b5d-170">Choose the **AAD-Application (client) ID** variable and enter the ID of your Azure AD application.</span></span>
5. <span data-ttu-id="33b5d-171">Vyberte proměnnou **UserID** a zadejte své ID uživatele.</span><span class="sxs-lookup"><span data-stu-id="33b5d-171">Choose the **UserId** variable and enter your user ID.</span></span>
6. <span data-ttu-id="33b5d-172">Vyberte proměnnou **UserPassword** a zadejte uživatelské heslo.</span><span class="sxs-lookup"><span data-stu-id="33b5d-172">Choose the **UserPassword** variable and enter your user password.</span></span>
7. <span data-ttu-id="33b5d-173">Vyberte proměnnou **ID služby AAD-adresář (tenant)** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-173">Select the **AAD-Directory (tenant) ID** variable.</span></span> <span data-ttu-id="33b5d-174">Zadejte ID tenanta vaší aplikace Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33b5d-174">Enter the tenant ID of your Azure AD application.</span></span>
8. <span data-ttu-id="33b5d-175">Kliknutím na **Uložit** uložte tok.</span><span class="sxs-lookup"><span data-stu-id="33b5d-175">Choose **Save** to save your flow.</span></span>

    ![Obrazovka nastavení proměnných toků](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a><span data-ttu-id="33b5d-177">Ověření zpětného volání</span><span class="sxs-lookup"><span data-stu-id="33b5d-177">Authenticate the callback</span></span>

<span data-ttu-id="33b5d-178">Ověření události zpětného volání z partnerského centra:</span><span class="sxs-lookup"><span data-stu-id="33b5d-178">Authenticate the callback event from the Partner Center:</span></span>

> [!TIP]
> <span data-ttu-id="33b5d-179">Příklad najdete v [ukázce kódu aplikace Function App](#sample-function-app-code) v následující části.</span><span class="sxs-lookup"><span data-stu-id="33b5d-179">For an example, see the [sample function app code](#sample-function-app-code) in the following section.</span></span>

1. <span data-ttu-id="33b5d-180">[Vytvořte aplikaci funkcí Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) , která [ověří událost zpětného volání z partnerského centra](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span><span class="sxs-lookup"><span data-stu-id="33b5d-180">[Create an Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) that [authenticates the callback event from the Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span></span>

    1. <span data-ttu-id="33b5d-181">Ověřte, zda jsou k dispozici požadovaná záhlaví (**autorizace**, **x-MS-Certificate-URL** a **x-MS-Signature-Algorithm**).</span><span class="sxs-lookup"><span data-stu-id="33b5d-181">Verify that the required headers are present (**Authorization**, **x-ms-certificate-url**, and **x-ms-signature-algorithm**).</span></span>
    2. <span data-ttu-id="33b5d-182">Stáhněte si certifikát použitý k podepsání obsahu (**x-MS-Certificate-URL**).</span><span class="sxs-lookup"><span data-stu-id="33b5d-182">Download the certificate used to sign the content (**x-ms-certificate-url**).</span></span>
    3. <span data-ttu-id="33b5d-183">Ověřte řetěz certifikátů.</span><span class="sxs-lookup"><span data-stu-id="33b5d-183">Verify the certificate chain.</span></span>
    4. <span data-ttu-id="33b5d-184">Ověřte **organizaci** certifikátu.</span><span class="sxs-lookup"><span data-stu-id="33b5d-184">Verify the **Organization** of the certificate.</span></span>
    5. <span data-ttu-id="33b5d-185">Přečtěte si obsah s kódováním UTF-8 do vyrovnávací paměti.</span><span class="sxs-lookup"><span data-stu-id="33b5d-185">Read the content with UTF-8 encoding into a buffer.</span></span>
    6. <span data-ttu-id="33b5d-186">Vytvořte poskytovatele kryptografických služeb RSA.</span><span class="sxs-lookup"><span data-stu-id="33b5d-186">Create an RSA Crypto Provider.</span></span>
    7. <span data-ttu-id="33b5d-187">[Ověřte, že signatura odpovídá](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) hodnotám, které byly podepsány zadaným algoritmem hash (například SHA256).</span><span class="sxs-lookup"><span data-stu-id="33b5d-187">[Verify that the signature matches](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) what was signed with the specified hash algorithm (for example, SHA256).</span></span>
    8. <span data-ttu-id="33b5d-188">Pokud je ověření úspěšné, vrátí se zpráva **OK** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-188">If the verification succeeds, an **OK** message is returned.</span></span>

2. <span data-ttu-id="33b5d-189">Všimněte si vygenerovaného identifikátoru URI zpětného volání pro koncový bod HTTP aplikace Function App.</span><span class="sxs-lookup"><span data-stu-id="33b5d-189">Note the generated callback URI for your function app's HTTP endpoint.</span></span> <span data-ttu-id="33b5d-190">Tento identifikátor URI se zobrazí při vytváření aplikace Function App.</span><span class="sxs-lookup"><span data-stu-id="33b5d-190">This URI is displayed when you create your function app.</span></span> <span data-ttu-id="33b5d-191">Tento identifikátor URI můžete najít také na stránce prostředků Azure vaší aplikace Function App.</span><span class="sxs-lookup"><span data-stu-id="33b5d-191">You can also find this URI on your function app's Azure resource page.</span></span>
3. <span data-ttu-id="33b5d-192">V [Microsoft Flow](https://flow.microsoft.com)upravte tok "odkaz na partnera pro Microsoft Dynamics CRM zájemce", který jste naimportovali v oddílu *[Import toku synchronizace toků](#import-flow-synchronization-package)*.</span><span class="sxs-lookup"><span data-stu-id="33b5d-192">In [Microsoft Flow](https://flow.microsoft.com), edit the flow "Partner Referral to Microsoft Dynamics CRM Lead" that you imported in the section *[Import flow synchronization package](#import-flow-synchronization-package)*.</span></span>

    1. <span data-ttu-id="33b5d-193">Přidejte hodnotu identifikátoru URI aplikace Function App do kroku ověření certifikátu webového zavěšení.</span><span class="sxs-lookup"><span data-stu-id="33b5d-193">Add the value of the function app's URI to the "web hook certificate validation" step.</span></span>
    2. <span data-ttu-id="33b5d-194">Zkopírujte identifikátor URI zpětného volání aplikace Function App do dokumentu toku a vložte ho do něj.</span><span class="sxs-lookup"><span data-stu-id="33b5d-194">Copy and paste your function app's callback URI into the flow document.</span></span>
    3. <span data-ttu-id="33b5d-195">Uložte dokument Flow.</span><span class="sxs-lookup"><span data-stu-id="33b5d-195">Save your flow document.</span></span>

#### <a name="sample-function-app-code"></a><span data-ttu-id="33b5d-196">Ukázka kódu aplikace Function App</span><span class="sxs-lookup"><span data-stu-id="33b5d-196">Sample function app code</span></span>

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

### <a name="register-flow-with-partner-center"></a><span data-ttu-id="33b5d-197">Registrovat tok v partnerském centru</span><span class="sxs-lookup"><span data-stu-id="33b5d-197">Register flow with Partner Center</span></span>

<span data-ttu-id="33b5d-198">Zaregistrujte svůj prostředek toku pomocí partnerského centra, aby se aktivoval tok a přijímaly události Webhooku:</span><span class="sxs-lookup"><span data-stu-id="33b5d-198">Register your flow resource with the Partner Center to trigger the flow and receive webhook events:</span></span>

1. <span data-ttu-id="33b5d-199">V [Microsoft Flow](https://flow.microsoft.com)v navigační nabídce vyberte **Moje toky** .</span><span class="sxs-lookup"><span data-stu-id="33b5d-199">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="33b5d-200">Vyberte tok, který jste vytvořili nebo aktualizovali.</span><span class="sxs-lookup"><span data-stu-id="33b5d-200">Choose the flow you created or updated.</span></span>
3. <span data-ttu-id="33b5d-201">Na stránce flow (tok) vyberte **Upravit tok**.</span><span class="sxs-lookup"><span data-stu-id="33b5d-201">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="33b5d-202">Zkopírujte a uložte **adresu URL příspěvku http** daného toku.</span><span class="sxs-lookup"><span data-stu-id="33b5d-202">Copy and save the flow's **HTTP POST URL**.</span></span> <span data-ttu-id="33b5d-203">K aktivaci toku budete muset použít tuto adresu URL.</span><span class="sxs-lookup"><span data-stu-id="33b5d-203">You will need to use this URL to trigger the flow.</span></span>
5. <span data-ttu-id="33b5d-204">[Zaregistrujte se, pokud chcete přijímat události Webhooku](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) při vytváření nebo aktualizaci odkazů.</span><span class="sxs-lookup"><span data-stu-id="33b5d-204">[Register to receive webhook events](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) when referrals are created or updated.</span></span> <span data-ttu-id="33b5d-205">Použijte následující formát textu:</span><span class="sxs-lookup"><span data-stu-id="33b5d-205">Use the following body format:</span></span>

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
