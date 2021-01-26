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
# <a name="partner-api-authentication"></a>Ověřování rozhraní Partner API

Platí pro:

- Partnerské rozhraní API

Partnerské rozhraní API používá k ověřování službu Azure Active Directory (Azure AD). Při interakci s partnerským rozhraním API musíte správně nakonfigurovat aplikaci Azure AD a získat přístupový token. Přístupové tokeny můžete získat pro přístup k [aplikacím a uživatelům](#application-and-user-access) nebo jenom pro přístup k [aplikacím](#application-only-access).

## <a name="application-and-user-access"></a>Přístup k aplikacím a uživatelům

Tato metoda se doporučuje pro nastavení **aplikace a přístupu uživatelů** k rozhraní API.

1. Přihlaste se na [Azure Portal](https://portal.azure.com/).
2. Vyberte službu **Azure Active Directory** .
3. Zvolte **Registrace aplikací** a pak zvolte **Nová registrace aplikace**.
4. Vytvořte novou aplikaci. Jako **Typ aplikace** vyberte **nativní**. Zadejte název a adresu URL a pak vyberte **vytvořit**.
5. Pro aplikaci vyberte **oprávnění rozhraní API** . Na obrazovce **požádat o oprávnění API** zvolte **Přidat oprávnění** a pak zvolte **rozhraní API moje organizace používá** .
6. Vyhledejte rozhraní API pro *partnera Microsoftu* (*Microsoft Dev Center*) ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Snímek obrazovky s oprávněními rozhraní API pro vyžádání pomocí hledání rozhraní API pro partnery Microsoftu](../images/SearchGatewayApi.png)

7. Nastavte **delegovaná oprávnění** k **partnerskému centru**.

    ![Snímek obrazovky s konfigurací delegovaných oprávnění pro rozhraní API partnera Microsoftu](../images/SelectUserPermission.png)
    
8. Vyhledejte rozhraní API () *partnera Microsoftu* (*Microsoft Partner Center*) `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` .

    ![Snímek obrazovky s oprávněními rozhraní API pro vyžádání pomocí hledání rozhraní API partnerského centra Microsoftu](../images/SearchPCApi.png)
    
9. Vyberte **Partnerské centrum Microsoftu** a zaškrtněte **user_impersonation**.

10. Nastavte **delegovaná oprávnění** k **partnerskému centru**.

    ![Snímek obrazovky s konfigurací delegovaných oprávnění pro rozhraní API partnerského centra Microsoftu](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a>Přístup jen pro aplikace

Tato metoda se doporučuje pro nastavení **přístupu pouze k aplikacím** do rozhraní API.

> [!IMPORTANT]
> V aplikaci Azure AD musíte zadat ID aplikace, klíč aplikace a ID adresáře.

1. Přihlaste se na [Azure Portal](https://portal.azure.com/).
2. Vyberte službu **Azure Active Directory** .
3. Zvolte **Registrace aplikací** a pak vyberte **Nová registrace aplikace**.
4. Vytvořte novou aplikaci. Jako **Typ aplikace** vyberte **Webová aplikace/rozhraní API**. Zadejte **název** a **adresu URL** aplikace. Potom zvolte **Create** (Vytvořit).
5. Pro aplikaci vyberte **oprávnění rozhraní API** . Zvolte **Přidat oprávnění** a pak zvolte **rozhraní API, které má moje organizace používat** .
6. Vyhledejte rozhraní API pro *partnera Microsoftu* (*Microsoft Dev Center*) ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Snímek obrazovky s oprávněními rozhraní API pro vyžádání pomocí hledání rozhraní API pro partnery Microsoftu](../images/SearchGatewayApi.png)

7. Nastavte **delegovaná oprávnění** k **partnerskému centru**.

    ![Snímek obrazovky s konfigurací delegovaných oprávnění pro rozhraní API partnera Microsoftu](../images/SelectUserPermission.png)

8. U aplikace, kterou jste zaregistrovali, zvolte **vlastnosti** a pak vyberte **Kopírovat ID aplikace**.
9. Zvolte **Nastavení** a pak zvolte **certifikáty & tajných** kódů. Vyberte možnost **nový tajný klíč klienta** a nastavte **vypršení platnosti**  na hodnotu **nikdy nevyprší**. Pak zvolte **Uložit**.
10. V nabídce **klíče** vyberte možnost **zkopírovat hodnotu klíče**. Uloží kopii této hodnoty.

> [!WARNING]
> Nezapomeňte uložit kopii hodnoty klíče pro klíč, který jste vytvořili. Tuto hodnotu klíče budete muset později použít k získání tokenu.

## <a name="partner-consent"></a>Souhlas partnera

Na portálu pro správu Azure vyberte **podnikové aplikace**. Vyhledejte aplikaci, kterou jste vytvořili v předchozí části, a vyberte ji. Vyberte **oprávnění** a pak vyberte **udělit souhlas správce pro partnerský účet**.
