---
title: Opmerkingen bij de release Experience Platform
description: Een voorvertoning van de meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 5cbf63cc0a149d54de63e3e1797cae4098498fe8
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 29%

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

**Datum van de Versie: Maart 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Geavanceerd beheer van de levenscyclus van gegevens](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Bestemmingen](#destinations)
- [Query-service](#query-service)
- [Realtime-klantenprofiel](#profile)
- [Uitvoeren en werken](#run-and-operate)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Geavanceerd beheer van de levenscyclus van gegevens {#advanced-data-lifecycle-management}

Experience Platform biedt een reeks mogelijkheden voor Gegevensgezondheid waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentenrecords en datasets. U kunt uw gegevensopslag effectief beheren met de werkruimte van de gegevenslevenscyclus in de gebruikersinterface of via aanroepen naar de API voor Gegevensgezondheid. Met deze mogelijkheden kunt u ervoor zorgen dat informatie wordt gebruikt zoals verwacht, wordt bijgewerkt wanneer onjuiste gegevens moeten worden gecorrigeerd en wordt verwijderd wanneer het organisatiebeleid dit noodzakelijk acht.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Meerdere gegevenssets en alleen-profielrecord verwijderen (alleen API) | U kunt één gegevensset-id, een door komma&#39;s gescheiden lijst met id&#39;s van gegevenssets of het letterlijke teken `ALL` in `datasetId` verzenden om id&#39;s te verwijderen uit een, veel of alle gegevenssets. U kunt het verwijderen ook beperken tot profielservices door `targetServices` in te stellen op `["identity","profile","ajo"]` , waardoor de gegevens ongewijzigd blijven. Zie de [&#x200B; gids van de Orden van het Werk van de Schrapping van het Verslag &#x200B;](../hygiene/api/workorder.md) voor meer details. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie het [overzicht van geavanceerd beheer van de levenscyclus van gegevens](../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Met Agent Orchestrator kunt u op AI gebaseerde agents maken en implementeren die workflows kunnen automatiseren en op meerdere kanalen met klanten kunnen communiceren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] | De Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] is uw ingesloten agent die Adobe-marketinginformatie rechtstreeks in alledaagse programma&#39;s zoals [!DNL Teams] , [!DNL Word] , [!DNL PowerPoint] en andere [!DNL Microsoft 365] -apps plaatst. U kunt deze agent gebruiken om vertrouwde campagneinzichten van Adobe-toepassingen te gebruiken terwijl u campagnes plant, publiek controleert of met collega&#39;s samenwerkt, klantvragen beantwoordt en met gegevens geïnformeerde beslissingen neemt zonder uw [!DNL Microsoft 365] -workflow te verlaten. |

{style="table-layout:auto"}

Voor meer informatie, zie de [&#x200B; documentatie van Agent Orchestrator &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [&#x200B; de Gebied van de Partij van Snowflake &#x200B;](../destinations/catalog/warehouses/snowflake-batch.md) selecteur | U kunt uw regio nu gemakkelijker vinden met het nieuwe doorzoekbare vervolgkeuzemenu, waarin zoek en vervolgkeuzelijst in één besturingselement worden gecombineerd. |
| De meta-gegevens van het publiek van de uitvoer aan [&#x200B; Partij van Snowflake &#x200B;](../destinations/catalog/warehouses/snowflake-batch.md) bestemmingen | De bestanden die naar dit doel worden geëxporteerd, bevatten nu metagegevens voor het publiek. De nieuwe tabelstructuur is van toepassing op alle nieuwe doelverbindingen die zijn ingesteld om voorwaarts te gaan. De oude tabelstructuur wordt nog drie maanden bewaard voordat deze wordt vervangen. |
| [!DNL Adobe Advertising Cloud DSP]-verbinding | De nieuwe Adobe Advertising DSP-verbinding biedt dezelfde functionaliteit als de oude verbinding plus ondersteuning voor extra identiteiten. |
| De externe publiekssteun voor [&#x200B; Commerciële Desk CRM &#x200B;](../destinations/catalog/advertising/tradedesk-emails.md), [&#x200B; Criteo &#x200B;](../destinations/catalog/advertising/criteo.md) en [&#x200B; Pinterest &#x200B;](../destinations/catalog/advertising/pinterest.md) | U kunt publiek voorbij de segmenten van de Dienst van de Segmentatie aan The Trade Desk CRM, Criteo, en Pinterest nu activeren, met inbegrip van douane uploadt publiek (ingevoerd uit CSV), blik-alike publiek, federated publiek, en publiek dat in andere Experience Platform apps zoals Adobe Journey Optimizer wordt gecreeerd. Zie [&#x200B; gesteunde publiek &#x200B;](../destinations/catalog/advertising/criteo.md#supported-audiences) sectie op de cataloguspagina van elke bestemming voor details. |
| Hogere limiet voor aangepast uploadbereik | U kunt nu maximaal 20 aangepaste uploadsoorten per doelinstantie activeren. Eerder was deze limiet 10. |
| [&#x200B; dossier van de Uitvoer nu &#x200B;](../destinations/ui/export-file-now.md) en [&#x200B; ad-hoc activering API &#x200B;](../destinations/api/ad-hoc-activation-api.md) steun voor extern publiek | U kunt nu de API voor activering van het bestand nu exporteren (UI) en de API voor ad-hocactivering gebruiken met een extern publiek (zoals aangepaste upload, look-alike, federated en publiek van andere Experience Platform-apps) wanneer u activeert naar batchbestemmingen op basis van bestanden. |
| HTTP API-doelen met OAuth 2 en mTLS | U kunt de bestemmingen van HTTP nu tot stand brengen en voor authentiek verklaren API die OAuth 2 gebruiken wanneer het authentificatieeindpunt wederzijdse TLS (mTLS) vereist; symbolische herwinning tijdens bestemmingsopstelling steunt nu mTLS. |
| Doel ZoomInfo-account | U kunt nu accountpubliek naar ZoomInfo vanuit Real-Time Customer Data Platform (B2B) sturen. |

{style="table-layout:auto"}

**Bevestigingen en verbeteringen**

| Repareren | Beschrijving |
| --- | --- |
| [&#x200B; Snowflake die &#x200B;](../destinations/catalog/warehouses/snowflake.md) de bevestiging van identiteitskaart van de rekening stromen | Er is een validator voor reguliere expressies toegevoegd aan de stap Account ID. Wanneer u uw id invoert, wordt deze nu gevalideerd om te zorgen dat de organisatie-id en de account-id de juiste indeling hebben (gescheiden door een punt). |
| [&#x200B; TikTok &#x200B;](../destinations/catalog/social/tiktok.md) hashing van het schakelaartelefoonaantal | Probleem verholpen waarbij een onjuiste configuratie van de doelkaart betekende dat identiteiten die van telefoonnummers werden afgehaald, niet werden geactiveerd voor TikTok. |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../destinations/home.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Tijdkiezer voor profielgebeurtenissen | U kunt nu een tijdvenster instellen op het tabblad Profielgebeurtenissen om gebeurtenissen binnen dat bereik weer te geven en te analyseren. U kunt het tijdvenster instellen op maximaal 30 dagen. Standaard worden gebeurtenissen in de afgelopen 48 uur weergegeven. |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van het realtime-klantenprofiel](../profile/home.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake]. U kunt willekeurige datasets van [!DNL Data Lake] combineren en de queryresultaten vastleggen als nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Data Distiller Accelerators | U kunt nu een sneltoets kiezen op het tabblad Versnellers, de vereiste parameters invoeren en de gegenereerde SQL uitvoeren of plannen zonder deze zelf te schrijven. U kunt alle sneltoetsen klonen in een aangepaste sjabloon die u wilt bewerken. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; overzicht van de Dienst van de Vraag &#x200B;](../query-service/home.md).

## Uitvoeren en werken {#run-and-operate}

Inspecteer, los problemen op, en optimaliseer uw implementaties van Experience Platform met de Looppas en werkende hulpmiddelen. Verbeter zicht in geplande partijactiviteiten, identificeer configuratiekwesties, en verbeter systeembetrouwbaarheid.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [&#x200B; Planningen van de Baan &#x200B;](../run-and-operate/job-schedules.md) algemene beschikbaarheid | [!DNL Job Schedules] verstrekt een verenigde mening van alle geplande banen van de partijverwerking over uw gegevenspijpleiding, van opname door bestemmingsactivering. Inspecteer uitvoeringsstatus, identificeer het plannen conflicten, en diagnoseer configuratiekwesties alvorens zij uw bedrijfsverrichtingen beïnvloeden. |
| Gezondheidscontroles algemene beschikbaarheid | Het slechte schema en de identiteitsconfiguraties leiden tot significante stroomafwaartse kwesties, met inbegrip van onjuiste profielverwezenlijking, ontbroken segmentkwalificatie, en onnauwkeurige activering. <br> de controles van de Gezondheid verschuiven uw benadering van het reactieve oplossen van problemen aan pro-actief, preventief onderhoud. De controles van de gezondheid zijn altijd-op scans van uw schema&#39;s en identiteiten die in uw zandbak worden gebruikt en verstrekken een overzicht van kwesties die u kunt gebruiken om te onderzoeken en problemen op te lossen. |

{style="table-layout:auto"}

Voor meer informatie, lees de [&#x200B; Looppas en geef overzicht &#x200B;](../run-and-operate/overview.md) in werking, [&#x200B; inspecteer baanprogramma&#39;s &#x200B;](../run-and-operate/job-schedules.md), en de [&#x200B; gids UI van het Platform &#x200B;](../landing/ui-guide.md).

## Segmentatieservice {#segmentation}

Met Experience Platform kunt u publiekssegmenten maken op basis van uw klantgegevens en kunt u deze doelgroepen volledig in de levenscyclus beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ingestiebron in Audience Builder | U kunt nu zien of elk attribuut uit een partij, het stromen, of randbron binnen de Bouwer van de Publiek komt om het bouwen van ongeldig of inefficiënt het stromen publiek te vermijden. |
| Alleen velden met gegevens weergeven in de accountAudience Builder | U kunt nu filteren om alleen kenmerken weer te geven die gegevens bevatten wanneer u een accountpubliek maakt. |

{style="table-layout:auto"}

Voor meer informatie, lees het [&#x200B; overzicht van het publiek &#x200B;](../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| Verbeterde ondersteuning voor het vastleggen van gegevens wijzigen | U kunt Gegevens wijzigen nu gebruiken met de bronnen [!DNL Marketo Engage] , [!DNL Microsoft Dynamics] en [!DNL Salesforce CRM] . |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../sources/home.md).

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) multiregion support | The Snowflake Streaming connector is now available to customers beyond the US VA7 region. Use the region dropdown selector to select which Snowflake region your account is in. The documentation has been updated with the expected data structure for Snowflake streaming tables. |
| Audience filtering in activation workflow | You can now find and filter audiences in the **[!UICONTROL Select audiences]** step with the same experience as the Audiences page; for example, you can filter on audience origin to easily find the audience you are looking for. |

-->