---
title: Aanvullende informatie van maart 2026 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2026 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8c55aebcb65327394ffbdf59db1d2a203182ed18
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 36%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!TIP]
>
>Raadpleeg de volgende documentatie voor aanvullende informatie voor andere Adobe Experience Platform-toepassingen:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/latest)
>- [Samenstelling van Federated-doelgroep](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/nl/docs/real-time-cdp-collaboration/using/latest)

**Releasedatum:woensdag 24 maart 2026**

Nieuwe functies en updates van bestaande functies in Adobe Experience Platform:

- [Geavanceerd beheer van de levenscyclus van gegevens](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Geavanceerd beheer van de levenscyclus van gegevens {#advanced-data-lifecycle-management}

Experience Platform biedt een reeks mogelijkheden voor Gegevensgezondheid waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentenrecords en datasets. Met de werkruimte van de Levenscyclus van Gegevens in de UI of aanroepen naar de API voor gegevenshygiëne kunt u uw gegevensopslagruimten effectief beheren. Met deze mogelijkheden kunt u ervoor zorgen dat informatie wordt gebruikt zoals verwacht, wordt bijgewerkt wanneer onjuiste gegevens moeten worden gecorrigeerd en wordt verwijderd wanneer het organisatiebeleid dit noodzakelijk acht.

| Functie | Beschrijving |
| --- | --- |
| Meerdere gegevenssets en record met alleen profiel verwijderen (alleen API) | U kunt één gegevensset-id, een door komma&#39;s gescheiden lijst met id&#39;s van gegevenssets of het letterlijke teken `ALL` in `datasetId` verzenden om id&#39;s te verwijderen uit een, veel of alle gegevenssets. U kunt het verwijderen ook beperken tot services met betrekking tot profielen door `targetServices` in te stellen op `["identity","profile","ajo"]` , waardoor de gegevens ongewijzigd blijven. Deze functionaliteit is alleen beschikbaar via de API voor gegevenshygiëne. Zie het [&#x200B; Verslag schrap de gids van de het werkorden &#x200B;](../../hygiene/api/workorder.md) voor meer details. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie het [overzicht van geavanceerd beheer van de levenscyclus van gegevens](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Met Agent Orchestrator kunt u op AI gebaseerde agents maken en implementeren die workflows kunnen automatiseren en op meerdere kanalen met klanten kunnen communiceren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [&#x200B; Adobe Marketing Agent voor  [!DNL Microsoft 365 Copilot] &#x200B;](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | De Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] is uw ingesloten agent die Adobe-marketinginformatie rechtstreeks in alledaagse programma&#39;s zoals [!DNL Teams] , [!DNL Word] , [!DNL PowerPoint] en andere [!DNL Microsoft 365] -apps plaatst. U kunt deze agent gebruiken om vertrouwde campagneinzichten van Adobe-toepassingen te gebruiken terwijl u campagnes plant, publiek controleert, met collega&#39;s samenwerkt om klantvragen te beantwoorden en om met gegevens geïnformeerde beslissingen te nemen zonder uw [!DNL Microsoft 365] -workflow te verlaten. |

{style="table-layout:auto"}

Raadpleeg de [documentatie over Agent Orchestrator](https://experienceleague.adobe.com/nl/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator) voor meer informatie.

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms waarmee gegevens uit Experience Platform naadloos kunnen worden geactiveerd. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| --- | --- |
| [&#x200B; Adobe Advertising DSP &#x200B;](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) verbinding | De nieuwe Adobe Advertising DSP-verbinding biedt dezelfde functionaliteit als de oude verbinding plus ondersteuning voor extra identiteiten. Met de nieuwe connector kunt u op cookies gebaseerde identiteiten ook exporteren naar Adobe Advertising DSP. |
| [&#x200B; FreeWheel &#x200B;](../../destinations/catalog/advertising/freewheel.md) verbinding | Verzend [!DNL Real-Time CDP] publiek naar FreeWheel als dagelijkse batchbestanden, zodat u deze kunt gebruiken in FreeWheel-deals en -campagnes op CTV, video en weergave. Neem contact op met uw Adobe-accountteam voor toegang. |
| De externe publiekssteun voor [&#x200B; Commerciële Desk CRM &#x200B;](../../destinations/catalog/advertising/tradedesk-emails.md) en [&#x200B; Pinterest &#x200B;](../../destinations/catalog/advertising/pinterest.md) | U kunt nu soorten publiek activeren, van oorsprong buiten Segmentation Service tot The Trade Desk CRM, Criteo en Pinterest, inclusief publiek voor aangepaste upload (geïmporteerd vanuit CSV), look-alike soorten publiek, gefedereerd publiek en publiek dat is gemaakt in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] . Deze update wordt eind maart uitgevoerd. Zie [&#x200B; gesteunde publiek &#x200B;](../../destinations/catalog/advertising/criteo.md#supported-audiences) sectie op de cataloguspagina van elke bestemming voor details. |
| Hogere limiet voor aangepast uploadpubliek | U kunt nu maximaal 20 aangepaste uploadsoorten per doelinstantie activeren. Eerder was deze limiet 10. Zie de [&#x200B; bestemmingsgidsen &#x200B;](../../destinations/guardrails.md#batch-file-based-activation) voor details. |
| [&#x200B; dossier van de Uitvoer nu &#x200B;](../../destinations/ui/export-file-now.md) en [&#x200B; ad-hoc activering API &#x200B;](../../destinations/api/ad-hoc-activation-api.md) steun voor extern publiek | U kunt nu de API voor activering van het bestand nu exporteren (UI) en de API voor ad-hocactivering gebruiken met een extern publiek (zoals aangepaste upload, look-alike, federated en publiek van andere Experience Platform-apps) wanneer u activeert naar batchbestemmingen op basis van bestanden. Deze update wordt eind maart uitgevoerd. |

{style="table-layout:auto"}

**Bevestigingen en verbeteringen**

| Repareren | Beschrijving |
| --- | --- |
| [&#x200B; TikTok &#x200B;](../../destinations/catalog/social/tiktok.md) hashing van het schakelaartelefoonaantal | Probleem verholpen waarbij een onjuiste configuratie van de doelkaart betekende dat identiteiten die van telefoonnummers werden afgehaald, niet werden geactiveerd voor TikTok. Om van deze moeilijke situatie te profiteren, opstelling een nieuwe activeringsstroom, of verwijder de afbeelding van het telefoonaantal uit uw bestaande stroom, bewaar het, en voeg het opnieuw toe. |

{style="table-layout:auto"}

Voor meer informatie leest u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

| Functie | Beschrijving |
| --- | --- |
| XDM-entiteitsacties en ondersteuning verwijderen | U hebt rechtstreeks vanuit inline tabelmenu&#39;s en detailpaginakopmenu&#39;s toegang tot handelingen voor schema&#39;s, klassen, veldgroepen en gegevenstypen. Als u de vereiste toestemmingen hebt, kunt u de entiteiten van uw organisatie ook schrappen wanneer zij niet door datasets en niet toegelaten voor Profiel worden gebruikt. Zie de [&#x200B; gids XDM UI &#x200B;](../../xdm/ui/explore.md) voor meer details. |

Voor meer informatie raadpleegt u het [overzicht van XDM](../../xdm/home.md).

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Doelgroepen kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Type ontsteking | U kunt nu het innametype van uw kenmerken weergeven. Zo weet u waar uw gegevens vandaan komen, zodat u een beter publiek kunt maken. Voor meer informatie over deze eigenschap, lees de [&#x200B; gids van de Bouwer van het Segment &#x200B;](/help/segmentation/ui/segment-builder.md). |
| Samenvattingsgegevens | U kunt nu de samenvattingsgegevens voor uw kenmerken voor account en op personen gebaseerd publiek weergeven. Voor meer informatie over deze eigenschap in rekeningspubliek, lees de gids van de Bouwer van het publiek van de rekening [&#x200B; &#x200B;](/help/rtcdp/segmentation/audience-builder.md). Voor meer informatie over deze eigenschap in op mensen-gebaseerd publiek, lees de [&#x200B; gids van de Bouwer van het Segment &#x200B;](/help/segmentation/ui/segment-builder.md). |

Voor meer informatie raadpleegt u het [[!DNL Segmentation Service] overzicht](../../segmentation/home.md).

## Bronnen

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte bronnen**

| Bron | Beschrijving |
| --- | --- |
| [!DNL Talon.One] | U kunt Experience Platform nu met [!DNL Talon.One] verbinden gebruikend de nieuwe [!DNL Talon.One] [&#x200B; partij &#x200B;](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) en [&#x200B; het stromen &#x200B;](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) bronnen. Gebruik de nieuwe bronnen om loyaliteitsprofielgegevens evenals transactie en loyaliteitsactiviteitengebeurtenissen aan Experience Platform in te voeren. |
| Nieuwe IP adressen aan lijst van gewenste personen | Nieuwe IP adressen voor GBR9: Het Verenigd Koninkrijk is toegevoegd aan de lijst van adressen u moet lijsten van gewenste personen verzekeren succesvolle partijbronverbindingen aan Experience Platform op Azure. Bekijk de lijst in de [&#x200B; IP gids van de lijst van gewenste personen van het adres &#x200B;](../../sources/ip-address-allow-list.md#gbr9-united-kingdom) voor meer informatie. |
| Verbeterde ondersteuning voor het vastleggen van gegevens wijzigen | U kunt Gegevens wijzigen nu gebruiken met de bronnen [!DNL Marketo Engage] , [!DNL Microsoft Dynamics] en [!DNL Salesforce CRM] . |
| Verbeterde verificatiegids voor [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | De verificatiegids voor de [!DNL Google BigQuery] -bron is uitgebreid met de volgende informatie: <ul><li>Het noodzakelijke werkingsgebied voor vernieuwt teken.</li><li>De IAM-rollen die vereist zijn voor de [!DNL Google] -identiteit.</li><li>Aanvullende instructies voor het gebruik van `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bronnen](../../sources/home.md).

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->