---
title: Oracle Eloqua (V2) Source - Overzicht
description: Leer hoe u Oracle Eloqua verbindt met Adobe Experience Platform.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 0%

---

# Overzicht van de bron [!DNL Oracle Eloqua] (V2)

>[!IMPORTANT]
>
>De originele [[!DNL Oracle Eloqua]  (V1) &#x200B;](oracle-eloqua.md) bron is afgekeurd vanaf Januari 2026. Er zijn geen migraties beschikbaar voor deze vervangen bron en u moet uw gegevens opnieuw implementeren met de nieuwe bron [!DNL Oracle Eloqua] (V2).

[!DNL Oracle Eloqua] is een krachtig platform voor marketingautomatisering op bedrijfsniveau dat organisaties helpt, vooral in de B2B-ruimte, om het complexe proces van het beheren van leads te automatiseren en aan te passen en koperstransporten te ordenen. Het fungeert als centraal knooppunt waar marketingteams geavanceerde campagnes kunnen definiëren, implementeren en meten over meerdere digitale kanalen, zodat de vooruitzichten de juiste inhoud krijgen op het moment dat ze het meest betrokken zijn. De gesteunde voorwerpen voor opname door [!DNL Eloqua] zijn **Contacten**, **Rekeningen**, **Campagnes**, en **Activiteiten**. Nadat de eerste opname is voltooid, worden alle gewijzigde gegevens geïmporteerd met een gepland incrementeel proces.

U kunt de [!DNL Eloqua] -bron gebruiken om uw [!DNL Eloqua] -account te verbinden met Adobe Experience Platform. Lees de onderstaande documentatie voor meer informatie.

## Voorbeelden van hoofdletters gebruiken {#use-case-examples}

Hieronder ziet u een tabel met de marketingobjecten die worden ondersteund door de integratie van [!DNL Eloqua] (V2) met Adobe Experience Platform. Voor elk object vindt u een beschrijving samen met voorbeelden van gebruiksgevallen om te illustreren hoe het integreren van [!DNL Eloqua] -gegevens met Real-Time CDP de doeltreffendheid van marketing en de resultaten van de campagne kan verhogen.

| Object | Beschrijving | Voorbeelden van hoofdletters gebruiken |
| --- | --- | --- |
| Contactpersonen | Voeg contactgegevens (zoals naam, e-mail, telefoonnummer, functie) toe aan Real-Time CDP om gedetailleerde, uniforme klantprofielen te maken die alle interacties en afspraken met elk individueel contact consolideren. | **Optimalisering van de Campagne:** door contactgegevens van [!DNL Eloqua] te integreren, kan uw marketing team prioriteitsvooruitzichten identificeren die op recente activiteiten zoals e-mail opent, vormvoorlegging, en gebeurtenisregistraties worden gebaseerd. Real-Time CDP biedt een 360°-weergave van het gedrag van elk contact via e-mail, websites en andere marketingaanraakpunten, zodat marketingteams campagnes op maat kunnen maken en berichten kunnen optimaliseren voor een betere betrokkenheid en conversie. |
| Accounts | Vermeld gegevens op accountniveau (zoals bedrijfsnaam, industrie, bedrijfsomvang, inkomsten, locatie) om op account gebaseerde marketingstrategieën (ABM) in Real-Time CDP te maken en uw team in staat te stellen de juiste organisaties te richten en in te schakelen met relevante berichten. | **ABM Campagnes:** Integrating rekeningsgegevens van [!DNL Eloqua] hulp bouwt gerichte campagnes ABM. Een softwarebedrijf zou bijvoorbeeld de accountgegevens kunnen gebruiken om aangepaste e-mailcampagnes te segmenteren en te sturen naar beleidsmakers in de financiële sector, door nieuwe oplossingen te promoten die zijn toegesneden op hun branche. |
| Campagnes | Verzamel campagnegegevens (zoals campagnemenamen, types, doelstellingen, prestatiesmetriek zoals open tarieven, CTRs) in de Real-Time CDP om campagneprestaties over veelvoudige kanalen te volgen en te optimaliseren. Met deze gegevens kunt u uw investeringsrendement meten en uw strategieën verfijnen. | **Cross-Channel Attribution:** als [!DNL Eloqua] campagnegegevens naar Real-Time CDP verzendt, kunnen de marketing teams de prestaties van campagnes over diverse kanalen (e-mail, sociale media, advertenties, enz.) bekijken, die omzettingen aan de juiste aanrakingspunten en toekomstige die strategieën verfijnen op die insight worden gebaseerd. |
| Activiteiten | Voeg activiteitengegevens toe (zoals e-mail opent, klikt, websitebezoeken, verzonden formulieren, webinar aanwezigheid) om het gedrag in real time en de contacten over verschillende kanalen te volgen, die kansen voor persoonlijke betrokkenheid in real time creëren. | **Echte - tijdZorgen:** door activiteitengegevens van [!DNL Eloqua] te integreren, kan Real-Time CDP gepersonaliseerde e-mail of berichten aan verkoopteams teweegbrengen wanneer een contact met inhoud (zoals het downloaden van een whitepaper of het klikken op een e-mailverbinding) aangaat, die voor geschikte follow-up en betere omzettingsmogelijkheden toestaat. |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Lees de onderstaande secties voor de vereiste configuratie die u moet voltooien voordat u uw bron kunt verbinden met Experience Platform.

### Toepassing instellen voor verificatie

Volg de onderstaande stappen om te leren hoe u uw [!DNL Eloqua] -account kunt instellen en verbinding kunt maken met Experience Platform met behulp van basisverificatie.

Meld u om aan de slag te gaan bij uw [!DNL Eloqua] -instantie als beheerder (of als een gebruiker die toegang heeft om gebruikers, beveiligingsgroepen en toepassingen te maken).

![&#x200B; Mijn dashboard Eloqua.](../../images/tutorials/create/eloqua/admin.png)

Navigeer aan **Montages** > **Uitbreidingen van het Platform** > **de Ontwikkelaar van de Wolk van de App** > **creeer App**. Geef details voor uw app op, zoals de naam, beschrijving, het pictogram en de URL voor OAuth-callback. Selecteer **sparen** wanneer gebeëindigd.

![&#x200B; het paneel van de Ontwikkelaar van de App en Create App knoop in het Eloqua dashboard.](../../images/tutorials/create/eloqua/create-app.png)

| Eigenschap | Beschrijving |
| --- | --- |
| Naam | De naam van uw app. |
| Beschrijving | Een korte beschrijving voor uw app. |
| Pictogram | De URL voor het pictogram. |
| OAuth Callback URL | De URL waarnaar gebruikers moeten worden omgeleid nadat ze de app hebben geïnstalleerd en met [!DNL Eloqua] zijn geverifieerd. |

![&#x200B; creeer app venster in Eloqua.](../../images/tutorials/create/eloqua/new-app.png)

Met uw gecreeerde app, navigeer aan [!DNL Authentication to Eloqua] en wint **identiteitskaart van de Cliënt** en **geheim van de Cliënt** van pas gecreëerde app terug. Deze waarden worden later gebruikt wanneer u verbinding maakt met Experience Platform.

![&#x200B; Cliënt identiteitskaart en cliëntgeheim in Eloqua.](../../images/tutorials/create/eloqua/credentials.png)

De groepen van de veiligheid staan beheerders toe om te controleren welke niveaus van toegangsgebruikers aan activa, eigenschappen, interfaces, etc. hebben. Om een veiligheidsgroep tot stand te brengen, navigeer aan **Montages** > **Gebruikers**. Dan, selecteer het **lusje van de Groep** op het linkerpaneel en selecteer **creeer nieuwe Groep van de Veiligheid**.

![&#x200B; het dashboard van het gebruikersbeheer in Eloqua.](../../images/tutorials/create/eloqua/user-management.png)

Gebruik het venster **[!DNL Security Group Overview]** om een naam en een acroniem voor uw veiligheidsgroep te verstrekken. Zodra gecreeerd, navigeer aan [!DNL Action Permissions] en voeg de [!DNL Consume] API toestemming van de lijst toe en selecteer **sparen**.

![&#x200B; het venster van het overzicht van de veiligheidsgroep in Eloqua.](../../images/tutorials/create/eloqua/security-group-overview.png)

![&#x200B; het selectievenster voor consume API &#x200B;](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>[!DNL Consume] API is een vereiste machtiging, maar u kunt meer machtigingen toevoegen, afhankelijk van uw gebruik van de app.

Om campagnegegevens in te voeren, navigeer aan **uitgeeft de interface van de Gebruiker** en voeg [!DNL Guided Campaigns] aan uw geselecteerde veiligheidsgroep toe.

![&#x200B; de veiligheidsgroep met geleide toegevoegde campagnes.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

U kunt desgewenst een extra gebruiker maken en die gebruiker toevoegen aan een beveiligingsgroep. Voor gedetailleerde stappen, lees de [!DNL Eloqua] documentatie over [&#x200B; creërend een gebruiker &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm) en [&#x200B; toewijzend een gebruiker aan een veiligheidsgroep &#x200B;](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm).

### Vereiste referenties verzamelen

U moet waarden opgeven voor de volgende referenties om [!DNL Eloqua] te verbinden met Experience Platform.

| Credentials | Beschrijving |
| --- | --- |
| Client-id | De openbaar gemaakte id die door [!DNL Eloqua] wordt gebruikt om uw account te identificeren bij het autoriseren naar Experience Platform. |
| Clientgeheim | De vertrouwelijke sleutel die slechts aan de cliënttoepassing en vergunningsserver wordt bekend. Deze sleutel is vereist naast de client-id om uw account te verifiëren. |
| Gebruikersnaam | De gebruikersnaam die aan uw [!DNL Eloqua] -account is gekoppeld. Dit wordt gebruikt om uw toegang te verifiëren en te machtigen. De gebruikersnaam volgt de notatie van `CompanyName\Username` . |
| Wachtwoord | Het wachtwoord dat aan uw [!DNL Eloqua] account is gekoppeld. Samen met uw gebruikersnaam geeft deze toegang tot uw Eloqua-omgeving. |
| Basiseindpunt | Het voorvoegsel van de basis-URI voor verificatie voor [!DNL Eloqua] . Het eindpunt van de basis mag `http://` of `https://` niet opnemen bij verificatie. |

## [!DNL Eloqua] hulplijn voor toewijzing

>[!NOTE]
>
>Hieronder vindt u de deltavelden die intern worden gebruikt voor het laden van incrementele gegevens:
>
>- **Contacten:** `C_DateModified`
>- **Rekeningen:** `M_DateModified`
>- **Activiteit:** `CreatedAt`
>- **de Voorwerpen van de Douane:** `UpdatedAt`
>- **Campagne:** `updatedAt`

De volgende tabellen bevatten gedetailleerde toewijzingen tussen [!DNL Eloqua] bronvelden en de bijbehorende XDM-doelvelden (Experience Data Model) in Experience Platform. Elke rij geeft een overzicht van de transformatielogica, of het veld onveranderlijk is en bevat aanvullende notities om u te helpen begrijpen hoe uw [!DNL Eloqua] -gegevens in Experience Platform worden opgenomen en gestructureerd.

### Accounts

| Eloqua Source-kolom | XDM-doelpad | Notities |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | Dit veld wordt altijd ingesteld op de vaste waarde Eloqua. |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountscore | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | De connector kan uw CRM-instantie-id niet automatisch detecteren. U moet `${CRM_INSTANCE_ID}` handmatig vervangen door uw eigenlijke CRM-instantie-id, ofwel uw Salesforce- of Dynamics-instantie-id. Als `M_SFDCAccountID` aanwezig is tijdens inname, genereert de connector de externe sleutel met behulp van die waarde en voegt deze `\@CRM_INSTANCE_ID.Salesforce` toe. Als dat veld leeg is, gebruikt de connector `M_MSCRMAccountID` en voegt deze `\@CRM_INSTANCE_ID.Dynamics` toe. Als beide velden leeg zijn, wordt dit veld ingesteld op null. |

{style="table-layout:auto"}

### Activiteiten

| Eloqua Source-kolom | XDM-doelpad | Notities |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | Dit veld wordt altijd ingesteld op de vaste waarde Eloqua. |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | Gebaseerd op ActivityType, zal de overeenkomstige Experience Platform eventType waarde worden bevolkt. Voor ExternalActiviteiten is er geen eventType in Experience Platform. U kunt deze toewijzing wijzigen om meer typen af te handelen. |
| `ActivityDate` | tijdstempel | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### Campagnes

| Eloqua Source-kolom | XDM-doelpad | Notities |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | Dit veld wordt altijd ingesteld op de vaste waarde Eloqua. |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `name` | campagneName | |
| `endAt` | campagneEndDate | |
| `startAt` | campagneStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campagneDescription | |
| `currentStatus` | campagneStatus | |
| `campaignType` | campagneType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### Contactpersonen

| Eloqua Source-kolom | XDM-doelpad | Notities |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | Dit veld wordt altijd ingesteld op de vaste waarde Eloqua. |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | `SOURCE_INSTANCE_ID` zal automatisch door de schakelaar worden vervangen. |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | Als de [!DNL Eloqua] -instantie wordt gesynchroniseerd met Salesforce, moet u deze toewijzing behouden. Anders verwijdert u het. De schakelaar heeft geen manier om CRM_INSTANCE_ID te bepalen, zodat moet u $ {CRM_INSTANCE_ID} met uw gesynchroniseerde Salesforce instantie ID vervangen. Deze zelfde afbeelding is op personComponents en extSourceSystemAudit van toepassing, zodat houd allebei. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | Als de [!DNL Eloqua] -instantie wordt gesynchroniseerd met Dynamics, moet u deze toewijzing behouden. Anders verwijdert u het. De schakelaar heeft geen manier om CRM_INSTANCE_ID te bepalen, zodat moet u $ {CRM_INSTANCE_ID} met uw gesynchroniseerde instantie ID van de Dynamiek vervangen. Deze zelfde afbeelding is op personComponents en extSourceSystemAudit van toepassing, zodat houd allebei. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | Als de [!DNL Eloqua] -instantie wordt gesynchroniseerd met Salesforce, moet u deze toewijzing behouden. Anders verwijdert u het. De schakelaar heeft geen manier om CRM_INSTANCE_ID te bepalen, zodat moet u $ {CRM_INSTANCE_ID} met uw gesynchroniseerde Salesforce instantie ID vervangen. Deze zelfde afbeelding is op personComponents en extSourceSystemAudit van toepassing, zodat houd allebei. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Als de [!DNL Eloqua] -instantie wordt gesynchroniseerd met Dynamics, moet u deze toewijzing behouden. Anders verwijdert u het. De schakelaar heeft geen manier om CRM_INSTANCE_ID te bepalen, zodat moet u $ {CRM_INSTANCE_ID} met uw gesynchroniseerde instantie ID van de Dynamiek vervangen. Deze zelfde afbeelding is op personComponents en extSourceSystemAudit van toepassing, zodat houd allebei. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | De schakelaar heeft geen manier om CRM_INSTANCE_ID te bepalen, zodat moet u $ {CRM_INSTANCE_ID} met uw gesynchroniseerde instantieID van CRM, of Salesforce instantie identiteitskaart of de de instantieidentiteitskaart van de Dynamiek vervangen. Deze zelfde afbeelding is op zowel b2b.accountKey als personComponents.sourceAccountKey van toepassing, zodat houd allebei. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | De schakelaar heeft geen manier om CRM_INSTANCE_ID te bepalen, zodat moet u $ {CRM_INSTANCE_ID} met uw gesynchroniseerde instantieID van CRM, of Salesforce instantie identiteitskaart of de de instantieidentiteitskaart van de Dynamiek vervangen. Deze zelfde afbeelding is op zowel b2b.accountKey als personComponents.sourceAccountKey van toepassing, zodat houd allebei. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### Toewijzingsverwijzing naar type activiteit

| Eloqua ActivityType | XDM eventType |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | as-is doorlopen |

{style="table-layout:auto"}

### Variabele plaatsaanduidingen

De toewijzingssjablonen gebruiken de volgende plaatsaanduidingen voor variabelen die worden vervangen wanneer een gegevensstroom wordt uitgevoerd:

| Plaatsaanduiding | Beschrijving | Gebruik |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | Unieke id voor broninstantie Eloqua | Gebruikt in bronsleutels |
| `${CRM_INSTANCE_ID}` | Unieke id voor CRM-systeem (Salesforce/Dynamics) | Wordt gebruikt in externe toetsen |

## Verbinden [!DNL Eloqua] met Experience Platform

Ga door om uw [!DNL Eloqua] bronverbinding in Experience Platform te configureren. Voor een geleidelijke gids bij vestiging de verbinding door UI, verwijs hier naar het [&#x200B; leerprogramma &#x200B;](../../tutorials/ui/create/marketing-automation/eloqua.md). Lees deze zelfstudie voor meer informatie over het verbinden van uw [!DNL Eloqua] -account, het selecteren van gegevens, het toewijzen van velden, het plannen van indelingen en het controleren van uw gegevensstromen.

