---
title: Aanvullende informatie voor Adobe Experience Platform van juni 2025
description: Aanvullende informatie voor Adobe Experience Platform van juni 2025
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c78dc0e83976499403e066b314a0889df803c976
workflow-type: ht
source-wordcount: '1646'
ht-degree: 100%

---


# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/pre-release-notes)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: 18 juni 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Toegangsbeheer](#access-control)
- [Geavanceerd beheer van de levenscyclus van gegevens](#advanced-data-lifecycle-management)
- [Catalogusservice](#catalog-service)
- [Dashboards](#dashboards)
- [Datagovernance](#data-governance)
- [Bestemmingen](#destinations)
- [Samenstelling van Federated-doelgroep](#fac)
- [Privacyservice](#privacy-service)
- [Sandboxes](#sandboxes)
- [Segmentatie](#segmentation-service)
- [Bronnen](#sources)

## Toegangsbeheer {#access-control}

Experience Platform maakt gebruik van [Adobe Admin Console](https://adminconsole.adobe.com)-productprofielen om gebruikers te koppelen aan machtigingen en sandboxen. Met machtigingen wordt de toegang tot diverse mogelijkheden van het Experience Platform beheerd, waaronder gegevensmodellering, profielbeheer en sandboxbeheer.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| Machtiging voor het exporteren van dashboardgegevens | Voor de dashboardopties **[!UICONTROL Download CSV]** en **[!UICONTROL Send as email]** is nu de machtiging **[!UICONTROL Export Dashboard Data]** vereist. Dankzij deze machtiging kunnen alleen geautoriseerde gebruikers tabelgegevens exporteren, wat leidt tot strakker beleid voor governance en gegevenstoegang. Lees het [gedeelte over machtigingen in de handleiding voor toegangsbeheer](../../access-control/home.md#permissions) voor meer informatie. |

Raadpleeg voor meer informatie het [overzicht van toegangsbeheer](../../access-control/home.md).

## Geavanceerd beheer van de levenscyclus van gegevens {#advanced-data-lifecycle-management}

Experience Platform biedt een reeks mogelijkheden voor Gegevensgezondheid waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentenrecords en datasets. U kunt uw gegevensopslag effectief beheren met de werkruimte van de gegevenslevenscyclus in de gebruikersinterface of via aanroepen naar de API voor Gegevensgezondheid. Met deze mogelijkheden kunt u ervoor zorgen dat informatie wordt gebruikt zoals verwacht, wordt bijgewerkt wanneer onjuiste gegevens moeten worden gecorrigeerd en wordt verwijderd wanneer het organisatiebeleid dit noodzakelijk acht.

**Nieuwe documentatie**

| Nieuwe documentatie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid voor verwijdering van records | U kunt nu via de gebruikersinterface of API afzonderlijke records verwijderen op basis van identiteitsvelden. Met deze functie kunt u opslagruimte beperken, governance afdwingen en de gegevensopschoning verbeteren door verwijdering uit één dataset of uit alle datasets toe te staan. Er gelden volumebeperkingen en toelatingsvoorwaarden. Raadpleeg de [handleiding voor records verwijderen](../../hygiene/ui/record-delete.md) voor meer informatie. |

Raadpleeg voor meer informatie het [overzicht van geavanceerd beheer van de levenscyclus van gegevens](../../hygiene/home.md).

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie en herkomst van gegevens binnen Adobe Experience Platform. Alle gegevens die in Experience Platform worden opgenomen, worden in een datalake opgeslagen als bestanden en mappen. De catalogus bevat daarentegen de metagegevens en beschrijvingen van die bestanden en mappen voor opzoek- en controledoeleinden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde voorvertoning van dataset: snellere navigatie en duidelijkere inzichten | Bekijk snel een voorbeeld van datasetgegevens, bekijk onderliggende SQL-query&#39;s en verken tot 100 rijen dankzij verbeterde filtering en duidelijker inzicht in de structuur, allemaal binnen de vertrouwde Dataset Preview-ervaring. Raadpleeg de [handleiding voor de gebruikersinterface](../../catalog/datasets/user-guide.md#preview) voor meer informatie. |

{style="table-layout:auto"}

## Dashboards {#dashboards}

Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten krijgt in de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnames.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verzenden als e-mailexportoptie | U kunt nu tot 10.000 records uit de modus Query Pro exporteren door **[!UICONTROL Send as email]** te selecteren in het menu **[!UICONTROL View more]**. Met deze optie wordt veilig een downloadkoppeling naar uw aan Adobe gekoppelde e-mail verzonden voor een grotere exportbewerking. Raadpleeg de [handleiding voor meer weergeven](../../dashboards/sql-insights-query-pro-mode/view-more.md#export) voor meer informatie. |

Voor meer informatie over dashboards, bijvorbeeld hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Datagovernance {#data-governance}

Adobe Experience Platform-datagovernance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving te waarborgen van regelgeving, beperkingen en beleidsregels die op gegevensgebruik van toepassing zijn. Dit speelt binnen [!DNL Experience Platform] een sleutelrol op verschillende niveaus zoals catalogisering, gegevensoorsprong, labeling van gegevensgebruik, beleid voor gegevenstoegang en beheer van toegang tot gegevens voor marketingacties.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Azure CMK Alerts en configuratie van de lijst met IP&#39;s van gewenste personen | U kunt nu het statische IP-adres van Adobe in Azure Key Vault op de Lijst van gewenste personen zetten, zodat er toegang blijft wanneer netwerkbeperkingen zijn ingeschakeld. Hiermee voorkomt u onderbrekingen in de diensten van het platform vanwege beperkte sleuteltoegang. |
| CMK-configuratiewaarschuwingen en -oplossingen | Experience Platform activeert nu waarschuwingen wanneer Adobe-services de toegang tot uw Azure Key Vault verliezen (bijvoorbeeld als gevolg van verwijderde IP-vermeldingen uit de lijst met gewenste personen, of uitgeschakelde sleutels). Met een nieuwe handleiding kunt u elke melding begrijpen en corrigerende actie ondernemen. |

Raadpleeg voor meer informatie het [overzicht van datagovernance](../../data-governance/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md)-verbinding | Gebruik de bestemming [!DNL Algolia] om consistente personalisatie op alle sites te leveren, van de startpagina tot de zoekresultaten. Stel uitgebreide doelgroepen samen uit meerdere gegevensbronnen en deel deze via verschillende kanalen voor betere targetingstrategieën en personalisatie van campagnes. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| [Google Customer Match + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) algemene beschikbaarheid | De Google Customer Match + DV360-bestemming is nu beschikbaar voor alle Experience Platform-gebruikers. De documentatie bevat nu gedetailleerde richtlijnen voor het [koppelen van accounts](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking) tussen [!DNL Adobe] en [!DNL Google] advertentieaccounts. |
| [Bewaking op doelgroepniveau](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) voor streamingbestemmingen | Monitoring op doelgroepniveau is nu beschikbaar voor de volgende bestemmingen: <ul><li>[[!DNL (API) Oracle Eloqua] verbinding](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| Ondersteuning van aanvullende identificatiegegevens voor [Facebook](../../destinations/catalog/social/facebook.md#supported-identities)-bestemmingen | De bestemming [!DNL Facebook] ondersteunt nu het toewijzen van nieuwe adresgerelateerde velden voor verbeterde targeting en matching met profielen wat betreft Facebook-eigenschappen. Zie de sectie [ondersteunde identiteiten](../../destinations/catalog/social/facebook.md#supported-identities) voor meer informatie over de nieuwe adresgerelateerde velden.<br> ![Platform UI-afbeelding met de extra velden voor Facebook.](../2025/assets/june/facebook-destination-fields.png "Platform-UI-afbeelding met de extra velden voor Facebook."){width="200" align="center" zoomable="yes"} |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md)-bestemmingsupgrade | Vanaf vrijdag 19 juni 2025 kunt u twee **[!DNL Braze]**-kaarten naast elkaar zien in de bestemmingencatalogus. Dit komt door een interne upgrade van de bestemmingsservice. De naam van de bestaande bestemmingsconnector [!DNL Braze] is gewijzigd in **[!UICONTROL (Deprecated) Braze]** en er is nu een nieuwe kaart met de naam **[!UICONTROL Braze]** voor u beschikbaar. <br> Gebruik de **[!UICONTROL Braze]**-verbinding in de catalogus voor nieuwe activeringsgegevensstromen. Als u actieve gegevensstromen naar de bestemming **[!UICONTROL (Deprecated) Braze]** hebt, worden deze automatisch bijgewerkt. U hoeft dus niets te doen. <br> Als u gegevensstromen maakt via de [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/), moet u uw [!DNL flow spec ID] en [!DNL connection spec ID] bijwerken naar de volgende waarden: <ul><li>Stroomspecificatie-ID: `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>Verbindingsspecificatie-ID: `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Samenstelling van Federated-doelgroep {#fac}

Samenstelling van Federated-doelgroep stelt ondernemingen in staat om gegevens samen te stellen voor een betere toepassing in diverse gebruikssecenario&#39;s. Met deze nieuwe aanpak kunt u als gebruiker van Adobe Real-Time Customer Data Platform en/of Adobe Journey Optimizer datasets rechtstreeks vanuit uw bestaande datawarehouse samenvoegen om Adobe Experience Platform-doelgroepen en -kenmerken in één systeem te maken en te verrijken.

| Nieuwe functie | Beschrijving |
| ----------- | ----------- |
| Algemene beschikbaarheid voor Adobe Healthcare Shield-klanten | Samenstelling van Federated-doelgroep zal eind juni beschikbaar zijn voor klanten van het Adobe Healthcare Shield voor het maken van doelgroepen, verrijking en het gebruik van profielverrijking. Voor meer informatie over de privacy en de veiligheidsmaatregelen van de samenstelling van de Federated-doelgroep raadpleegt u het [overzicht voor privacy en de veiligheid in de samenstelling van de Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/start/privacy-security). Voor meer informatie over de naleving van HIPAA voor de producten van Experience Platform in het algemeen raadpleegt u het [ overzicht van HIPAA en de producten en services van Adobe ](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Raadpleeg voor meer informatie de [documentatie over samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Verschillende wettelijke en organisatorische voorschriften geven gebruikers het recht om op verzoek hun persoonlijke gegevens in te zien of te verwijderen uit uw gegevensopslag. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot privé- of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | ---|
| Ondersteuning voor privacywetten in Tennessee en Minnesota | Privacy Service ondersteunt nu de Tennessee Information Protection Act (`tipa_tn_usa`) en de Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). U kunt verzoeken om toegang en verwijdering verwerken in overeenstemming met deze nieuwe regelgeving op staatsniveau. Raadpleeg het [regelgevingsoverzicht](https://experienceleague.adobe.com/nl/docs/experience-platform/privacy/regulations/overview) voor meer informatie. |

Zie het [overzicht van de Privacyservice](../../privacy-service/home.md) voor meer informatie over de service.

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Migratie van objectconfiguratie-updates | U kunt nu na de eerste replicatie herhalende objectconfiguratie-updates migreren tussen sandboxen. Deze verbetering ondersteunt ontwikkelingsworkflows waarbij configuraties moeten worden bijgewerkt en verspreid over omgevingen zonder de gehele sandboxconfiguratie opnieuw te maken. Voor meer informatie raadpleegt u de handleiding over het [overdragen van configuratie-updates tussen sandboxes](../../sandboxes/ui/sandbox-tooling.md#move-configs). |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Beschikbaarheidsupdate van lookalike-inzichten | Lookalike-inzichten en lookalike-doelgroepen worden voor omgevingen met een laag gebruik automatisch uitgeschakeld. Laag gebruik wordt gedefinieerd als het niet weergeven van lookalike-inzichten gedurende de afgelopen drie maanden, of het niet maken van een nieuwe lookalike-doelgroep gedurende de afgelopen zes maanden. Meer informatie over deze wijziging vindt u in de [handleiding voor lookalike-doelgroepen](../../segmentation/types/lookalike-audiences.md). |

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} UI-ondersteuning voor [!DNL Azure Databricks] | U kunt uw [!DNL Azure Databricks]-account nu verbinden met Experience Platform via de bronnenwerkruimte in de gebruikersinterface. Raadpleeg de handleiding over [verbinding maken [!DNL Databricks]  met Experience Platform in de gebruikersinterface](../../sources/connectors/databases/databricks.md) voor meer informatie. |
| Ondersteuning voor nieuw verificatietype voor [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] ondersteunt nu ook de belangrijkste verificatie van de service, naast verificatie van de bestaande verbindingstekenreeks. Raadpleeg het [[!DNL Azure Synapse Analytics] verificatieoverzicht](../../sources/connectors/databases/synapse-analytics.md) voor meer informatie. |
| [!DNL Salesforce] Afschaffing van basisverificatie | De basisverificatie voor [Salesforce CRM](../../sources/connectors/crm/salesforce.md) en [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md) wordt vanaf januari 2026 afgeschaft. Klanten moeten naar OAuth 2.0-verificatie migreren om connectiviteit te behouden. Deze wijziging is van invloed op beide bronconnectoren en zorgt voor verbeterde beveiliging en naleving van de verificatienormen van Salesforce. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).
