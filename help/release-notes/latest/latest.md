---
title: Aanvullende informatie van oktober 2025 voor Adobe Experience Platform
description: Aanvullende informatie van oktober 2025 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 57cb9f5e57c83576a125ec2de5eb3e4526d5b572
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 28%

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

**Releasedatum: donderdag 22 oktober 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Waarschuwingen](#alerts)
- [Bestemmingen](#destinations)
- [Bronnen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator is de nieuwe laag op agentbasis in Adobe Experience Platform.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Audience-agent | De Audience Agent biedt nu ondersteuning voor publiek op basis van account voor het verkennen van conversaties en het detecteren van dubbele doelgroepen. Raadpleeg voor meer informatie de [documentatie over Audience-agent](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Voor meer informatie over agenten, lees de [&#x200B; documentatie van Agent Orchestrator &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/home).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwing over activeringsfout | Een nieuw alarm is toegevoegd voor bestemmingen: **het mislukkingstarief van de Activering overschrijdt drempel**. Deze waarschuwing geeft een melding wanneer het aantal mislukte records tijdens de gegevensactivering de toegestane drempel heeft overschreden, zodat u snel kunt reageren op activeringsproblemen. Lees de documentatie over [&#x200B; standaardalarm regels &#x200B;](../../observability/alerts/rules.md) voor meer informatie. |

{style="table-layout:auto"}

Raadpleeg het [[!DNL Observability Insights] overzicht](../../observability/home.md) voor meer informatie over meldingen.

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [!DNL Adform] | Gebruik deze bestemming om Adobe Real-Time CDP-gebruikers naar [!DNL Adform] te sturen voor activering op basis van de Experience Cloud-id (ECID) en de ID-versie van [!DNL Adform] . De ID Fusion van [!DNL Adform] is een service voor het oplossen van id&#39;s waarmee u uw eerste publiek kunt activeren op basis van de Experience Cloud-id (ECID). Lees de [[!DNL Adform]  documentatie &#x200B;](../../destinations/catalog/advertising/adform.md) voor meer informatie |
| [!DNL Amazon Ads] | Er is extra ondersteuning voor persoonlijke identificaties toegevoegd. Dit zijn velden zoals `firstName` , `lastName` , `street` , `city` , `state` , `zip` en `country` . Door deze velden toe te wijzen als doelidentiteiten, kunt u de overeenkomende populatiegraad verbeteren. Lees de [[!DNL Amazon Ads]  documentatie &#x200B;](../../destinations/catalog/advertising/amazon-ads.md) voor meer informatie. |
| [!DNL Snowflake Batch] (beperkte beschikbaarheid) | Maak een live [!DNL Snowflake] gegevensuitwisseling om dagelijkse publieksupdates rechtstreeks als gedeelde tabellen in uw account te ontvangen. Deze integratie is momenteel beschikbaar voor klantenorganisaties die in de VA7-regio zijn gevestigd. Lees de [[!DNL Snowflake Batch]  documentatie &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md) voor meer informatie. |
| [!DNL Snowflake Streaming] (beperkte beschikbaarheid) | Maak een live [!DNL Snowflake] gegevensuitwisseling om streaming publiek-updates rechtstreeks als gedeelde tabellen in uw account te ontvangen. Deze integratie is momenteel beschikbaar voor klantenorganisaties die in de VA7-regio zijn gevestigd. Lees de [[!DNL Snowflake Streaming]  documentatie &#x200B;](../../destinations/catalog/warehouses/snowflake.md) voor meer informatie. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| [&#x200B; Verscheidene nieuwe bestemmingen die publiek-vlakke controle &#x200B;](../../dataflows/ui/monitor-destinations.md#audience-level-view) steunen | De volgende bestemmingen steunen nu publiek-vlakke controle: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] Betrokkenheid account</li><li>[!DNL The Trade Desk]</li></ul> |
| Oplossing voor instructies voor het exporteren van gegevens | Er is een correctie toegepast op de exportinstructies voor de gegevensset. Eerder, werden sommige datasets die een timestamp kolom omvatten maar __ gebaseerd op het schema van de Gebeurtenissen van de Ervaring XDM niet verkeerd behandeld als datasets van de Gebeurtenissen van de Ervaring, die de uitvoer beperken tot een terugkijkvenster van 365 dagen. De gedocumenteerde naslaggids voor 365 dagen is nu uitsluitend van toepassing op datasets van Experience Events. Datasets die een ander schema gebruiken dan het schema voor XDM Experience Events worden nu beheerst door de handleiding voor 10 miljard records. Sommige klanten kunnen verhoogde uitvoeraantallen voor datasets zien die verkeerd onder het terugkijkvenster van 365 dagen vielen. Dit laat u toe om datasets voor vooruitlopende werkschema&#39;s uit te voeren die een lang raadplegingsvenster hebben. Voor meer informatie, lees de [&#x200B; de uitvoergidsen van de dataset &#x200B;](../../destinations/guardrails.md#dataset-exports). |
| Verbeterde publieksrapportage voor zakelijke doelen | Na deze release zullen klanten nauwkeurigere publieksrapportagenummers zien met alleen publiek dat relevant is voor de geselecteerde bestemming. Deze aanpassing van de bewaking zorgt ervoor dat de rapportage alleen betrekking heeft op publiek dat is toegewezen aan de dataflow, zodat duidelijker inzicht wordt verkregen in de feitelijke activering van gegevens. Dit heeft geen invloed op de hoeveelheid gegevens die wordt geactiveerd, maar is louter een verbetering van de controle om de nauwkeurigheid van de rapportage te verbeteren. |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Wijziging in gegevensset maken voor Adobe Analytics-bron | Als onderdeel van het proces voor het maken van gegevensbestanden tussen Adobe Analytics en Experience Platform, wordt een gegevensset gemaakt via Catalog Service. Deze dataset dient als container voor de gegevens binnen te landen. Momenteel, impliceert dit proces een identiteitskaart DataSource die van de het rapportreeks van Analytics wordt getrokken, naar de Dienst van de Catalogus wordt verzonden, en dan met de pas gecreëerde dataset wordt geassocieerd. Na de verandering, zal de optie om identiteitskaart te verstrekken DataSource niet meer tijdens datasetverwezenlijking beschikbaar zijn. Daarom zullen de nieuwe datasets die door de bron van Analytics worden gecreeerd geen identiteitskaart DataSource meer verbonden aan het in de Dienst van de Catalogus hebben. Deze wijziging is alleen van toepassing op de metagegevens en verandert de opslag van gegevens in de gegevensset op geen enkele wijze. Nochtans, is het belangrijk om te weten dat identiteitskaart DataSource die door de Dienst van de Catalogus wordt verstrekt niet meer in pas gecreëerde datasets voor Adobe Analytics beschikbaar zal zijn. Lees de [&#x200B; de brondocumentatie van Adobe Analytics &#x200B;](../../sources/connectors/adobe-applications/analytics.md) voor meer informatie over de bron van Adobe Analytics schakelaar. |
| Algemene beschikbaarheid van [!DNL Google Ads] source (alleen API) | De [&#x200B; API versie van de  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md) bron is nu in Algemene Beschikbaarheid. De API-documentatie is bijgewerkt om aan te geven dat de nieuwste versie nu `v21` is en Experience Platform ondersteunt alle versies v19 en hoger. [&#x200B; de versie UI &#x200B;](../../sources/tutorials/ui/create/advertising/ads.md) blijft in bèta en steunt slechts éénmalige opname. Gebruik de API-route om incrementele gegevensinvoer te gebruiken. |
| [!DNL Azure Event Hubs] virtuele netwerkondersteuning | Adobe biedt nu expliciet ondersteuning voor virtuele netwerkverbindingen met [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md), waardoor gegevensoverdracht via particuliere netwerken mogelijk wordt en niet via openbare netwerken. De klanten kunnen Experience Platform VNet lijsten van gewenste personen om het verkeer van de Hubs van de Gebeurtenis door de Azure privé backbone privé te leiden, die verbeterde veiligheid en naleving voor de werkschema&#39;s van de gegevensopname verstrekt. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->