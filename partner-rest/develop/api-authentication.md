---
title: Ověřování rozhraní Partner API
description: Nakonfigurujte nastavení ověřování tak, aby pro ověřování používalo partnerské rozhraní API se službou Azure AD.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c5810678dccc2be1c3c084c901299961d6ba7820
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770347"
---
# <a name="partner-api-authentication"></a><span data-ttu-id="f91a7-103">Ověřování rozhraní Partner API</span><span class="sxs-lookup"><span data-stu-id="f91a7-103">Partner API authentication</span></span>

<span data-ttu-id="f91a7-104">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="f91a7-104">Applies to:</span></span>

- <span data-ttu-id="f91a7-105">Partnerské rozhraní API</span><span class="sxs-lookup"><span data-stu-id="f91a7-105">Partner API</span></span>

<span data-ttu-id="f91a7-106">Partnerské rozhraní API používá k ověřování službu Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f91a7-106">The Partner API utilizes Azure Active Directory (Azure AD) for authentication.</span></span> <span data-ttu-id="f91a7-107">Při interakci s partnerským rozhraním API musíte správně nakonfigurovat aplikaci Azure AD a získat přístupový token.</span><span class="sxs-lookup"><span data-stu-id="f91a7-107">When you interact with the Partner API, you must correctly configure an Azure AD application and obtain an access token.</span></span> <span data-ttu-id="f91a7-108">Přístupové tokeny můžete získat pro přístup k [aplikacím a uživatelům](#application-and-user-access) nebo jenom pro přístup k [aplikacím](#application-only-access).</span><span class="sxs-lookup"><span data-stu-id="f91a7-108">You can obtain access tokens for [application and user access](#application-and-user-access) or [application-only access](#application-only-access).</span></span>

## <a name="application-and-user-access"></a><span data-ttu-id="f91a7-109">Přístup k aplikacím a uživatelům</span><span class="sxs-lookup"><span data-stu-id="f91a7-109">Application and user access</span></span>

<span data-ttu-id="f91a7-110">Tato metoda se doporučuje pro nastavení **aplikace a přístupu uživatelů** k rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="f91a7-110">This method is recommended to set up **application and user access** to the API.</span></span>

1. <span data-ttu-id="f91a7-111">Přihlaste se na [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f91a7-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f91a7-112">Vyberte službu **Azure Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="f91a7-112">Choose the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="f91a7-113">Zvolte **Registrace aplikací** a pak zvolte **Nová registrace aplikace**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-113">Choose **App registrations**, then choose **New application registration**.</span></span>
4. <span data-ttu-id="f91a7-114">Vytvořte novou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f91a7-114">Create your new application.</span></span> <span data-ttu-id="f91a7-115">Jako **Typ aplikace** vyberte **nativní**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-115">For **Application type**, select **Native**.</span></span> <span data-ttu-id="f91a7-116">Zadejte název a adresu URL a pak vyberte **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-116">Provide a name and URL, then select **Create**.</span></span>
5. <span data-ttu-id="f91a7-117">Pro aplikaci vyberte **oprávnění rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="f91a7-117">Choose **API permissions** for the application.</span></span> <span data-ttu-id="f91a7-118">Na obrazovce **požádat o oprávnění API** zvolte **Přidat oprávnění** a pak zvolte **rozhraní API moje organizace používá** .</span><span class="sxs-lookup"><span data-stu-id="f91a7-118">On the **Request API permissions** screen, choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="f91a7-119">Vyhledejte rozhraní API pro *partnera Microsoftu* (*Microsoft Dev Center*) ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="f91a7-119">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Snímek obrazovky s oprávněními rozhraní API pro vyžádání pomocí hledání rozhraní API pro partnery Microsoftu](../images/SearchGatewayApi.png)

7. <span data-ttu-id="f91a7-121">Nastavte **delegovaná oprávnění** k **partnerskému centru**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-121">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Snímek obrazovky s konfigurací delegovaných oprávnění pro rozhraní API partnera Microsoftu](../images/SelectUserPermission.png)
    
8. <span data-ttu-id="f91a7-123">Vyhledejte rozhraní API () *partnera Microsoftu* (*Microsoft Partner Center*) `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` .</span><span class="sxs-lookup"><span data-stu-id="f91a7-123">Search for the *Microsoft Partner* (*Microsoft Partner Center*) API (`fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd`).</span></span>

    ![Snímek obrazovky s oprávněními rozhraní API pro vyžádání pomocí hledání rozhraní API partnerského centra Microsoftu](../images/SearchPCApi.png)
    
9. <span data-ttu-id="f91a7-125">Vyberte **Partnerské centrum Microsoftu** a zaškrtněte **user_impersonation**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-125">Select **Microsoft Partner Center** and check **user_impersonation**.</span></span>

10. <span data-ttu-id="f91a7-126">Nastavte **delegovaná oprávnění** k **partnerskému centru**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-126">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Snímek obrazovky s konfigurací delegovaných oprávnění pro rozhraní API partnerského centra Microsoftu](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a><span data-ttu-id="f91a7-128">Přístup jen pro aplikace</span><span class="sxs-lookup"><span data-stu-id="f91a7-128">Application-only access</span></span>

<span data-ttu-id="f91a7-129">Tato metoda se doporučuje pro nastavení **přístupu pouze k aplikacím** do rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="f91a7-129">This method is recommended for **application-only access** setup to the APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f91a7-130">V aplikaci Azure AD musíte zadat ID aplikace, klíč aplikace a ID adresáře.</span><span class="sxs-lookup"><span data-stu-id="f91a7-130">You must provide the application ID, application key, and directory ID from your Azure AD application.</span></span>

1. <span data-ttu-id="f91a7-131">Přihlaste se na [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f91a7-131">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f91a7-132">Vyberte službu **Azure Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="f91a7-132">Select the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="f91a7-133">Zvolte **Registrace aplikací** a pak vyberte **Nová registrace aplikace**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-133">Choose **App registrations**, then select **New application registration**.</span></span>
4. <span data-ttu-id="f91a7-134">Vytvořte novou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f91a7-134">Create your new application.</span></span> <span data-ttu-id="f91a7-135">Jako **Typ aplikace** vyberte **Webová aplikace/rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-135">For **Application type**, choose **Web app/API**.</span></span> <span data-ttu-id="f91a7-136">Zadejte **název** a **adresu URL** aplikace.</span><span class="sxs-lookup"><span data-stu-id="f91a7-136">Enter a an application **name** and **URL**.</span></span> <span data-ttu-id="f91a7-137">Potom zvolte **Create** (Vytvořit).</span><span class="sxs-lookup"><span data-stu-id="f91a7-137">Then choose **Create**.</span></span>
5. <span data-ttu-id="f91a7-138">Pro aplikaci vyberte **oprávnění rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="f91a7-138">Choose **API permissions** for the application.</span></span> <span data-ttu-id="f91a7-139">Zvolte **Přidat oprávnění** a pak zvolte **rozhraní API, které má moje organizace používat** .</span><span class="sxs-lookup"><span data-stu-id="f91a7-139">Choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="f91a7-140">Vyhledejte rozhraní API pro *partnera Microsoftu* (*Microsoft Dev Center*) ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="f91a7-140">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Snímek obrazovky s oprávněními rozhraní API pro vyžádání pomocí hledání rozhraní API pro partnery Microsoftu](../images/SearchGatewayApi.png)

7. <span data-ttu-id="f91a7-142">Nastavte **delegovaná oprávnění** k **partnerskému centru**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-142">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Snímek obrazovky s konfigurací delegovaných oprávnění pro rozhraní API partnera Microsoftu](../images/SelectUserPermission.png)

8. <span data-ttu-id="f91a7-144">U aplikace, kterou jste zaregistrovali, zvolte **vlastnosti** a pak vyberte **Kopírovat ID aplikace**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-144">For the application you registered, choose **Properties** and then select **copy the Application ID**.</span></span>
9. <span data-ttu-id="f91a7-145">Zvolte **Nastavení** a pak zvolte **certifikáty & tajných** kódů.</span><span class="sxs-lookup"><span data-stu-id="f91a7-145">Choose **Settings**, then choose **Certificates & Secrets**.</span></span> <span data-ttu-id="f91a7-146">Vyberte možnost **nový tajný klíč klienta** a nastavte **vypršení platnosti**  na hodnotu **nikdy nevyprší**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-146">Choose **New Client Secret** and set the **Expiration**  to **Never expires**.</span></span> <span data-ttu-id="f91a7-147">Pak zvolte **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-147">Then choose **Save**.</span></span>
10. <span data-ttu-id="f91a7-148">V nabídce **klíče** vyberte možnost **zkopírovat hodnotu klíče**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-148">On the **Keys** menu, choose **Copy the key value**.</span></span> <span data-ttu-id="f91a7-149">Uloží kopii této hodnoty.</span><span class="sxs-lookup"><span data-stu-id="f91a7-149">Save a copy of this value.</span></span>

> [!WARNING]
> <span data-ttu-id="f91a7-150">Nezapomeňte uložit kopii hodnoty klíče pro klíč, který jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="f91a7-150">Be sure to save a copy of the key value for the key you created.</span></span> <span data-ttu-id="f91a7-151">Tuto hodnotu klíče budete muset později použít k získání tokenu.</span><span class="sxs-lookup"><span data-stu-id="f91a7-151">You will need to use this key value later to obtain a token.</span></span>

## <a name="partner-consent"></a><span data-ttu-id="f91a7-152">Souhlas partnera</span><span class="sxs-lookup"><span data-stu-id="f91a7-152">Partner consent</span></span>

<span data-ttu-id="f91a7-153">Na portálu pro správu Azure vyberte **podnikové aplikace**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-153">In the Azure management portal, select **Enterprise applications**.</span></span> <span data-ttu-id="f91a7-154">Vyhledejte aplikaci, kterou jste vytvořili v předchozí části, a vyberte ji.</span><span class="sxs-lookup"><span data-stu-id="f91a7-154">Search for the application you created in the previous section, and select that application.</span></span> <span data-ttu-id="f91a7-155">Vyberte **oprávnění** a pak vyberte **udělit souhlas správce pro partnerský účet**.</span><span class="sxs-lookup"><span data-stu-id="f91a7-155">Select **Permissions** , then select **Grant Admin Consent for Partner Account**.</span></span>
