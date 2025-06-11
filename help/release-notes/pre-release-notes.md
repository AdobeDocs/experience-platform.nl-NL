---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: c34c41d384fbc4f309dffa8bba97a0f6f3468efc
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 41%

---


# Opmerkingen bij de release Adobe Experience Platform

>[!IMPORTANT]
>
>Dit document is voorgenomen als a **voorproef** van de versienota&#39;s voor de huidige maand. Release-items kunnen worden gewijzigd en worden toegevoegd of verwijderd in de definitieve versie.

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum: donderdag 18 juni 2025**

Nieuwe functies en updates voor bestaande functies in Adobe Experience Platform:

- [Toegangsbeheer](#access-control)
- [Geavanceerd beheer van de levenscyclus van gegevens](#advanced-data-lifecycle-management)
- [Dashboards](#dashboards)
- [Datagovernance](#data-governance)
- [Bestemmingen](#destinations)
- [Samenstelling van Federated-doelgroep](#fac)
- [Privacyservice](#privacy-service)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Bronnen](#sources)

## Toegangsbeheer {#access-control}

Experience Platform hefboomwerkingen [ Adobe Admin Console ](https://adminconsole.adobe.com) productprofielen om gebruikers met toestemmingen en zandbakken te verbinden. Machtigingen beheren de toegang tot verschillende Experience Platform-mogelijkheden, waaronder gegevensmodellering, profielbeheer en sandboxbeheer.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| machtiging Dashboard-gegevens exporteren | Voor de opties **[!UICONTROL Download CSV]** en **[!UICONTROL Send as email]** in dashboards is nu de machtiging **[!UICONTROL Export Dashboard Data]** vereist. Deze toestemming zorgt ervoor dat alleen geautoriseerde gebruikers insight-gegevens met tabs kunnen exporteren, en ondersteunt een strenger beheer en beleid voor het beheer van gegevenstoegang. |

Voor meer informatie, te zien gelieve het [ overzicht van de toegangscontrole ](../access-control/home.md).

## Geavanceerd beheer van de levenscyclus van gegevens {#advanced-data-lifecycle-management}

Experience Platform biedt een reeks mogelijkheden voor Gegevensgezondheid waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentenrecords en datasets. U kunt uw gegevensopslag effectief beheren met de werkruimte van de gegevenslevenscyclus in de gebruikersinterface of via aanroepen naar de API voor Gegevensgezondheid. Met deze mogelijkheden kunt u ervoor zorgen dat informatie wordt gebruikt zoals verwacht, wordt bijgewerkt wanneer onjuiste gegevens moeten worden gecorrigeerd en wordt verwijderd wanneer het organisatiebeleid dit noodzakelijk acht.

**Nieuwe documentatie**

| Nieuwe documentatie | Beschrijving |
| --- | --- |
| Opnemen algemene beschikbaarheid verwijderen | U kunt nu afzonderlijke records op basis van identiteitsvelden verwijderen met de gebruikersinterface of API. Deze functie helpt opslag te verminderen, het beheer af te dwingen en de gegevenshygiëne te verbeteren door het verwijderen van gegevens uit één gegevensset of uit alle gegevenssets toe te staan. Er gelden volumebeperkingen en machtigingsvereisten. |

Raadpleeg voor meer informatie het [overzicht van geavanceerd beheer van de levenscyclus van gegevens](../hygiene/home.md).

## Dashboards {#dashboards}

Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten krijgt in de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnames.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verzenden als e-mailexportoptie | U kunt nu maximaal 10.000 records uit de modus Query Pro exporteren door **[!UICONTROL Send as email]** in het menu **[!UICONTROL View more]** te selecteren. Met deze optie wordt veilig een downloadkoppeling naar uw aan Adobe gekoppelde e-mail verzonden voor een grotere exportbewerking. |

Voor meer informatie over dashboards, met inbegrip van hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../dashboards/home.md).

## Datagovernance {#data-governance}

Adobe Experience Platform-datagovernance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving te waarborgen van regelgeving, beperkingen en beleidsregels die op gegevensgebruik van toepassing zijn. Dit speelt binnen [!DNL Experience Platform] een sleutelrol op verschillende niveaus zoals catalogisering, gegevensoorsprong, labeling van gegevensgebruik, beleid voor gegevenstoegang en beheer van toegang tot gegevens voor marketingacties.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Azure CMK Alerts en IP de Configuratie van de Lijst van gewenste personen | U kunt nu het statische IP-adres van Adobe in Azure Key Vault lijsten van gewenste personen om ervoor te zorgen dat de toegang wordt voortgezet wanneer netwerkbeperkingen zijn ingeschakeld. Dit helpt verstoringen aan de diensten van het Platform wegens beperkte zeer belangrijke toegang te verhinderen. |
| Waarschuwingen en resoluties over CMK-configuratie | Experience Platform activeert nu waarschuwingen wanneer Adobe-services de toegang tot uw Azure Key Vault verliezen (bijvoorbeeld als gevolg van verwijderde IP-items voor lijsten van gewenste personen of uitgeschakelde sleutels). Een nieuwe gids helpt u elke alarm begrijpen en correctieve actie ondernemen. |

Raadpleeg voor meer informatie het [overzicht van datagovernance](../data-governance/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| Algolia-gebruikerssegmenten | De bestemming van de Segmenten van de Gebruiker van Algolia laat marketing beroeps toe om verenigbare verpersoonlijking over plaatsen van homepage aan onderzoek te leveren. Bouw rijk publiek van veelvoudige gegevensbronnen en deel hen over diverse kanalen voor betere gerichte strategieën en campagneverpersoonlijking. |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Informatie over verlopen van LinkedIn-account | Informatie over het verlopen van accounts voor LinkedIn-doelen is nu rechtstreeks beschikbaar in de weergaven [!UICONTROL Browse] en [!UICONTROL Accounts] . Eerder was deze informatie alleen beschikbaar in documentatie. Deze verbetering verstrekt betere zichtbaarheid in LinkedIn authentificatiestatus en credentiebeheer. |
| Google Customer Match + DV360 algemene beschikbaarheid en verbetering | De Google Customer Match + DV360-bestemming is nu beschikbaar voor alle Experience Platform-gebruikers. De documentatie bevat nu gedetailleerde richtsnoeren voor het maken van een verband tussen de advertentierekeningen van Adobe en Google. |
| Ondersteuning voor gegevenslandingszone (DLZ)-doelcodering | Toegevoegde encryptiesteun voor de bestemming van de Gebied van Gegevens Landing. U kunt nu openbare sleutels met RSA-indeling toevoegen om versleuteling toe te voegen aan geëxporteerde bestanden. |
| Toezicht op het niveau van het publiek op ondernemingsbestemmingen | Controle op het niveau van de doelgroep is nu beschikbaar voor de volgende ondernemingsdoelen: [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md) . |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Samenstelling van Federated-doelgroep {#fac}

Samenstelling van Federated-doelgroep stelt ondernemingen in staat om gegevens samen te stellen voor een betere toepassing in diverse gebruikssecenario&#39;s. Met deze nieuwe aanpak kunt u als gebruiker van Adobe Real-Time Customer Data Platform en/of Adobe Journey Optimizer datasets rechtstreeks vanuit uw bestaande datawarehouse samenvoegen om Adobe Experience Platform-doelgroepen en -kenmerken in één systeem te maken en te verrijken.

| Nieuwe functie | Beschrijving |
| ----------- | ----------- |
| Gereedheid van HIPAA | Federated Audience Composition is nu HIPAA-compatibel. Voor meer informatie over de privacy en de veiligheidsmaatregelen van de Samenstelling van de Federatieve Publiek, lees de [ privacy en de veiligheid in het Federated overzicht van de Samenstelling van de Publiek ](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security). Voor meer informatie over de naleving van HIPAA voor de producten van Experience Platform in het algemeen, lees [ HIPAA en het overzicht van de Producten en van de Diensten van Adobe ](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Raadpleeg voor meer informatie de [documentatie over Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Verschillende wettelijke en organisatorische voorschriften geven gebruikers het recht om op verzoek hun persoonlijke gegevens in te zien of te verwijderen uit uw gegevensopslag. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot privé- of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor Tennessee- en Minnesota Privacy-wetten | Privacy Service ondersteunt nu de Tennessee Information Protection Act (`tipa_tn_usa`) en de Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa` ). U kunt toegangs en schrappingsverzoeken in overeenstemming met deze nieuwe staat-vlakke verordeningen verwerken. Zie het [ overzicht van Verordeningen ](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview) voor meer details. |

Zie het [overzicht van de Privacy Service](../privacy-service/home.md) voor meer informatie over de service.

## Query-service {#query-service}

Voer query&#39;s uit op gegevens in het Adobe Experience Platform-data lake met behulp van standaard SQL met Query Service. Combineer naadloos datasets en produceer nieuwe degenen van uw vraagresultaten aan macht rapportering, laat de werkschema&#39;s van de gegevenswetenschap toe, of vergemakkelijkt opname in het Profiel van de Klant in real time.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Geavanceerde statistische functies | **de schetsdoorsnede van de Theta**: De nieuwe functie voor gegevensverwerkingsreeks snijpunten die de eta schetsen voor benaderend verschillend tellen en vastgestelde verrichtingen gebruiken. **KLL histogrammen**: Verbeterde histogrammogelijkheden die KLL (Kth kleinst, L grootste, Grote punten) schetsen gebruiken voor kwantitatieve raming en verdelingsanalyse. Deze functies zijn beschikbaar voor Distiller-klanten van Data. |
| SQL-sjabloonbibliotheek | Er is nu een uitgebreide bibliotheek met SQL-sjablonen voor algemene gebruiksgevallen beschikbaar. Deze functie versnelt de ontwikkeling van query&#39;s door sjablonen voor best practices voor frequente analytische patronen te bieden, waardoor klanten van Data Distiller efficiënter complexe analyses kunnen implementeren. |

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Voorbeeld van RFM-modellen | Een uitgebreid voorbeeld van Recency, Frequency, Monetary (RFM) modellering voor klanten van Data Distiller. Dit omvat gedetailleerde documentatie en implementatiegidsen voor klantensegmentatie en waardeanalyse gebruikend technieken RFM. |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Migratie van objectconfiguratie-updates | U kunt nu configuratieupdates van herhalende objecten migreren over sandboxen na de eerste replicatie. Deze verbetering steunt ontwikkelingswerkschema&#39;s waar de configuraties over milieu&#39;s moeten worden bijgewerkt en worden verspreid zonder de volledige zandbakopstelling opnieuw te creëren. |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, raadpleegt u het [ overzicht van sandboxes](../sandboxes/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor nieuw verificatietype voor [!DNL Azure Synapse Analytics] | [!DNL Azure Synapse Analytics] zal nu ook de dienst belangrijkste authentificatie, naast de bestaande authentificatie van het verbindingskoord steunen. |

**Belangrijke authentificatieupdates**

| Bijwerken | Beschrijving |
| --- | --- |
| [!DNL Salesforce] Basisversie van verificatie | Basic Authentication for Salesforce CRM and Salesforce Service Cloud will be deprecated by January 2026. Klanten moeten naar OAuth 2.0-verificatie migreren om connectiviteit te behouden. Deze verandering beïnvloedt zowel bronschakelaars en verzekert betere veiligheid en naleving van de Salesforce authentificatienormen. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).
