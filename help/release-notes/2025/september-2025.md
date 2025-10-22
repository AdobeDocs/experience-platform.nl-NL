---
title: Aanvullende informatie van september 2025 voor Adobe Experience Platform
description: Aanvullende informatie voor de versie van september 2025 voor Adobe Experience Platform.
exl-id: 9c5ab487-22b8-4590-b4ea-abec0f377703
source-git-commit: 96b9fcd8bfb4ff62eb9d4adce2e486782d918344
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 91%

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

**Releasedatum: 23 september 2025**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Waarschuwingen](#alerts)
- [Bestemmingen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Real-Time Customer Profile](#profile)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator is de nieuwe laag op agentbasis in Adobe Experience Platform.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator is de nieuwe laag op agentbasis in Adobe Experience Platform. Experience Platform Agent Orchestrator is ontworpen om de uitgebreide kennis van gegevens en klanten van het platform te benutten. De tool stuurt de intelligentie en redenering aan achter speciaal ontwikkelde, deskundige Adobe Experience Platform Agents. Deze kunnen hierdoor complexe besluitvormings- en probleemoplossingstaken snel en op grote schaal uitvoeren, allemaal onder menselijk toezicht. Wanneer u in natuurlijke taal vragen stelt of om hulp vraagt in een gespreksinterface zoals AI Assistant, roept Agent Orchestrator automatisch gespecialiseerde agenten op om u de juiste antwoorden te geven. Agent Orchestrator herinnert zich uw gespreksgeschiedenis, zodat u op een natuurlijke manier kunt voortbouwen op eerdere vragen zonder de context te hoeven herhalen. Ook combineert Agent Orchestrator inzichten van meerdere agenten om u duidelijke, uniforme antwoorden te bieden. Raadpleeg de [documentatie over Agent Orchestrator](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator) voor meer informatie. |
| Audience-agent | Met de Audience -agent kunt u inzicht krijgen in doelgroepen, zoals het detecteren van belangrijke wijzigingen in de omvang van doelgroepen, het detecteren van dubbele doelgroepen, het verkennen van uw doelgroepsvoorraad en het ophalen van de omvang van uw doelgroepen. Raadpleeg voor meer informatie de [documentatie over Audience-agent](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Raadpleeg de [documentatie over Agent Orchestrator](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/home) voor meer informatie.

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende Experience Platform-activiteiten. U kunt zich aanmelden voor verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van Experience Platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwingen voor het opnemen van streamingprofielen | U kunt zich nu abonneren op twee nieuwe waarschuwingen voor streamingopname op gegevensstroomniveau: <ul><li>Foutpercentage van streamingopname overschreden</li><li>Overgeslagen percentage van streamingopname overschreden</li></ul> U ontvangt waarschuwingen op het platform of per e-mail wanneer de drempelwaarden voor de standaarddrempel of een door u gedefinieerde drempelwaarde worden overschreden. Voor meer informatie raadpleegt u de handleiding [Profielwaarschuwingen](../../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Raadpleeg het [[!DNL Observability Insights] overzicht](../../observability/home.md) voor meer informatie over meldingen.

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [[!DNL Snowflake Batch]](../../destinations/catalog/cloud-storage/snowflake-batch.md) connector | Er is nu een nieuwe [!DNL Snowflake Batch]-connector beschikbaar die een alternatief biedt voor de streamingconnector voor specifieke gebruiksscenario&#39;s. |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) ondersteuning voor versleuteling | U kunt nu openbare sleutels in RSA-formaat toevoegen om uw geëxporteerde bestanden te versleutelen. Zo heeft uhetzelfde beveiligingsniveau als andere cloudopslaglocaties voor gevoelige informatie. |
| Informatie over de vervaldatum van de authenticatie voor [[!DNL Pinterest]](../../destinations/catalog/advertising/pinterest.md)-bestemmingen | Informatie over de verloopdatum van de verificatie voor [!DNL Pinterest]-bestemmingen is nu rechtstreeks zichtbaar in de Experience Platform-interface. Zo kunt u zien wanneer uw verificatie verloopt en deze vernieuwen voordat er verstoringen in uw gegevensstromen ontstaan. U kunt de vervaldatums van uw tokens controleren in de kolom **[!UICONTROL Account expiration date]** op de tabbladen **[[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts)** of **[[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse)** . |

**Nieuwe of bijgewerkte functionaliteit**

| Functie | Beschrijving |
| --- | --- |
| Verbeterde mogelijkheden voor bestemmingsbeheer in de gebruikersinterface van het Experience Platform | Verbeter uw workflow voor het beheer van doelen met nieuwe sorteermogelijkheden op de tabbladen [[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse) en [[!UICONTROL Accounts]](../../destinations/ui/destinations-workspace.md#accounts). U kunt nu ook een visuele indicator zien wanneer uw accountverificatie bijna verloopt. <br> ![](../../destinations/assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |
| Instellingen voor permanente kolombreedte | De instellingen voor kolombreedte blijven nu behouden wanneer u een pagina verlaat en ernaar terugkeert. Als u bijvoorbeeld een kolombreedte aanpast op het tabblad [[!UICONTROL Browse]](../../destinations/ui/destinations-workspace.md#browse) , blijft de aangepaste kolombreedte ongewijzigd wanneer u dat tabblad verlaat en er vervolgens weer naar terugkeert. |

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Relationele schema&#39;s | Vereenvoudig uw gegevensmodellering met Relationele Schema&#39;s (vroeger bekend als Model-Gebaseerde Schema&#39;s). U kunt nu eenvoudiger schema&#39;s maken met uitgebreide voorbeelden en richtlijnen. Deze functie is momenteel beschikbaar voor Campaign Orchestration-licentiehouders en zal worden uitgebreid naar Data Distiller-klanten bij GA, waardoor gegevensmodellering toegankelijker en efficiënter wordt. De functie biedt ondersteuning voor gegevens uit tijdreeksen en mogelijkheden voor het vastleggen van gewijzigde gegevens. |

Voor meer informatie raadpleegt u het [overzicht van XDM](../../xdm/home.md).

<!--

| Data Mirror | Ingest row-level changes from cloud data warehouses (e.g., Snowflake, Databricks, BigQuery) into Adobe Experience Platform using relational schemas. Data Mirror eliminates upstream ETL and preserves relationships, versioning, and deletions by mirroring existing database structures directly into the data lake. Time-series and record event schema behavior with change data capture capabilities are all supported. This feature is currently available for Campaign Orchestration license holders and will expand through this limited release, also including Customer Journey Analytics customers. See the [Data Mirror documentation](../../xdm/data-mirror/overview.md) for more details. Contact your Adobe representative for access. |
-->

## Real-Time Customer Profile {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| [!BADGE &#x200B; Alpha &#x200B;]{type=Informative} Deze eigenschap is momenteel in Alpha. Verbeteringen voor profielviewer | In de release van september 2025 zijn de volgende verbeteringen aangebracht in de profielviewer. <ul><li>**Gecombineerde weergave**: kenmerken, gebeurtenissen, en inzichten zijn gecombineerd in één enkele weergave.</li><li>**Door AI gegenereerde inzichten**: op de pagina met profielgegevens worden nu door AI gegenereerde inzichten weergegeven, zodat u weet welke gegevens uit uw profiel zijn gegenereerd. Deze inzichten kunnen informatie omvatten zoals propensity-scores en trendanalyse.</li><li>**Stijlupdate**: de pagina met profielgegevens is visueel vernieuwd.</li><li>**Bladeren**: u kunt nu uw profielen verkennen via een interactieve, op kaarten gebaseerde carrousel met zoek- en aanpassingsmogelijkheden.</li></ul> |

**Belangrijke updates**

| Bijwerken | Beschrijving |
| ------ | ----------- |
| API-afleiding profiel verwijderen | Het [&#x200B; Profiel schrapt API &#x200B;](/help/profile/api/entities.md#delete-entity) zal tegen eind oktober 2025 worden afgekeurd. Als u verslag schrapt verrichtingen wilt uitvoeren, kunt u het [&#x200B; verslag van de Levenscyclus van Gegevens gebruiken schrapt API werkschema &#x200B;](/help/hygiene/api/workorder.md) of het [&#x200B; het verslag van de Levenscyclus van Gegevens schrapt UI &#x200B;](/help/hygiene/ui/record-delete.md) in plaats daarvan. De workflows van de gegevenslevenscyclus bieden end-to-end levenscyclustracering en maandelijkse quota&#39;s die u kunt bekijken en beheren. <br/><br/> nadat het eindpunt is afgekeurd, zal om het even welke gebruiker die momenteel dit eindpunt gebruikt toegang tot dit eindpunt blijven hebben. Het einde van de levensduur van dit product wordt apart bekendgemaakt. Neem contact op met de klantenservice van Adobe als u vragen hebt. |

Voor meer informatie raadpleegt u het [overzicht van het realtime-klantenprofiel](../../profile/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Accountdoelgroepen met beëindiging van ervaringsgebeurtenissen | Na de upgrade van de B2B-architectuur worden accountdoelgroepen met ervaringsgebeurtenissen niet meer ondersteund. Gebruik in plaats daarvan het nieuwe segment van de segmentbenadering: maak een personendoelgroep met ervaringsgebeurtenissen en verwijs vervolgens naar die personendoelgroep wanneer u een accountdoelgroep maakt. Dit biedt een flexibelere en eenvoudigere benadering voor het maken van B2B-doelgroepen. |

**Belangrijke updates**

| Bijwerken | Beschrijving |
| ------- | ----------- |
| Automatisch vernieuwen van doelgroepschattingen is teruggezet | De verbeterde automatische vernieuwing van doelgroepinschattingen is teruggezet. Doelgroepinschattingen worden nog steeds binnen Segment Builder gegenereerd, maar de automatische vernieuwingsfunctie is teruggezet. |
| Externe doelgroep | Vanaf 30 september worden externe doelgroepen opgehaald via Unified Search in Segment Builder. Als u Segment Match gebruikt, kunt u de oude ervaring binnen Segment Builder inschakelen. |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe bronnen in algemene beschikbaarheid | De volgende bronnen zijn nu beschikbaar in algemene beschikbaarheid: verschillende bronconnectoren zijn bijgewerkt van Beta naar GA: <ul><li>[Acxiom Data-opname](../../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Acxiom Prospect Data-opname](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Deze bronnen worden nu volledig ondersteund en zijn klaar voor gebruik bij de productie. |
| [!DNL Snowflake] ondersteuning voor sleutelpaarverificatie | Uitgebreide beveiliging voor Snowflake-verbindingen met ondersteuning voor sleutelpaarverificatie. Basisverificatie (gebruikersnaam/wachtwoord) wordt vanaf november 2025 afgeschaft. Klanten worden daarom aangeraden om over te stappen op sleutelpaarverificatie voor een betere beveiliging. Raadpleeg de [[!DNL Snowflake] documentatie](../../sources/connectors/databases/snowflake.md) voor meer informatie. |
| [!BADGE Beta]{type=Informative} [!DNL Capillary Streaming Events] | Gebruik de [[!DNL Capillary Streaming Events] bron](../../sources/connectors/loyalty/capillary.md) om loyaliteitsgegevens van uw [!DNL Capillary]-account naar Experience Platform te streamen. |
| [!BADGE Beta]{type=Informative} [!DNL Relay Connector] | Gebruik [[!DNL Relay Connector]](../../sources/tutorials/ui/create/marketing-automation/relay-connector.md) om gebeurtenisgegevens te streamen vanaf uw [!DNL Relay Network] -integratie naar Experience Platform. |
| Algemene beschikbaarheid van ondersteuning voor privékoppelingen in bronnen | U kunt nu **privékoppelingen** gebruiken voor een geselecteerde groep bronnen. Met deze functie kunt u een privé-eindpunt maken waarmee uw bron verbinding kan maken. Met privé-eindpunten kunt u verbindingen en gegevensstromen instellen die het openbare internet omzeilen. Zo profiteert u van een betere beveiliging en netwerkisolatie voor uw gevoelige gegevens. Ondersteuning voor privékoppelingen is beschikbaar voor de volgende bronnen: <ul><li>[[!DNL Azure Blob Storage]](../../sources/connectors/cloud-storage/blob.md)</li><li>[[!DNL ADLS Gen2]](../../sources/connectors/cloud-storage/adls-gen2.md)</li><li>[[!DNL Azure File Storage]](../../sources/connectors/cloud-storage/azure-file-storage.md)</li></ul>. Voor meer informatie raadpleegt u de handleidingen over het maken van privékoppelingen [in de API](../../sources/tutorials/api/private-link.md) en [in de gebruikersinterface](../../sources/tutorials/ui/private-link.md). |

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).