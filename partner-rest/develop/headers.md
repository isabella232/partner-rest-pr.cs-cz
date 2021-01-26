---
title: Záhlaví REST rozhraní API pro partnery
description: REST API partner podporuje následující hlavičky žádosti a odpovědi HTTP.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 955cab07da7f3a386690e18042165015906d864a
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770327"
---
# <a name="partner-rest-api-headers"></a>Hlavičky REST API partnerů

Partnerská REST API podporuje následující hlavičky požadavků a odpovědí HTTP.

> [!NOTE]
> Ne všechna volání rozhraní API přijímají všechny hlavičky.

## <a name="request-headers"></a>Hlavičky požadavku

REST API partner podporuje následující hlavičky požadavků HTTP.

| Hlavička                       | Typ hodnoty | Description                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| Autorizace           | řetězec     | Povinná hodnota. Autorizační token v tokenu nosiče formuláře &lt; &gt; .                    |
| Přijmout                  | řetězec     | Určuje typ žádosti a odpovědi "Application/JSON".                           |
| klient-požadavek-ID         | Identifikátor GUID       | Povinná hodnota. Jedinečný identifikátor pro volání, který je vhodný v protokolech a trasování sítě pro řešení chyb. Hodnota by měla být resetována pro každé volání. Všechny operace by měly zahrnovat tuto hlavičku. |
| If-Match:                    | řetězec     | Používá se pro řízení souběžnosti. Některá volání rozhraní API vyžadují předání značky ETag přes hlavičku If-Match. Značka ETag je obvykle na prostředku a proto vyžaduje, abyste získali nejnovější. |

## <a name="response-headers"></a>Hlavičky odpovědi

Následující hlavičky HTTP odpovědi mohou být vráceny partnerským REST API.

| Hlavička                    | Typ hodnoty | Description                                                                                                               |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| Přijmout                | řetězec     | Určuje typ žádosti a odpovědi "Application/JSON".                                     |
| ID žádosti        | Identifikátor GUID       | Jedinečný identifikátor pro volání, který slouží k zajištění ID-účinnosti. V případě časového limitu by volání opakování mělo zahrnovat stejnou hodnotu. Po přijetí odpovědi (úspěch nebo obchodní selhání) by měla být hodnota pro další volání resetována. |
| klient-požadavek-ID| Identifikátor GUID| Jedinečný identifikátor pro volání, užitečné protokoly a trasování sítě pro řešení chyb. Hodnota by měla být resetována pro každé volání. Všechny operace by měly zahrnovat tuto hlavičku.                                                |
| x-MS-AGS-Diagnostics   | řetězec | Řetězec, který obsahuje diagnostické informace ze služby.
| časové razítko|řetězec | Časové razítko požadavku při volání rozhraní API
|Značk |řetězec | Značka ETag prostředku
