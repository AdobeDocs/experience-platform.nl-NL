---
keywords: Experience Platform;home;populaire onderwerpen;Marketo-bronaansluiting;naamruimten;schema's
solution: Experience Platform
title: 'Marketo-naamruimten '
topic: overzicht
description: Dit document biedt een overzicht van aangepaste naamruimten die zijn vereist voor het maken van een Marketo Engage-bronaansluiting.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---


# (bèta) [!DNL Marketo Engage] naamruimten en schema&#39;s

>[!IMPORTANT]
>
>De bron [!DNL Marketo Engage] bevindt zich momenteel in bèta. Het kenmerk en de documentatie worden gewijzigd door het onderwerp.

Dit document bevat informatie over de onderliggende instelling voor B2B-naamruimten en -schema&#39;s die worden gebruikt met [!DNL Marketo Engage] (hierna &quot;[!DNL Marketo]&quot; genoemd). Dit document bevat ook informatie over het instellen van uw Postman-automatiseringsprogramma dat nodig is voor het genereren van [!DNL Marketo] B2B-naamruimten en -schema&#39;s.

## Vereisten

Voordat u uw B2B-naamruimten en -schema&#39;s kunt genereren, moet u eerst de ontwikkelaarsconsole van uw Platform en de [!DNL Postman]-omgeving instellen. Zie de zelfstudie over het instellen van de ontwikkelaarsconsole en [!DNL Postman]](../../../../landing/postman.md) voor meer informatie.[

Met een console van de ontwikkelaar van het Platform en [!DNL Postman] opstelling, pas de volgende variabelen op uw [!DNL Marketo] milieu toe:

| Omgevingsvariabele | Voorbeeldwaarde | Notities |
| --- | --- | --- |
| `PRIVATE_KEY` | `{PRIVATE_KEY}` |
| `SANDBOX_NAME` | `prod` |
| `TENANT_ID` | `b2bcdpproductiontest` |
| `munchkinId` | `123-ABC-456 ` | Zie de zelfstudie over [het verifiëren van uw [!DNL Marketo] instance](./marketo-auth.md) voor meer informatie. |
| `sfdc_org_id` | `00D4W000000FgYJUA0` | Zie de volgende [[!DNL Salesforce] handleiding](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) voor meer informatie over het verkrijgen van uw organisatie-id. |
| `msd_org_id` | `f6438fab-67e8-4814-a6b5-8c8dcdf7a98f` | Zie de volgende [[!DNL Microsoft Dynamics] handleiding](https://docs.microsoft.com/en-us/power-platform/admin/determine-org-id-name) voor meer informatie over het verkrijgen van uw organisatie-id. |
| `has_abm` | `false` | Deze waarde wordt ingesteld op `true` als u bent geabonneerd op Account-Based Marketing. |
| `has_msi` | `false` | Deze waarde wordt ingesteld op `true` als u bent geabonneerd op [!DNL Marketo Sales Insight]. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Marketo] naamruimten

Identiteitsnaamruimten zijn een component van [[!DNL Identity Service]](../../../../identity-service/home.md) die als indicatoren van de context dienen waarop een identiteit betrekking heeft.

Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace. Voor elke nieuwe [!DNL Marketo]-instantie en gegevenssetcombinatie is een nieuwe aangepaste naamruimte vereist. Bijvoorbeeld, vereist een [!DNL Marketo] bronschakelaar die de `programs` dataset opneemt zijn eigen douanespatie, en een andere van de bron Marketo schakelaar die de zelfde dataset opneemt vereist ook zijn eigen nieuwe douannamespace. Zie het [namespaces overzicht](../../../../identity-service/namespaces.md) voor meer informatie.

De naamruimte [!DNL Marketo] wordt gebruikt in de primaire identiteit van de entiteit.

De volgende tabel bevat informatie over de onderliggende set-up voor naamruimten [!DNL Marketo].

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

| Weergavenaam | Identiteitssymbool | Identiteitstype | Type uitgever | Type emittent | [!DNL Salesforce] ID-voorbeeld van abonnementsorganisatie |
| --- | --- | --- | --- | --- | --- |
| `salesforce_person_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `CROSS_DEVICE` | [!DNL Salesforce] | `person` | `00DA0000000Hz79` |
| `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_ACCOUNT` | [!DNL Salesforce] | `account` | `00DA0000000Hz79` |
| `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY` | [!DNL Salesforce] | `opportunity` | `00DA0000000Hz79` |
| `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY_PERSON` | [!DNL Salesforce] | `opportunity contact role` | `00DA0000000Hz79` |
| `salesforce_campaign_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN` | [!DNL Salesforce] | `campaign` | `00DA0000000Hz79` |
| `salesforce_campaign_member_{SALESFORCE_ORGANIZATION_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN_MEMBER` | [!DNL Salesforce] | `campaign member` | `00DA0000000Hz79` |

{style=&quot;table-layout:auto&quot;}

### [!DNL Microsoft Dynamics] naamruimten

Als u aan de [!DNL Dynamics] integratie wordt geabonneerd, wordt [!DNL Dynamics] namespace gebruikt als secundaire identiteit van de entiteit.

De volgende tabel bevat informatie over de onderliggende set-up voor naamruimten [!DNL Dynamics].

| Weergavenaam | Identiteitssymbool | Identiteitstype | Type uitgever | Type emittent | [!DNL Salesforce] ID-voorbeeld van abonnementsorganisatie |
| --- | --- | --- | --- | --- | --- |
| `microsoft_person_{DYNAMICS_ID}` | automatisch gegenereerd | `CROSS_DEVICE` | [!DNL Microsoft] | `person` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_account_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_ACCOUNT` | [!DNL Microsoft] | `account` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY` | [!DNL Microsoft] | `opportunity` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_opportunity_contact_connection_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_OPPORTUNITY_PERSON` | [!DNL Microsoft] | `opportunity relationship` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN` | [!DNL Microsoft] | `campaign` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |
| `microsoft_campaign_member_{DYNAMICS_ID}` | automatisch gegenereerd | `B2B_CAMPAIGN_MEMBER` | [!DNL Microsoft] | `campaign member` | `94cahe38-e51h-3d57-a9c6-2edklb7184mh` |

## [!DNL Marketo] schema&#39;s

Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens.

Voordat gegevens in Platform kunnen worden opgenomen, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. Schema&#39;s bestaan uit een basisklasse en nul of meer mixen.

Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes en beste praktijken, zie [grondbeginselen van schemacompositie](../../../../xdm/schema/composition.md).

De volgende lijst bevat informatie over de onderliggende opstelling van [!DNL Marketo] schema&#39;s.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Schemanaam | Basisklasse | Mixins | Primaire identiteit | Primaire naamruimte | Secundaire identiteit | Secundaire naamruimte voor identiteit | Relatie | Notities |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [!DNL Marketo] Bedrijf {MUNCHKIN_ID} | XDM Business Account | XDM-bedrijfsaccountgegevens | `accountID` in de basisklasse | `marketo_company_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details mixen</li><li>Type: één-op-één</li><li>Referentieschema: Marketo Company {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_company_{MUNCHKIN_ID}`</li></ul> |
| [!DNL Marketo] Persoon {MUNCHKIN_ID} | Afzonderlijk XDM-profiel | <ul><li>XDM Business Person Details</li><li>XDM Business Person-componenten</li></ul> | `personID` in de basisklasse | `marketo_person_{MUNCHKIN_ID}` | <ol><li>`extSourceSystemAudit.externalID` van XDM Business Person Details-mix</li><li>`workEmail.address` van XDM Business Person Details-mix</li><li>`identityMap` van identiteitskaartmix</ol></li> | <ol><li>`salesforce_person_{SALESFORCE_ORGANIZATION_ID}`</li><li>Email</li><li>ECID</li></ol> | <ul><li>`personComponents.sourceAccountID` van XDM Business Person Components, mix</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo Company {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_company_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `accountID`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatienaam van referentieschema: Mensen</li></ul> |
| [!DNL Marketo] Opportunity {MUNCHKIN_ID} | XDM Business Opportunity | XDM Business Opportunity-gegevens | `opportunityID` in de basisklasse | `marketo_opportunity_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_opportunity_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo Company {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_company_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `accountID`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatienaam van referentieschema: Kansen</li></ul> |
| [!DNL Marketo] Functie contactpersoon opportunity {MUNCHKIN_ID} | XDM Business Opportunity Person Relatie | Geen | `opportunityPersonID` in de basisklasse | `marketo_opportunity_contact_role_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_opportunity_contact_role_{SALESFORCE_ORGANIZATION_ID}` | Eerste relatie<ul><li>`personID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo Person {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_person_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `personID`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: Kansen</li></ul>Tweede relatie<ul><li>`opportunityID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo Opportunity {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_opportunity_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `opportunityID`</li><li>Relatienaam uit huidig schema: Opportunity</li><li>Relatienaam van referentieschema: Mensen</li></ul> |
| [!DNL Marketo] Program {MUNCHKIN_ID} | XDM Business Campaign | XDM Business Campaign - details | `campaignID` in de basisklasse | `marketo_program_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_campaign_SALESFORCE_ORGANIZATION_ID}` |
| [!DNL Marketo] Program Member {MUNCHKIN_ID} | XDM Business Campaign-lid | XDM Business Campagne Member Details | `campaignMemberID` in de basisklasse | `marketo_program_member_{MUNCHKIN_ID}` | Geen | Geen | Eerste relatie<ul><li>`personID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo Person {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_person_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `personID`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: Programma&#39;s</li></ul>Tweede relatie<ul><li>`campaignID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo-programma {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_program_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: campagneID</li><li>Relatienaam uit huidig schema: Programma</li><li>Relatienaam van referentieschema: Mensen</li></ul> |
| [!DNL Marketo] Statische lijst {MUNCHKIN_ID} | XDM Business Marketing List | Geen | `marketingListID` in de basisklasse | `marketo_static_list_{MUNCHKIN_ID}` | Geen | Geen | Geen | Statische lijst wordt niet gesynchroniseerd vanuit [!DNL Salesforce] en heeft daarom geen secundaire identiteit |
| [!DNL Marketo] Lid statische lijst {MUNCHKIN_ID} | Leden van XDM Business Marketing List | Geen | `marketingListMemberID` in de basisklasse | `marketo_static_list_member_{MUNCHKIN_ID}` | Geen | Geen | Eerste relatie<ul><li>`personID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Marketo Person {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_person_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `personID`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: Lijsten</li></ul>Tweede relatie<ul><li>`marketingListID` in de basisklasse</li><li>Type: Veel-op-één</li><li>Referentieschema: Statische Marketo-lijst {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_static_list_{MUNCHKIN_ID}`</li><li>Eigenschap van bestemming: `marketingListID`</li><li>Relatienaam uit huidig schema: Lijst</li><li>Relatienaam van referentieschema: Mensen</li></ul> |
| [!DNL Marketo] Benoemd account {MUNCHKIN_ID} | XDM Business Account | XDM-bedrijfsaccountgegevens | `accountID` in de basisklasse | `marketo_named_account_{MUNCHKIN_ID}` | `extSourceSystemAudit.externalID` in de basisklasse | `salesforce_account_{SALESFORCE_ORGANIZATION_ID}` | <ul><li>`accountParentID` in XDM Business Account Details mixen</li><li>Type: één-op-één</li><li>Referentieschema: Benoemd Marketo-account {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_named_account_{MUNCHKIN_ID}` |
| [!DNL Marketo] Activity {MUNCHKIN ID} | XDM Experience Event | <ul><li>Webpagina bezoeken</li><li>Nieuwe lead</li><li>Regelafstand omzetten</li><li>Toevoegen aan lijst</li><li>Verwijderen uit lijst</li><li>Toevoegen aan opportunity</li><li>Verwijderen uit opportunity</li><li>Formulier ingevuld</li><li>Koppelingsklikken</li><li>E-mail bezorgd</li><li>E-mail geopend</li><li>E-mail geklikt</li><li>E-mail verzonden</li><li>Door e-mail teruggekaatst</li><li>E-mail niet geabonneerd</li><li>Gewijzigde score</li><li>Opportunity bijgewerkt</li><li>Status in gewijzigde campagnevoortgang</li><li>Persoon-id</li><li>Marketo-webURL | `personID` van Person Identifier-mix | marketo_person_{MUNCHKIN_ID} | Geen | Geen | Eerste relatie<ul><li>`listOperations.listID` field</li><li>Type: één-op-één</li><li>Referentieschema: Statische Marketo-lijst {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_static_list_{MUNCHKIN_ID}`</li></ul>Tweede relatie<ul><li>`opportunityEvent.opportunityID` field</li><li>Type: één-op-één</li><li>Referentieschema: Marketo Opportunity {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_opportunity_{MUNCHKIN_ID}`</li></ul>Derde relatie<ul><li>`leadOperation.campaignProgression.campaignID` field</li><li>Type: één-op-één</li><li>Referentieschema: Marketo-programma {MUNCHKIN_ID}</li><li>Naamruimte: `marketo_program_{MUNCHKIN_ID}`</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Alle schema&#39;s zijn ingeschakeld voor [!DNL Real-time Customer Profile]

## Volgende stappen

Leer hoe te om uw [!DNL Marketo] gegevens aan Platform aan te sluiten, zie de zelfstudie op [creërend een bron van Marketo schakelaar in UI](../../../tutorials/ui/create/adobe-applications/marketo.md).