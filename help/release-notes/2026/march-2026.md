---
title: Aanvullende informatie van maart 2026 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2026 voor Adobe Experience Platform.
exl-id: 66b948fd-caa0-4e5e-83dd-3b15b77c09fa
source-git-commit: 6b6a03fb8675ed01dd255f7206b23b05c809f2a6
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 20%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/nl/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/releases/latest)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum:woensdag 24 maart 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Geavanceerd beheer van de levenscyclus van gegevens](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Gegevensstromen](#datastreams)
- [Bestemmingen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Real-Time Customer Profile](#real-time-customer-profile)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Geavanceerd beheer van de levenscyclus van gegevens {#advanced-data-lifecycle-management}

Experience Platform biedt een reeks mogelijkheden voor gegevenshygiëne om u te helpen uw opgeslagen gegevens te beheren door middel van programmatische verwijderingen van consumentengegevens en gegevenssets. Met de werkruimte van de Levenscyclus van Gegevens in de UI of aanroepen naar de API voor gegevenshygiëne kunt u uw gegevensopslagruimten effectief beheren. Met deze mogelijkheden kunt u ervoor zorgen dat informatie wordt gebruikt zoals verwacht, wordt bijgewerkt wanneer onjuiste gegevens moeten worden gecorrigeerd en wordt verwijderd wanneer het organisatiebeleid dit noodzakelijk acht.

| Functie | Beschrijving |
| --- | --- |
| Meerdere gegevenssets en record met alleen profiel verwijderen (alleen API) | U kunt één gegevensset-id, een door komma&#39;s gescheiden lijst met id&#39;s van gegevenssets of het letterlijke teken `ALL` in `datasetId` verzenden om id&#39;s te verwijderen uit een, veel of alle gegevenssets. U kunt het verwijderen ook beperken tot services met betrekking tot profielen door `targetServices` in te stellen op `["identity","profile","ajo"]` , waardoor de gegevens ongewijzigd blijven. Deze functionaliteit is alleen beschikbaar via de API voor gegevenshygiëne. Zie het [&#x200B; Verslag schrap de gids van de het werkorden &#x200B;](../../hygiene/api/workorder.md) voor meer details. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie het [overzicht van geavanceerd beheer van de levenscyclus van gegevens](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Met Agent Orchestrator kunt u op AI gebaseerde agents maken en implementeren die workflows automatiseren en op meerdere kanalen met klanten communiceren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [&#x200B; Adobe Marketing Agent voor  [!DNL Microsoft 365 Copilot] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | De Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] is uw ingesloten agent die Adobe-marketinginformatie rechtstreeks in alledaagse programma&#39;s zoals [!DNL Teams] , [!DNL Word] , [!DNL PowerPoint] en andere [!DNL Microsoft 365] -apps plaatst. U kunt deze agent gebruiken om vertrouwde campagneinzichten van Adobe-toepassingen te gebruiken terwijl u campagnes plant, publiek controleert, met collega&#39;s samenwerkt om klantvragen te beantwoorden en om met gegevens geïnformeerde beslissingen te nemen zonder uw [!DNL Microsoft 365] -workflow te verlaten. |

{style="table-layout:auto"}

Raadpleeg de [documentatie over Agent Orchestrator](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator) voor meer informatie.

## Gegevensstromen {#datastreams}

Een gegevensstroom vertegenwoordigt de server-zijconfiguratie wanneer het uitvoeren van het Web van Adobe Experience Platform en Mobiele SDKs en de Server API van Adobe Experience Platform Edge Network. Het bevel van de gegevensstroomconfiguratie in SDKs behandelt alle diensten die een cliënt met in wisselwerking staat.

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van dynamische gegevensstroomconfiguraties | Dynamische gegevensstroomconfiguraties zijn nu over het algemeen beschikbaar. Met dynamische configuraties van gegevensstroom, kunt u user-configurable reeksen regels voor elke dienst bepalen die voor uw gegevensstroom wordt toegelaten, die dicteren welke oplossing Experience Cloud elk type van gegevens zou moeten ontvangen. Zie de [&#x200B; dynamische gids van de configuraties van de gegevensstroom &#x200B;](../../datastreams/configure-dynamic-datastream.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; overzicht van gegevensstromen &#x200B;](../../datastreams/overview.md).

## Bestemmingen {#destinations}

[!DNL Destinations] is vooraf gebouwde integratie met bestemmingsplatforms. Gebruik doelen om uw bekende en onbekende gegevens te activeren voor marketingcampagnes over meerdere kanalen, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [&#x200B; de Gebied van de Partij van Snowflake &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md) selecteur | U kunt uw regio nu gemakkelijker vinden met het nieuwe doorzoekbare vervolgkeuzemenu, waarin zoek en vervolgkeuzelijst in één besturingselement worden gecombineerd. Deze update wordt eind maart uitgevoerd. |
| Nieuwe lijststructuur voor [&#x200B; de Partij van Snowflake &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md) bestemmingen | Tabellen die worden gedeeld in uw Snowflake-account, hebben nu een nieuwe structuur die aparte kolommen voor de naam van het publiek en de oorsprong van het publiek bevat. De nieuwe tabelstructuur is van toepassing op alle nieuwe doelverbindingen die zijn ingesteld om voorwaarts te gaan. Voor alle nieuwe verbindingen die u instelt, worden beide tabelstructuren gemaakt: de nieuwe structuur wordt voorafgegaan door V2 en de oude structuur blijft tot eind juni 2026 behouden, waarna deze wordt vervangen. Lees meer in de [&#x200B; Uitgevoerde gegevens &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) sectie van de documentatie van de Partij van Snowflake. Deze update wordt eind maart uitgevoerd. |
| [&#x200B; Adobe Advertising DSP &#x200B;](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md) verbinding | De nieuwe Adobe Advertising DSP-verbinding biedt dezelfde functionaliteit als de oude verbinding plus ondersteuning voor extra identiteiten. Met de nieuwe connector kunt u op cookies gebaseerde identiteiten ook exporteren naar Adobe Advertising DSP. |
| [&#x200B; FreeWheel &#x200B;](../../destinations/catalog/advertising/freewheel.md) verbinding | Verzend [!DNL Real-Time CDP] publiek naar FreeWheel als dagelijkse batchbestanden, zodat u deze kunt gebruiken in FreeWheel-deals en -campagnes op CTV, video en weergave. Neem contact op met uw Adobe-accountteam voor toegang. |
| De externe publiekssteun voor [&#x200B; Commerciële Desk CRM &#x200B;](../../destinations/catalog/advertising/tradedesk-emails.md) en [&#x200B; Pinterest &#x200B;](../../destinations/catalog/advertising/pinterest.md) | U kunt nu soorten publiek activeren, van oorsprong buiten Segmentation Service tot The Trade Desk CRM, Criteo en Pinterest, inclusief publiek voor aangepaste upload (geïmporteerd vanuit CSV), look-alike soorten publiek, gefedereerd publiek en publiek dat is gemaakt in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] . Deze update wordt eind maart uitgevoerd. Zie [&#x200B; gesteunde publiek &#x200B;](../../destinations/catalog/advertising/criteo.md#supported-audiences) sectie op de cataloguspagina van elke bestemming voor details. |
| Hogere limiet voor aangepast uploadpubliek | U kunt nu maximaal 20 aangepaste uploadsoorten per doelinstantie activeren. Eerder was deze limiet 10. Zie de [&#x200B; bestemmingsgidsen &#x200B;](../../destinations/guardrails.md#batch-file-based-activation) voor details. |
| [&#x200B; dossier van de Uitvoer nu &#x200B;](../../destinations/ui/export-file-now.md) en [&#x200B; ad-hoc activering API &#x200B;](../../destinations/api/ad-hoc-activation-api.md) steun voor extern publiek | U kunt nu de API voor activering van het bestand nu exporteren (UI) en de API voor ad-hocactivering gebruiken met een extern publiek (zoals aangepaste upload, look-alike, federated en publiek van andere Experience Platform-apps) wanneer u activeert naar batchbestemmingen op basis van bestanden. Deze update wordt eind maart uitgevoerd. |
| [&#x200B; HTTP API &#x200B;](../../destinations/catalog/streaming/http-destination.md) bestemmingen met OAuth 2 en mTLS | U kunt de bestemmingen van HTTP nu tot stand brengen en voor authentiek verklaren API die OAuth 2 gebruiken wanneer het authentificatieeindpunt wederzijdse TLS (mTLS) vereist; symbolische herwinning tijdens bestemmingsopstelling steunt nu mTLS. Deze update wordt eind maart uitgevoerd. |

{style="table-layout:auto"}

**Bevestigingen en verbeteringen**

| Repareren | Beschrijving |
| --- | --- |
| [&#x200B; TikTok &#x200B;](../../destinations/catalog/social/tiktok.md) hashing van het schakelaartelefoonaantal | Probleem verholpen waarbij een onjuiste configuratie van de doelkaart betekende dat identiteiten die van telefoonnummers werden afgehaald, niet werden geactiveerd voor TikTok. Om van deze moeilijke situatie te profiteren, opstelling een nieuwe activeringsstroom, of verwijder de afbeelding van het telefoonaantal uit uw bestaande stroom, bewaar het, en voeg het opnieuw toe. |
| [&#x200B; Snowflake het Streamen &#x200B;](../../destinations/catalog/warehouses/snowflake.md) en [&#x200B; de 3 bevestiging van identiteitskaart van de Partij van Snowflake &lbrace;](../../destinations/catalog/warehouses/snowflake-batch.md) | Er is een validator voor reguliere expressies toegevoegd aan de stap Account ID. Wanneer u uw id invoert, wordt deze nu gevalideerd om te zorgen dat de organisatie-id en de account-id de juiste indeling hebben (gescheiden door een punt). Deze update wordt eind maart uitgevoerd. |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

| Functie | Beschrijving |
| --- | --- |
| XDM-entiteitsacties en ondersteuning verwijderen | U hebt rechtstreeks vanuit inline tabelmenu&#39;s en detailpaginakopmenu&#39;s toegang tot handelingen voor schema&#39;s, klassen, veldgroepen en gegevenstypen. Als u de vereiste toestemmingen hebt, kunt u de entiteiten van uw organisatie ook schrappen wanneer zij niet door datasets en niet toegelaten voor Profiel worden gebruikt. Zie de [&#x200B; gids XDM UI &#x200B;](../../xdm/ui/explore.md) voor meer details. |

Voor meer informatie raadpleegt u het [overzicht van XDM](../../xdm/home.md).

## Real-Time Customer Profile {#real-time-customer-profile}

Het profiel van de Klant in real time geeft u een volledige mening van elke individuele klant door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens te combineren. Gebruik Profiel om uw klantgegevens te consolideren in een verenigde weergave die een actionable, tijdstempelaccount van elke klantinteractie biedt.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Gebeurtenissen | U kunt nu de terugzoekperiode van gebeurtenissen instellen wanneer u door uw profielen bladert. Dit laat u de gebeurtenissen zien waaraan het profiel voor de gespecificeerde tijdspanne wordt geassocieerd. Voor meer informatie, lees de [&#x200B; gids UI van het Profiel &#x200B;](../../profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [[!DNL Real-Time Customer Profile] overzicht](../../profile/home.md).

## Uitvoeren en werken {#run-and-operate}

Inspecteer, los problemen op, en optimaliseer uw implementaties van Experience Platform met de Looppas en werkende hulpmiddelen. Verbeter zicht in geplande partijactiviteiten, identificeer configuratiekwesties, en verbeter systeembetrouwbaarheid.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [&#x200B; Planningen van de Baan &#x200B;](../../run-and-operate/job-schedules.md) algemene beschikbaarheid | [!DNL Job Schedules] verstrekt een verenigde mening van alle geplande banen van de partijverwerking over uw gegevenspijpleiding, van opname door bestemmingsactivering. Inspecteer uitvoeringsstatus, identificeer het plannen conflicten, en diagnoseer configuratiekwesties alvorens zij uw bedrijfsverrichtingen beïnvloeden. |
| [&#x200B; de Controles van de Gezondheid &#x200B;](../../run-and-operate/health-checks.md) algemene beschikbaarheid | Het slechte schema en de identiteitsconfiguraties leiden tot significante stroomafwaartse kwesties, met inbegrip van onjuiste profielverwezenlijking, ontbroken segmentkwalificatie, en onnauwkeurige activering. <br> de controles van de Gezondheid verschuiven uw benadering van het reactieve oplossen van problemen aan pro-actief, preventief onderhoud. De controles van de gezondheid zijn altijd-op scans van uw schema&#39;s en identiteiten die in uw zandbak worden gebruikt en verstrekken een overzicht van kwesties die u kunt gebruiken om te onderzoeken en problemen op te lossen. |

{style="table-layout:auto"}

Voor meer informatie, lees de [&#x200B; Looppas en geef overzicht &#x200B;](../../run-and-operate/overview.md) in werking, [&#x200B; inspecteer baanprogramma&#39;s &#x200B;](../../run-and-operate/job-schedules.md), en de [&#x200B; gids UI van het Platform &#x200B;](../../landing/ui-guide.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Type ontsteking | U kunt nu het innametype van uw kenmerken weergeven. Zo weet u waar uw gegevens vandaan komen, zodat u een beter publiek kunt maken. Voor meer informatie over deze eigenschap, lees de [&#x200B; gids van de Bouwer van het Segment &#x200B;](../../segmentation/ui/segment-builder.md). |
| Samenvattingsgegevens | U kunt nu de samenvattingsgegevens voor uw kenmerken voor account en op personen gebaseerd publiek weergeven. Voor meer informatie over deze eigenschap in rekeningspubliek, lees de gids van de Bouwer van het publiek van de rekening [&#x200B; &#x200B;](../../rtcdp/segmentation/audience-builder.md). Voor meer informatie over deze eigenschap in op mensen-gebaseerd publiek, lees de [&#x200B; gids van de Bouwer van het Segment &#x200B;](../../segmentation/ui/segment-builder.md). |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Gebruik deze bronverbindingen om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestitielooppas te plaatsen, en gegevensingevoerproductie te beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| Nieuwe IP adressen aan lijst van gewenste personen | Nieuwe IP adressen voor GBR9: Het Verenigd Koninkrijk is toegevoegd aan de lijst van adressen u moet lijsten van gewenste personen verzekeren succesvolle partijbronverbindingen aan Experience Platform op Azure. Bekijk de lijst in de [&#x200B; IP gids van de lijst van gewenste personen van het adres &#x200B;](../../sources/ip-address-allow-list.md#gbr9-united-kingdom) voor meer informatie. |
| Verbeterde ondersteuning voor het vastleggen van gegevens wijzigen | U kunt Gegevens wijzigen nu gebruiken met de bronnen [!DNL Marketo Engage] , [!DNL Microsoft Dynamics] en [!DNL Salesforce CRM] . |
| Verbeterde verificatiegids voor [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | De verificatiegids voor de [!DNL Google BigQuery] -bron is uitgebreid met de volgende informatie: <ul><li>Het noodzakelijke werkingsgebied voor vernieuwt teken.</li><li>De IAM-rollen die vereist zijn voor de [!DNL Google] -identiteit.</li><li>Aanvullende instructies voor het gebruik van `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).
