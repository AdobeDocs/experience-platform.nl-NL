---
title: B2B-naamruimten en -schema's
description: Dit document biedt een overzicht van aangepaste naamruimten die zijn vereist voor het maken van een B2B-bronconnector.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: 5eeb0397ddc96a224919a776f94058ae3a539b69
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 0%

---

# B2B-naamruimten en -schema&#39;s

>[!AVAILABILITY]
>
>- U moet toegang tot [&#x200B; Adobe Real-Time Customer Data Platform B2B edition &#x200B;](../../../../rtcdp/b2b-overview.md) voor uw B2B- schema&#39;s hebben om in [&#x200B; in real time het Profiel van de Klant &#x200B;](../../../../profile/home.md) te kwalificeren.
>
>- Beginnend Januari 2026, zal Real-Time CDP B2B edition niet meer **niet-standaard** verhoudingen tussen B2B entiteiten steunen. Daarom wordt u aangemoedigd om uw B2B entiteiten bij te werken om de standaardverhoudingen te gebruiken die in [&#x200B; worden geschetst B2B namespaces en schemagids &#x200B;](../../../../rtcdp/schemas/b2b.md).

>[!NOTE]
>
>U kunt sjablonen in de gebruikersinterface van Adobe Experience Platform gebruiken om het maken van elementen voor B2B- en B2C-gegevens te versnellen. Voor meer informatie, lees de gids op [&#x200B; gebruikend malplaatjes in Experience Platform UI &#x200B;](../../../tutorials/ui/templates.md).

Lees dit document voor informatie over de onderliggende opstelling voor namespaces en schema&#39;s die met B2B bronnen moeten worden gebruikt. Dit document bevat ook informatie over het instellen van het Postman-hulpprogramma voor automatisering dat vereist is voor het genereren van B2B-naamruimten en -schema&#39;s.

## B2B-naamruimten instellen en hulpprogramma voor automatisch genereren van schema&#39;s

>[!IMPORTANT]
>
>De JWT-gegevens (Service Account) zijn afgekeurd. U moet ervoor zorgen dat u uw toepassing of integratie aan de nieuwe server-aan-Server referentie OAuth vóór 27 Januari, 2025 migreert. Lees de volgende documentatie voor gedetailleerde stappen op [&#x200B; hoe te om uw geloofsbrieven van JWT aan de Server-aan-Server referentie OAuth &#x200B;](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/) te migreren.

Raadpleeg de volgende documentatie voor informatie over de manier waarop u de [!DNL Postman] -omgeving zo kunt instellen dat deze ondersteuning biedt voor de naamruimte B2B en het hulpprogramma voor automatisch genereren van schema&#39;s.

- U kunt namespace en schema auto-generatie nutsinzameling en milieu van deze [&#x200B; bewaarplaats GitHub &#x200B;](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) downloaden.
- Voor informatie bij het gebruiken van Experience Platform APIs met inbegrip van details over hoe te om waarden voor vereiste kopballen te verzamelen en steekproefAPI vraag te lezen, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../landing/api-guide.md).
- Voor informatie over hoe te om uw geloofsbrieven voor Experience Platform APIs te produceren, zie het leerprogramma op [&#x200B; voor authentiek verklaren en tot Experience Platform APIs toegang heeft &#x200B;](../../../../landing/api-authentication.md).
- Voor informatie over hoe te opstelling [!DNL Postman] voor Experience Platform APIs, zie het leerprogramma op [&#x200B; vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../../landing/postman.md).

Met een Experience Platform-ontwikkelaarsconsole en [!DNL Postman] -configuratie kunt u nu de juiste omgevingswaarden toepassen op uw [!DNL Postman] -omgeving.

De volgende tabel bevat voorbeeldwaarden en aanvullende informatie over het vullen van de [!DNL Postman] -omgeving:

| Variabele | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `CLIENT_SECRET` | Een unieke id die wordt gebruikt om de `{ACCESS_TOKEN}` te genereren. Zie het leerprogramma op [&#x200B; voor authentiek verklaren en tot Experience Platform APIs toegang hebben &#x200B;](../../../../landing/api-authentication.md) voor informatie over hoe te om uw `{CLIENT_SECRET}` terug te winnen. | `{CLIENT_SECRET}` |
| `API_KEY` | Een unieke id die wordt gebruikt om aanroepen naar Experience Platform API&#39;s te verifiëren. Zie het leerprogramma op [&#x200B; voor authentiek verklaren en tot Experience Platform APIs toegang hebben &#x200B;](../../../../landing/api-authentication.md) voor informatie over hoe te om uw `{API_KEY}` terug te winnen. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Het toestemmingstoken wordt vereist om vraag aan Experience Platform APIs te voltooien. Zie het leerprogramma op [&#x200B; voor authentiek verklaren en tot Experience Platform APIs toegang hebben &#x200B;](../../../../landing/api-authentication.md) voor informatie over hoe te om uw `{ACCESS_TOKEN}` terug te winnen. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ent_dataservices_sdk` . | `ent_dataservices_sdk` |
| `CONTAINER_ID` | De `global` container bevat alle standaard door Adobe en Experience Platform verschafte klassen, groepen met schemavelden, gegevenstypen en schema&#39;s. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op `global` . | `global` |
| `TECHNICAL_ACCOUNT_ID` | Een referentie die wordt gebruikt om te integreren in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Het Identity Management System (IMS) biedt het framework voor verificatie van Adobe-services. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ims-na1.adobelogin.com` . | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Een onderneming die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden. Zie het leerprogramma op [&#x200B; vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../../landing/postman.md) voor instructies op hoe te om uw `{ORG_ID}` informatie terug te winnen. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | De naam van de virtuele sandboxpartitie die u gebruikt. | `prod` |
| `TENANT_ID` | Een id die wordt gebruikt om ervoor te zorgen dat de bronnen die u maakt, correct worden genoemd en zich binnen uw organisatie bevinden. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Het URL-eindpunt waarnaar u API-aanroepen maakt. Deze waarde is vast en wordt altijd ingesteld op: `http://platform.adobe.io/` . | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### Scripts uitvoeren

Als de verzameling van [!DNL Postman] is ingesteld en de omgeving is ingesteld, kunt u het script nu uitvoeren via de interface van [!DNL Postman] .

Selecteer in de interface [!DNL Postman] de hoofdmap van het hulpprogramma voor automatische generator en selecteer vervolgens **[!DNL Run]** in de bovenste koptekst.

![&#x200B; de wortelomslag van de de generator van Namespaces en van Schema in Postman UI. &quot;Runs&quot; wordt benadrukt in de hoogste menubar.](../images/marketo/root_folder.png)

De interface [!DNL Runner] wordt weergegeven. Controleer van hieruit of alle selectievakjes zijn ingeschakeld en selecteer vervolgens **[!DNL Run Namespaces and Schemas Autogeneration Utility]** .

![&#x200B; De Runner interface van Postman UI met verscheidene verzoeken in de inzameling van Namespaces en van Schema&#39;s gecontroleerd en &quot;de knoop van Namespaces en van de Lopen&quot;op de rechterkant wordt benadrukt.](../images/marketo/run_generator.png)

Een succesvol verzoek leidt tot namespaces en schema&#39;s die voor B2B worden vereist.

## B2B-naamruimten

Identiteitsnaamruimten zijn een component van [[!DNL Identity Service]](../../../../identity-service/home.md) die dienen om de context van een identiteit te onderscheiden. Een volledig gekwalificeerde identiteit omvat een identiteitswaarde en een namespace. Lees het [&#x200B; namespaces overzicht &#x200B;](../../../../identity-service/features/namespaces.md) voor meer informatie.

B2B-naamruimten worden gebruikt in de primaire identiteit van de entiteit.

De volgende tabel bevat informatie over de onderliggende instelling voor B2B-naamruimten.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Weergavenaam | Identiteitssymbool | Identiteitstype |
| --- | --- | --- |
| B2B-persoon | `b2b_person` | `CROSS_DEVICE` |
| B2B-account | `b2b_account` | `B2B_ACCOUNT` |
| B2B-opportuniteit | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B-opportuniteitsrelatie | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B-campagne | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B Campagne-lid | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B-marketinglijst | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B Marketing List Member | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B Betrekking van rekeningpersoon | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## B2B-schema&#39;s

Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens.

Voordat gegevens in Experience Platform kunnen worden ingevoerd, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. De schema&#39;s bestaan uit een basisklasse en nul of meer groepen van het schemagebied.

Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes en beste praktijken, zie de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../../../../xdm/schema/composition.md).

De volgende tabel bevat informatie over de onderliggende opstelling van B2B-schema&#39;s.

>[!NOTE]
>
>Schuif naar links/rechts om de volledige inhoud van de tabel weer te geven.

| Schemanaam | Basisklasse | Veldgroepen | [!DNL Profile] in schema | Primaire identiteit | Primaire naamruimte | Secundaire identiteit | Secundaire naamruimte voor identiteit | Relatie | Notities |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B-account | [&#x200B; XDM BedrijfsRekening &#x200B;](../../../../xdm/classes/b2b/business-account.md) | XDM-bedrijfsaccountgegevens | Ingeschakeld | `accountKey.sourceKey` in de basisklasse | B2B-account | `extSourceSystemAudit.externalKey.sourceKey` in de basisklasse | B2B-account | <ul><li>`accountParentKey.sourceKey` in de XDM Business Account Details-veldgroep</li><li>Eigenschap van bestemming: `/accountKey/sourceKey`</li><li>Type: een-op-een</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li></ul> |  |
| B2B-persoon | [&#x200B; XDM Individueel Profiel &#x200B;](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM Business Person - Gegevens</li><li>XDM Business Person-componenten</li><li>IdentityMap</li><li>Details van goedkeuring en voorkeur</li></ul> | Ingeschakeld | `b2b.personKey.sourceKey` in de XDM Business Person Details Field Group | B2B-persoon | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` van de XDM Business Person Details-veldgroep</li><li>`workEmail.address` van de XDM Business Person Details-veldgroep</ol></li> | <ol><li>B2B-persoon</li><li>Email</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` van XDM Business Person Components, veldgroep</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Bestemmingseigenschap: accountKey.sourceKey</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |
| B2B-opportuniteit | [&#x200B; XDM Business Opportunity &#x200B;](../../../../xdm/classes/b2b/business-opportunity.md) | XDM Business Opportunity-gegevens | Ingeschakeld | `opportunityKey.sourceKey` in de basisklasse | B2B-opportuniteit | `extSourceSystemAudit.externalKey.sourceKey` in de basisklasse | B2B-opportuniteit | <ul><li>`accountKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Eigenschap van bestemming: `accountKey.sourceKey`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie naam van referentieschema: mogelijkheden</li></ul> |  |
| B2B-opportuniteitsrelatie | [&#x200B; XDM de Verhouding van de Person van BedrijfsOpportunity &#x200B;](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | Geen | Ingeschakeld | `opportunityPersonKey.sourceKey` in de basisklasse | B2B-opportuniteitsrelatie | | | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: b2b.personKey.sourceKey</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatie naam van referentieschema: mogelijkheden</li></ul>**Tweede verhouding**<ul><li>`opportunityKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B Opportunity </li><li>Namespace: B2B Opportunity </li><li>Eigenschap van bestemming: `opportunityKey.sourceKey`</li><li>Relatienaam uit huidig schema: Opportunity</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |
| B2B-campagne | [&#x200B; XDM Bedrijfs Campagne &#x200B;](../../../../xdm/classes/b2b/business-campaign.md) | XDM Business Campaign - details | Ingeschakeld | `campaignKey.sourceKey` in de basisklasse | B2B-campagne | | |  |
| B2B Campagne-lid | [&#x200B; XDM Bedrijfs Campagne Leden &#x200B;](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM Business Campagne Member Details | Ingeschakeld | `ccampaignMemberKey.sourceKey` in de basisklasse | B2B Campagne-lid | | | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.sourceKey`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatie-naam vanuit referentieschema: campagnes</li></ul>**Tweede verhouding**<ul><li>`campaignKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-campagne</li><li>Naamruimte: B2B-campagne</li><li>Eigenschap van bestemming: `campaignKey.sourceKey`</li><li>Relatienaam van huidig schema: Campagne</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |
| B2B-marketinglijst | [&#x200B; XDM Business Marketing List &#x200B;](../../../../xdm/classes/b2b/business-marketing-list.md) | Geen | Ingeschakeld | `marketingListKey.sourceKey` in de basisklasse | B2B-marketinglijst | Geen | Geen | Geen | Statische lijst wordt niet gesynchroniseerd vanuit [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| B2B Marketing List Member | [&#x200B; XDM Bedrijfs de Leden van de Lijst van de Marketing &#x200B;](../../../../xdm/classes/b2b/business-marketing-list-members.md) | Geen | Ingeschakeld | `marketingListMemberKey.sourceKey` in de basisklasse | B2B Marketing List Member | Geen | Geen | **Eerste verhouding**<ul><li>`PersonKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.sourceKey`</li><li>Relatienaam uit huidig schema: Persoon</li><li>Relatienaam van referentieschema: marketinglijsten</li></ul>**Tweede verhouding**<ul><li>`marketingListKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-marketinglijst</li><li>Naamruimte: B2B-marketinglijst</li><li>Eigenschap van bestemming: `marketingListKey.sourceKey`</li><li>Relatienaam uit huidig schema: Marketinglijst</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> | Lid van een statische lijst wordt niet gesynchroniseerd vanuit [!DNL Salesforce] en heeft daarom geen secundaire identiteit. |
| B2B Betrekking van rekeningpersoon | [&#x200B; XDM de Verhouding van de Persoon van de Bedrijfs Rekening &#x200B;](../../../../xdm/classes/b2b/business-account-person-relation.md) | Identiteitskaart | Ingeschakeld | `accountPersonKey.sourceKey` in de basisklasse | B2B Betrekking van rekeningpersoon | Geen | Geen | **Eerste verhouding**<ul><li>`personKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-persoon</li><li>Naamruimte: B2B-persoon</li><li>Eigenschap van bestemming: `b2b.personKey.SourceKey`</li><li>Relatie-naam uit huidig schema: Personen</li><li>Relatie-naam vanuit referentieschema: Account</li></ul>**Tweede verhouding**<ul><li>`accountKey.sourceKey` in de basisklasse</li><li>Type: veel-op-één</li><li>Referentieschema: B2B-account</li><li>Naamruimte: B2B-account</li><li>Eigenschap van bestemming: `accountKey.sourceKey`</li><li>Relatienaam uit huidig schema: Account</li><li>Relatie-naam vanuit referentieschema: Personen</li></ul> |  |

{style="table-layout:auto"}

## Volgende stappen

Leren hoe te om uw [!DNL Marketo] gegevens met Experience Platform te verbinden, zie het leerprogramma op [&#x200B; het creëren van een bron van Marketo schakelaar in UI &#x200B;](../../../tutorials/ui/create/adobe-applications/marketo.md).

<!--

| B2B Activity | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>Visit WebPage</li><li>New Lead</li><li>Convert Lead</li><li>Add To List</li><li>Remove From List</li><li>Add To Opportunity</li><li>Remove From Opportunity</li><li>Form Filled Out</li><li>Link Clicks</li><li>Email Delivered</li><li>Email Opened</li><li>Email Clicked</li><li>Email Bounced</li><li>Email Bounced Soft</li><li>Email Unsubscribed</li><li>Score Changed</li><li>Opportunity Updated</li><li>Status in Campaign Progression Changed</li><li>Person Identifier</li><li>Marketo Web URL</li><li>Interesting Moment</li><li>Call Webhook</li><li>Change Campaign Cadence</li><li>Revenue Stage Changed</li><li>Merge Leads</li><li>Email Sent</li><li>Change Campaign Stream</li><li>Add to Campaign</li></ul> | Enabled | `personKey.sourceKey` of Person Identifier field group | B2B Person | None | None | | `ExperienceEvent` is different from entities. The identity of experience event is the person who did the activity. |

-->