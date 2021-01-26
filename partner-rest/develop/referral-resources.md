---
title: Zdroje informací o referenčních seznamech
description: Referenční materiály reprezentují prodejní zájemce přímo od zákazníka, Microsoftu nebo jiného partnera.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 08438d208da57a4df40aeb609b14b6b6a6128d45
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770325"
---
# <a name="referral-resources"></a>Zdroje informací o referenčních seznamech

Platí pro:

- Partnerské centrum

Tyto prostředky reprezentují prodejní zájemce přímo od zákazníka, Microsoftu nebo jiného partnera.

## <a name="referral"></a>Jí

Představuje odkaz.

| Vlastnost              | Typ                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | řetězec                                            | ID pro tento odkaz.                                                                                         |
| EngagementId          | řetězec                                            | EngagementID pro tento odkaz. K jednomu EngagementID může být přidruženo několik odkazů.                 |
| Name                  | řetězec                                            | Název odkazu                 |
| ExternalReferenceId   | řetězec                                            | Externí identifikátor pro odkaz Příklad: Uložte si vlastní ID zájemce nebo příležitosti pro Dynamics 365.                    |
| CreatedDateTime       | řetězec ve formátu data a času UTC                    | Datum vytvoření odkazu                                                                                |
| UpdatedDateTime       | řetězec ve formátu data a času UTC                    | Datum poslední aktualizace odkazu                                                                           |
| ExpirationDateTime    | řetězec ve formátu data a času UTC                    | Datum, po jehož uplynutí bude platnost odkazu vypršet.                                                                                |
| Status                | [ReferralStatus](referral-resources.md#referralstatus)      | [Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu. |
| SubStatus          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | [Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav dílčího odkazu. |
| StatusReason          | řetězec                                            | Popisná zpráva o stavu Příklad: Proč byl odkaz ztracen? |
| ReferralType          | [ReferralType](referral-resources.md#referraltype)          | Představuje typ odkazu.                                                                                     |
| Qualification         | [ReferralQualification](referral-resources.md#referralqualification)| Představuje kvalitu odkazu.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | Informace o zákazníkovi.                                                                                     |
| Souhlas               | [Souhlas](referral-resources.md#consent)                    | Příznaky souhlasu týkající se sdílení informací s ostatními organizacemi a jejich umožnění kontaktování uživatelů         |
| Podrobnosti               | [ReferralDetails](referral-resources.md#referraldetails)    | Podrobnosti o zákazníkovi, poznámky, hodnota obchodu, datum ukončení měny.                                                                |
| Tým                  | [Člen](referral-resources.md#member)                      | Představuje uživatele v organizacích, které jsou zapojeny.                                |
| InviteContext         | [InviteContext](referral-resources.md#invitecontext)        | Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.  |
| Značk                  | řetězec                                            | Značky ETag jsou používány a jsou požadovány pro kontrolu souběžnosti při aktualizaci prostředků. |
| Cíl         | [ReferralTarget](referral-resources.md#target)        | Představuje další informace, které může uživatel poskytnout při pozvání jiné organizace do partnerského zapojení.  |

## <a name="referralstatus"></a>ReferralStatus

[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu.

| Hodnota           | Description                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| Žádná            |                                                                                             |
| Nová             | Představuje nový odkaz.                                                                 |
| Aktivní          | Představuje aktivní odkaz.                                                             |
| Uzavřeno          | Představuje uzavřený odkaz.                                                              |

## <a name="referralsubstatus"></a>ReferralSubstatus

[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu.

| Hodnota           | Description                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| Žádná            |                                                                                            |
| Čekající         | Představuje nový odkaz, který čeká na vyřízení.                                                 |
| Přijato        | Představuje nový odkaz, který byl přijat.                   |
| Přijato        | Představuje aktivní odkaz, který byl přijat.                                                    |
| Získání             | Představuje uzavřený odkaz, který byl získán.                                            |
| Ztráty            | Představuje uzavřený odkaz, který byl ztracen.                                           |
| Odmítnuto        | Představuje uzavřený odkaz, který byl odmítnut.                                       |
| Platnost vypršela         | Představuje uzavřený odkaz, jehož platnost vypršela.                                             |

### <a name="status--substatus-transition-states"></a>Stavový & stav přechodu dílčího stavu

| Status                | Povolený přechod stavu     | Povolený dílčí stav                |
|-----------------------|-------------------------------|---------------------------------------|
| Nová                   | Nové, aktivní, uzavřené           | Čeká na vyřízení, přijato                     |
| Aktivní                | Aktivní, uzavřeno                | Přijato                              |
| Uzavřeno                | Uzavřeno                        | Výhra, ztraceno, odmítnuto, vypršela platnost          |

## <a name="referraltype"></a>ReferralType

[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují typ odkazu.

| Vlastnost              | Popis                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| Shared                | Představuje odkaz, ve kterém budou všechny zúčastněné strany spolupracovat na uzavření.  |
| Víjí           | Představuje odkaz, ve kterém budou dvě strany spolupracovat na uzavření.           |

## <a name="referralqualification"></a>ReferralQualification

[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují stav odkazu.

| Hodnota                | Description                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| Žádná                 | Představuje odkaz, který nemá přidruženou žádnou míru kvality.                               |
| Direct               | Představuje odkaz, který byl vytvořen přímo zákazníkem.                         |
| MarketingQualified   | Představuje odkaz, který byl vygenerován prostřednictvím Microsoft Marketing Automation Systems.   |
| SalesQualified       | Představuje odkaz od programu Microsoft Sales agent.                                         |

## <a name="customerprofile"></a>CustomerProfile

Obsahuje kontaktní informace zákazníka.

| Vlastnost | Typ                                                   | Popis                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| Název     | řetězec                                                 | Název organizace zákazníka                        |
| Adresa  | [Adresa](referral-resources.md#address)                         | Adresa zákazníka.                           |
| Velikost     | řetězec                                                 | Počet zaměstnanců v organizaci pro zákazníky. |
| Tým     | [Člen](referral-resources.md#member)                           | Kontakty pro organizaci zákazníka.            |
| Identifikační      | [CustomerProfileType](referral-resources.md#customerprofiletype) | [Pole](https://docs.microsoft.com/dotnet/api/system.array) hodnot, které označují externí ID pro zákazníka.                        |

## <a name="customerprofiletype"></a>CustomerProfileType

Obsahuje externí ID pro zákazníka.

| Vlastnost | Typ   | Description                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Duns     | řetězec | [Telefonické připojení & Bradstreet číslo](https://www.dnb.com/duns-number.html) zákazníka. |
| Externí | řetězec | ID zákazníka, které je pro vaši organizaci jedinečné.                                            |

## <a name="address"></a>Adresa

Adresa, která se má použít pro zákazníka

| Vlastnost     | Typ   | Description                                                |
|--------------|--------|------------------------------------------------------------|
| AddressLine1 | řetězec | První řádek adresy                             |
| AddressLine2 | řetězec | Druhý řádek adresy. Tato vlastnost je nepovinná. |
| City         | řetězec | Město.                                                  |
| State        | řetězec | Stav                                                 |
| PostalCode   | řetězec | Poštovní směrovací číslo nebo PSČ                                |
| Země      | řetězec | Země nebo oblast ve [formátu kódu země ISO](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2)             |
| Oblast       | řetězec | Oblast.                                                |

## <a name="member"></a>Člen

Popisuje kontaktní informace pro konkrétního jednotlivce.

| Vlastnost    | Typ   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | řetězec | Křestní jméno kontaktu    |
| LastName    | řetězec | Příjmení kontaktu     |
| PhoneNumber | řetězec | Telefonní číslo kontaktu  |
| E-mail       | řetězec | E-mailová adresa kontaktu |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | Preference kontaktu pro příjem e-mailových oznámení |

## <a name="contactpreference"></a>ContactPreference

Popisuje předvolby kontaktu pro příjem e-mailových oznámení.

| Vlastnost    | Typ   | Description                  |
|-------------|--------|------------------------------|
| Národní prostředí   | řetězec | Národní prostředí e-mailového oznámení Podporují se [AllCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures), [NeutralCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures)a [SpecificCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures) .  |
| DisableNotifications    | bool | Zakáže e-mailová oznámení pro uživatele.     |

## <a name="consent"></a>Souhlas

Příznaky souhlasu týkající se sdílení informací s ostatními organizacemi a jejich umožnění kontaktování uživatelů

| Vlastnost                                         | Typ      | Description                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | boolean   | Označuje souhlas se sdílením identifikovatelných osobních údajů (PII) s ostatními.             |
| ConsentToContact                                 | boolean   | Označuje souhlas se kontaktními uživateli.  |

## <a name="invitecontext"></a>InviteContext

Další informace, které je možné sdílet při pozvání jiné organizace.

| Vlastnost              | Typ                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Poznámky                 | řetězec                                                     | Další poznámky k přijímající organizaci                |
| InvitedBy | [InvitedBy](referral-resources.md#invitedby)                                     | ID organizace, která odeslala odkaz.                                   |

## <a name="invitedby"></a>InvitedBy

Další informace, které je možné sdílet při pozvání jiné organizace.

| Vlastnost              | Typ                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| OrganizationId        | řetězec                                                     | ID organizace, která odeslala odkaz.                |
| OrganizationName      | řetězec                                                     | Název organizace, která odeslala odkaz.                                   |

## <a name="referraldetails"></a>ReferralDetails

Představuje podrobnosti odkazu.

| Vlastnost              | Typ                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Poznámky                 | řetězec                                                     | Další poznámky k přijímající organizaci                |
| DealValue             | decimal                                                    | Hodnota odkazu                                    |
| Měna              | řetězec                                                    | [Symbol měny ISO 4217](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | řetězec ve formátu data a času UTC                         | Datum, kdy zákazník hledá uzavření                           |
| Požadavky          | [ReferralRequirements](referral-resources.md#referralrequirements)   | Odvětví, produkty, typy služeb a řešení, o kterých se zákazník zajímá.|

## <a name="referralrequirements"></a>ReferralRequirements

Obsahuje požadavky zákazníka.

| Vlastnost        | Typ                                                         | Description                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Obory      | [Tag](referral-resources.md#tag)                                       | Odvětví, kterých se zákazník zajímá.        |
| Produkty        | [Tag](referral-resources.md#tag)                                       | Produkty, na které má zákazník zájem.          |
| Služby        | [Tag](referral-resources.md#tag)                                       | Služby, kterých se zákazník zajímá.          |
| Řešení       | [SolutionTag](referral-resources.md#solutiontag)                       | Řešení, se kterými se zákazník zajímá.                             |

## <a name="solutiontag"></a>SolutionTag

Obsahuje podrobnosti o řešení.

| Vlastnost        | Typ                                         | Description                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | řetězec                                       | ID řešení        |
| Name            | řetězec                                       | Název řešení.          |
| SolutionType    | [SolutionType](referral-resources.md#solutiontype)     | Typ řešení.          |

## <a name="solutiontype"></a>SolutionType

[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují typ řešení.

| Vlastnost        | Description                                                     |
|-----------------|-----------------------------------------------------------------|
| Žádná            |                                                                  |
| Kategorie        |  Využívá předdefinované názvy řešení.                            |
| Name            |  Možnost odkazovat na řešení z katalogu Microsoftu. |

## <a name="target"></a>Cíl

Popisuje cíl odkazu.

| Vlastnost                  | Typ                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | řetězec                                                | ID cíle odkazu |
| Typ                      | [ReferralTargetType](referral-resources.md#targettype) | Cílový typ odkazu |

## <a name="targettype"></a>TargetType

[Výčet](https://docs.microsoft.com/dotnet/api/system.enum) s hodnotami, které označují typ řešení.

| Vlastnost        | Description                                                     |
|-----------------|-----------------------------------------------------------------|
| Žádná            |                                                                  |
| BusinessProfileLocation         |  Umístění profilu z partnerského podnikového profilu.                            |
| SolutionProfile            |  Profil řešení partnera. |

## <a name="tag"></a>Značka

Popisuje značku.

| Vlastnost                  | Typ                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | řetězec                                                | ID pro tuto značku                                          |

### <a name="products"></a>Produkty

| Hodnota        |
|-----------------|
|Azure|
|EnterpriseMobilityAndSecurity|
|Výměna|
|DeveloperTools|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX, GP, NAV, SL|
|Microsoft365|
|Office|
|Power BI|
|Project|
|SharePoint|
|SkypeForBusiness|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### <a name="services"></a>Služby

| Hodnota        |
|-----------------|
|ConsultingAndProfessional|
|CustomSolution (ISV)|
|DeploymentOrMigration|
|Hardware|
|Integrace|
|IPServices (ISV)|
|LearningAndCertification|
|Licensing|
|ManagedServices|
|ProjectServices|

### <a name="industries"></a>Obory

| Hodnota        |
|-----------------|
|Zemědělství, lesnictví, & rybolov|
|Komunikační & média|
|Vzdělávání|
|Finanční služby|
|Státní správa|
|Zdravotnictví|
|Pohostinství|
|Výroba|
|Nástroje Power &|
|Veřejná bezpečnost a národní zabezpečení|
|Maloobchodní & spotřební zboží|
|Služby|
|Cestovní & Transport|
|Velkoobchodní & – distribuce|

### <a name="solutions"></a>Řešení

| Hodnota        |
|-----------------|
|AdvancedAnalytics|
|ApplicationIntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |BackupDisasterRecovery|
    |BigData|
    |Blockchain|
    |Chatovací robot|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |CompetitiveDatabaseMigration|
    |Kontejnery|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |Hry|
    |HighPerformanceComputing|
    |HybridStorage|
    |IdentityandAccessManagement|
    |InformationManagement|
    |InternetofThings|
    |MachineLearning|
    |Microserviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |Sítě|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |ServerlessComputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |Vývoj pro|

### <a name="customer-size"></a>Velikost zákazníka

| Hodnota        |
|-----------------|
|    1to50employees|
|    51to500employees|
|    Morethan500employees|
|    1to9employees|
|    10to50employees|
|    51to250employees|
|    251to1000employees|
|    1001to5000employees|
|    5001to10000employees|
|    10001to20000employees|
|    Morethan20000employees|
