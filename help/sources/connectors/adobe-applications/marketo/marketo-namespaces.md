---
keywords: Experience Platform;home;populaire onderwerpen;Marketo-bronaansluiting;naamruimten;schema's
solution: Experience Platform
title: Marketo-naamruimten
topic-legacy: overview
description: Dit document biedt een overzicht van aangepaste naamruimten die zijn vereist voor het maken van een Marketo Engage-bronaansluiting.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 609b951cbde880a9f354b343adb1796def0a812c
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 1%

---

# (bèta) [!DNL Marketo Engage] naamruimten en schema&#39;s

>[!IMPORTANT]
>
>De bron [!DNL Marketo Engage] bevindt zich momenteel in bèta. Het kenmerk en de documentatie worden gewijzigd door het onderwerp.

Dit document bevat informatie over de onderliggende instelling voor B2B-naamruimten en -schema&#39;s die worden gebruikt met [!DNL Marketo Engage] (hierna &quot;[!DNL Marketo]&quot; genoemd). Dit document bevat ook informatie over het instellen van uw Postman-automatiseringsprogramma dat nodig is voor het genereren van [!DNL Marketo] B2B-naamruimten en -schema&#39;s.

## Stel het hulpprogramma [!DNL Marketo] voor automatisch genereren van naamruimte en schema in

De eerste stap in het gebruiken van [!DNL Marketo] namespace en schema auto-generatienut is aan opstelling uw Platform ontwikkelaarsconsole en [!DNL Postman] milieu.

- U kunt de namespace en het schema auto-generatienutsinzameling en milieu van deze [bewaarplaats GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) downloaden.
- Voor informatie bij het gebruiken van Platform APIs met inbegrip van details over hoe te om waarden voor vereiste kopballen te verzamelen en steekproefAPI vraag te lezen, zie de gids op [aan de slag met Platform APIs](../../../../landing/api-guide.md).
- Voor informatie over hoe te om uw geloofsbrieven voor Platform APIs te produceren, zie de zelfstudie over [het voor authentiek verklaren van en het toegang tot van Experience Platform APIs](../../../../landing/api-authentication.md).
- Voor informatie over hoe te opstelling [!DNL Postman] voor Platform APIs, zie de zelfstudie over [vestiging de console van de ontwikkelaar en [!DNL Postman]](../../../../landing/postman.md).

Met een Platform-ontwikkelaarsconsole en [!DNL Postman] opstelling, kunt u nu beginnen de aangewezen milieuwaarden op uw &lt;a1 toe te passen/> milieu.[!DNL Postman]

De volgende tabel bevat voorbeeldwaarden en aanvullende informatie over het vullen van de [!DNL Postman]-omgeving:

| Variabele | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `CLIENT_SECRET` | Een unieke id die wordt gebruikt om uw `{ACCESS_TOKEN}` te genereren. Zie de zelfstudie over [het verifiëren van en de toegang tot van Experience Platform APIs](../../../../landing/api-authentication.md) voor informatie over hoe te om uw `{CLIENT_SECRET}` terug te winnen. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) is een verificatiereferentie die wordt gebruikt om uw {ACCESS_TOKEN} te genereren. Zie de zelfstudie over [het verifiëren van en de toegang tot van Experience Platform APIs](../../../../landing/api-authentication.md) voor informatie over hoe te om uw `{JWT_TOKEN}` te produceren. | `{JWT_TOKEN}` |
| `API_KEY` | Een unieke id die wordt gebruikt om aanroepen van Experience Platform-API&#39;s te verifiëren. Zie de zelfstudie over [het verifiëren van en de toegang tot van Experience Platform APIs](../../../../landing/api-authentication.md) voor informatie over hoe te om uw `{API_KEY}` terug te winnen. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Het toestemmingstoken dat wordt vereist om vraag aan Experience Platform APIs te voltooien. Zie de zelfstudie over [het verifiëren van en de toegang tot van Experience Platform APIs](../../../../landing/api-authentication.md) voor informatie over hoe te om uw `{ACCESS_TOKEN}` terug te winnen. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | De `global` container houdt alle standaardAdobe en de partner van het Experience Platform verstrekte klassen, de groepen van het schemagebied, gegevenstypes, en schema&#39;s. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op `global`. | `global` |
| `PRIVATE_KEY` | Een referentie die wordt gebruikt om uw [!DNL Postman]-instantie te verifiëren voor Experience Platform-API&#39;s. Zie de zelfstudie over het instellen van de ontwikkelaarsconsole en [het instellen van de ontwikkelaarsconsole en [!DNL Postman]](../../../../landing/postman.md) voor instructies over het ophalen van uw {PRIVATE_KEY} . | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Een referentie die wordt gebruikt om te integreren in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Het Identity Management System (IMS) biedt het kader voor verificatie van Adobe-services. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Een onderneming die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden. Zie de zelfstudie over [het instellen van de ontwikkelaarsconsole en [!DNL Postman]](../../../../landing/postman.md) voor instructies over het ophalen van uw `{IMS_ORG}`-informatie. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | De naam van de virtuele sandboxpartitie die u gebruikt. | `prod` |
| `TENANT_ID` | Een id die wordt gebruikt om ervoor te zorgen dat de bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw IMS-organisatie bevinden. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Het URL-eindpunt waarnaar u API-aanroepen maakt. Deze waarde is vast en wordt altijd ingesteld op: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | De unieke id voor uw [!DNL Marketo]-account. Zie de zelfstudie over [het verifiëren van uw  [!DNL Marketo] instantie](./marketo-auth.md) voor informatie over hoe te om uw `munchkinId` terug te winnen. | `123-ABC-456` |
| `sfdc_org_id` | De organisatie-id voor uw [!DNL Salesforce]-account. Zie de volgende [[!DNL Salesforce] handleiding](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) voor meer informatie over het verkrijgen van uw [!DNL Salesforce] organisatie-id. | `00D4W000000FgYJUA0` |
| `msd_org_id` | De organisatie-id voor uw [!DNL Dynamics]-account. Zie de volgende [[!DNL Microsoft Dynamics] handleiding](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) voor meer informatie over het verkrijgen van uw [!DNL Dynamics] organisatie-id. | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` |
| `has_abm` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Scripts uitvoeren

Met uw [!DNL Postman] inzameling en milieu opstelling, kunt u het manuscript door de [!DNL Postman] interface nu in werking stellen.

Selecteer in de interface [!DNL Postman] de hoofdmap van het hulpprogramma voor automatische generator en selecteer **[!DNL Run]** in de bovenste koptekst.

![hoofdmap](../images/marketo/root-folder.png)

De interface [!DNL Runner] verschijnt. Van hier, zorg ervoor dat alle controledozen worden geselecteerd en dan **[!DNL Run Adobe I/O Access Token Generation + Automate Namespace creation]** selecteren.

![loopgenerator](../images/marketo/run-generator.png)

Een succesvol verzoek leidt tot B2B namespaces en schema&#39;s volgens bètaspecificaties.

## [!DNL Marketo] naamruimten

Identiteitsnaamruimten zijn een component van [[!DNL Identity Service]](../../../../identity-service/home.md) die als indicatoren van de context dienen waarop een identiteit betrekking heeft.

Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace. Voor elke nieuwe [!DNL Marketo]-instantie en gegevenssetcombinatie is een nieuwe aangepaste naamruimte vereist. Bijvoorbeeld, vereist een [!DNL Marketo] bronschakelaar die de `programs` dataset opneemt zijn eigen douanespatie, en een andere van de bron Marketo schakelaar die de zelfde dataset opneemt vereist ook zijn eigen nieuwe douannamespace. Zie het [namespaces overzicht](../../../../identity-service/namespaces.md) voor meer informatie.

De naamruimte [!DNL Marketo] wordt gebruikt in de primaire identiteit van de entiteit.

De volgende tabel bevat informatie over de onderliggende set-up voor naamruimten [!DNL Marketo].

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Weergavenaam | Identiteitssymbool | Identiteitstype | Type uitgever | Type emittent | Voorbeeld van Munchkin-id |
| --- | --- | --- | --- | --- | --- |
| `marketo_person_{MUNCHKIN_ID}` | automatisch gegenereerd | `CROSS_DEVICE` | [!DNL Marketo] | `person` | `123-ABC-789` |
| `marketo_company_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_ACCOUNT` | [!DNL Marketo] | `company` | `123-ABC-789` |
| `marketo_opportunity_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY` | [!DNL Marketo] | `opportunity` | `123-ABC-789` |
| `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY_PERSON` | [!DNL Marketo] | `opportunity contact role` | `123-ABC-789` |
| `marketo_program_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN` | [!DNL Marketo] | `program` | `123-ABC-789` |
| `marketo_program_member_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN_MEMBER` | [!DNL Marketo] | `program member` | `123-ABC-789` |
| `marketo_static_list_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_MARKETING_LIST` | [!DNL Marketo] | `static list` | `123-ABC-789` |
| `marketo_static_list_member_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_MARKETING_LIST_MEMBER` | [!DNL Marketo] | `static list member` | `123-ABC-789` |
| `marketo_named_account_{MUNCHKIN_ID}` | automatisch gegenereerd | `B2B_ACCOUNT` | [!DNL Marketo] | `named account` | `123-ABC-789` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Salesforce] naamruimten

Als u aan de [!DNL Salesforce] integratie wordt geabonneerd, wordt [!DNL Salesforce] namespace gebruikt in de secundaire identiteit van de entiteit.

De volgende tabel bevat informatie over de onderliggende set-up voor naamruimten [!DNL Salesforce].

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Weergavenaam | Identiteitssymbool | Identiteitstype | Type uitgever | Type emittent | [!DNL Salesforce] ID-voorbeeld van abonnementsorganisatie |
| --- | --- | --- | --- | --- | --- |
| `salesforce_lead_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `CROSS_DEVICE` | [!DNL Salesforce] | `lead` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] naamruimten

Als u aan de [!DNL Dynamics] integratie wordt geabonneerd, wordt [!DNL Dynamics] namespace gebruikt als secundaire identiteit van de entiteit.

De volgende tabel bevat informatie over de onderliggende set-up voor naamruimten [!DNL Dynamics].

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Weergavenaam | Identiteitssymbool | Identiteitstype | Type uitgever | Type emittent | [!DNL Dynamics] ID-voorbeeld van abonnementsorganisatie |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | automatisch gegenereerd | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] schema&#39;s

Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens.

Voordat gegevens in Platform kunnen worden opgenomen, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. De schema&#39;s bestaan uit een basisklasse en nul of meer groepen van het schemagebied.

Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes en beste praktijken, zie [grondbeginselen van schemacompositie](../../../../xdm/schema/composition.md).

De volgende lijst bevat informatie over de onderliggende opstelling van [!DNL Marketo] schema&#39;s.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Schemanaam | Basisklasse | Veldengroepen | [!DNL Profile] in Schema | Primaire identiteit | Primaire naamruimte | Secundaire identiteit | Secundaire naamruimte voor identiteit | Relatie | Notities |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `[!DNL Marketo] Company {MUNCHKIN_ID}` | XDM Business Account | XDM-bedrijfsaccountgegevens | Ingeschakeld | `accountID` in de basisklasse | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details, veldgroep</li><li>Type: één-op-één</li><li>Referentieschema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| `[!DNL Marketo] Person {MUNCHKIN_ID}` | Afzonderlijk XDM-profiel | <ul><li>XDM Business Person Details</li><li>XDM Business Person-componenten</li><li>IdentityMap</li></ul> | Ingeschakeld | `personID` in de basisklasse | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` van XDM Business Person Details, veldgroep</li><li>`workEmail.address` van XDM Business Person Details, veldgroep</li><li>`identityMap` van de het gebiedsgroep van de Kaart van de Identiteit</ol></li> | <ol><li>`salesforce_lead_{SALESFORCE_ORGANIZATION_ID}`</li><li>Email</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` van XDM Business Person Components, veldgroep</li><li>Type: Veel-op-één</li><li>Referentieschema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_company_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `accountID`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatienaam van referentieschema: Mensen</li></ul> |
| `[!DNL Marketo] Opportunity {MUNCHKIN_ID}` | XDM Business Opportunity | XDM Business Opportunity-gegevens | Ingeschakeld | `opportunityID` in de basisklasse | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: `[!DNL Marketo] Company {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_company_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `accountID`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatienaam van referentieschema: Kansen</li></ul> |
| `[!DNL Marketo] Opportunity Contact Role {MUNCHKIN_ID}` | XDM Business Opportunity Person Relatie | Geen | Ingeschakeld | `opportunityPersonID` in de basisklasse | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Eerste relatie<ul><li>`personID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_person_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `personID`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: Kansen</li></ul>Tweede relatie<ul><li>`opportunityID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `opportunityID`</li><li>Relatienaam uit huidig schema: Opportunity</li><li>Relatienaam van referentieschema: Mensen</li></ul> |
| `[!DNL Marketo] Program {MUNCHKIN_ID}` | XDM Business Campaign | XDM Business Campaign - details | Ingeschakeld | `campaignID` in de basisklasse | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` |
| `[!DNL Marketo] Program Member {MUNCHKIN_ID}` | XDM Business Campaign-lid | XDM Business Campagne Member Details | Ingeschakeld | `campaignMemberID` in de basisklasse | `marketo_program_member_{MUNCHKIN_ID}` | Geen | Geen | Eerste relatie<ul><li>`personID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo Person {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_person_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `personID`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: Programma&#39;s</li></ul>Tweede relatie<ul><li>`campaignID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_program_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `campaignID`</li><li>Relatienaam uit huidig schema: Programma</li><li>Relatienaam van referentieschema: Mensen</li></ul> |
| `[!DNL Marketo] Static List {MUNCHKIN_ID}` | XDM Business Marketing List | Geen | Ingeschakeld | `marketingListID` in de basisklasse | `marketo_static_list_{MUNCHKIN_ID}` | Geen | Geen | Geen | De statische Lijst wordt niet gesynchroniseerd van [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| `[!DNL Marketo] Static List Member {MUNCHKIN_ID}` | Leden van XDM Business Marketing List | Geen | Ingeschakeld | `marketingListMemberID` in de basisklasse | `marketo_static_list_member_{MUNCHKIN_ID}` | Geen | Geen | Eerste relatie<ul><li>`personID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: `[!DNL Marketo] Person {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_person_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `personID`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: Lijsten</li></ul>Tweede relatie<ul><li>`marketingListID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `marketingListID`</li><li>Relatienaam uit huidig schema: Lijst</li><li>Relatienaam van referentieschema: Mensen</li></ul> | Het statische lijstlid wordt niet gesynchroniseerd van [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| `[!DNL Marketo] Named Account {MUNCHKIN_ID}` | XDM Business Account | XDM-bedrijfsaccountgegevens | Ingeschakeld | `accountID` in de basisklasse | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details, veldgroep</li><li>Type: één-op-één</li><li>Referentieschema: `[!DNL Marketo] Named Account {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Activiteit `{MUNCHKIN ID}` | XDM ExperienceEvent | <ul><li>Webpagina bezoeken</li><li>Nieuwe lead</li><li>Regelafstand omzetten</li><li>Toevoegen aan lijst</li><li>Verwijderen uit lijst</li><li>Toevoegen aan opportunity</li><li>Verwijderen uit opportunity</li><li>Formulier ingevuld</li><li>Koppelingsklikken</li><li>E-mail bezorgd</li><li>E-mail geopend</li><li>E-mail geklikt</li><li>E-mail verzonden</li><li>Door e-mail teruggekaatst</li><li>E-mail niet geabonneerd</li><li>Gewijzigde score</li><li>Opportunity bijgewerkt</li><li>Status in gewijzigde campagnevoortgang</li><li>Persoon-id</li><li>Marketo-webURL | Ingeschakeld | `personID` van Person Identifier-veldgroep | `marketo_person_{MUNCHKIN_ID}` | Geen | Geen | Eerste relatie<ul><li>`listOperations.listID` field</li><li>Type: één-op-één</li><li>Referentieschema: `[!DNL Marketo] Static List {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Tweede relatie<ul><li>`opportunityEvent.opportunityID` field</li><li>Type: één-op-één</li><li>Referentieschema: `[!DNL Marketo] Opportunity {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Derde relatie<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Type: één-op-één</li><li>Referentieschema: `[!DNL Marketo] Program {MUNCHKIN_ID}`</li><li>Naamruimte: `marketo_program_{MUNCHKIN_ID}`</li></ul> | De primaire identiteit van `[!DNL Marketo] Activity {MUNCHKIN_ID}` schema is `personID`, die het zelfde als de primaire identiteit van `[!DNL Marketo] Person {MUNCHKIN_ID}` schema is. |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

Leer hoe te om uw [!DNL Marketo] gegevens aan Platform aan te sluiten, zie de zelfstudie op [creërend een bron van Marketo schakelaar in UI](../../../tutorials/ui/create/adobe-applications/marketo.md).
