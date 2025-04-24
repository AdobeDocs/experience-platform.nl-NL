---
title: Aanvullende informatie van april 2024 voor Adobe Experience Platform
description: Aanvullende informatie van april 2024 voor Adobe Experience Platform.
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 98%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: 30 april 2024**

>[!TIP]
>
>Gebruik de [verklarende woordenlijst van Adobe Experience Platform](/help/landing/glossary.md) om vertrouwd te raken met terminologie die in Real-time Customer Data Platform en Adobe Experience Platform wordt gebruikt. Als u een specifieke term niet kunt vinden, kunt u via de feedbackopties op de pagina een verzoek indienen om nieuwe termen aan de woordenlijst toe te voegen.

Updates van bestaande functies in Experience Platform:

- [Dashboards](#dashboards)
- [Dataverzameling](#data-collection)
- [Bestemmingen](#destinations)
- [Identiteitsservice](#identity-service)
- [Bewaking](#monitoring)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten kunt bekijken over de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Real-Time Customer Data Platform B2B-inzichten | Ontdek vooraf geconfigureerde [Real-Time CDP B2B-gegevensinzichten voor accounts en mogelijkheden](../../dashboards/insights/account-profiles.md) om u te helpen uw gegevens te begrijpen en weloverwogen zakelijke beslissingen te nemen. U kunt ook [uw eigen inzichten bouwen met behulp van het Real-Time CDP B2B-datamodel](../../dashboards/data-models/cdp-insights-data-model-b2c.md) om uw gegevens te visualiseren en te verkennen en uw aangepaste visualisaties op te slaan in uw dashboard. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, inclusief het verlenen van toegangsrechten en het maken van aangepaste widgets, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensies | [!DNL Acxiom Anonymous Visitor Insights]Tags-extensie | Ontdek waar uw websitebezoekers vandaan komen met [!DNL Acxiom's Visitor Insights]. Acxiom kan de locatie van anonieme browsers bepalen door gebruik te maken van geografische IP-opzoektechnologie. Zodra de informatie is geïdentificeerd, levert een zoekopdracht in de georganiseerde database aanvullende inzichten op die naar de browser worden teruggestuurd. Contentmakers kunnen hun content zo afstemmen op deze datapunten. Zo kunnen ze bezoekers een persoonlijkere en boeiendere ervaring bieden, zelfs als ze in eerste instantie nog onbekenden zijn. |
| Gegevensstromen | [Edge Network-botdetectie](../../datastreams/bot-detection.md) | Verkeer afkomstig van niet-menselijke entiteiten, zoals geautomatiseerde programma&#39;s, web scrapers, spiders en scriptscanners, kan het moeilijker maken om gebeurtenissen van menselijke bezoekers te identificeren. Dit soort verkeer kan belangrijke bedrijfsstatistieken negatief beïnvloeden, wat kan leiden tot onjuiste verkeersrapportage. <br> Bot de opsporing staat u toe om gebeurtenissen te identificeren die door [ SDK van het Web ](../../web-sdk/home.md) worden geproduceerd, [ Mobiele SDK ](https://developer.adobe.com/client-sdks/home/) en [[!DNL Edge Network API] ](https://developer.adobe.com/data-collection-apis/docs/getting-started/) zoals die door bekende spinnen en bots worden geproduceerd. Door botdetectie voor uw datastreams te configureren, kunt u specifieke IP-adressen, IP-bereiken en verzoekheaders identificeren die u als botgebeurtenissen wilt classificeren. <br>De identificatie van botverkeer kan u een nauwkeurigere meting van de gebruikersactiviteit op uw site of mobiele app bieden. |
| Mobile SDK | Release van primaire versie | Er zijn nieuwe primaire versies van de Mobile SDK uitgebracht voor de volgende platforms: iOS Mobile Core 5.x en compatibele iOS-extensies, Android Mobile Core 3.x en compatibele Android-extensies, React Native Core 6.x en compatibele React Native-extensies, Flutter Core 4.x en compatibele Flutter-extensies. Deze releases bieden diverse nieuwe functies en verbeteringen, waaronder ondersteuning in de Android SDK voor Jetpack Compose, ondersteuning voor op code gebaseerde ervaringen van Adobe Journey Optimizer en algemene beschikbaarheid van de Adobe Journey Optimizer Messaging-extensie voor Flutter. Voor meer gedetailleerde aanvullende informatie, raadpleegt u de [aanvullende informatie voor Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobile SDK | Privacy | Vanwege de beleidsupdate van Apple, die op 1 mei 2024 ingaat, moeten ontwikkelaars nieuwe privacyfuncties implementeren om apps bij de App Store in te dienen. Alle Adobe-klanten die de Mobile SDK gebruiken, moeten upgraden naar versie 5.x van de SDK als ze na 1 mei goedkeuring van de App Store willen ontvangen. |
| Roku SDK | Roku SDK | De eerste grote versie van de Roku SDK is uitgebracht met ondersteuning voor de Streaming Media voor het Experience Platform Edge Network. |
| Tags en gebeurtenis doorsturen | Richtlijnen voor in-product | De functies [Tags](../../tags/home.md) en [Gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) van Experience Platform bieden een nieuwe reeks ervaringen waarmee u snel aan de slag kunt en snel waarde kunt creëren. Deze ervaringen omvatten nieuwe schermen voor onboarding, tutorials voor producten en tooltips.  <br>![Gebeurtenis doorsturen met de richtlijnen voor in-product gemarkeerd.](../2024/assets/april/event-forwarding.png "De Schema-editor met de velden Type en Type toewijzingswaarde gemarkeerd."){width="100" zoomable="yes"}<br> |
| Web SDK | Vereenvoudigde toepassing van de Web SDK voor Audience Manager-klanten | Meerdere Web SDK-updates vereenvoudigen nu de toepassing van Web SDK zonder dat u Experience-datamodel (XDM) hoeft te gebruiken voor Experience Cloud Solutions, zoals Audience Manager, Analytics en Target. Meer informatie over de toepassing van Audience Manager Web SDK vindt u in de volgende handleidingen: <ul><li><a href="https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Werk uw bibliotheek voor dataverzameling voor Audience Manager bij van de Audience Manager-tagextensie naar de Web SDK-tagextensie</li><li><a href="https://experienceleague.adobe.com/nl/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Werk uw bibliotheek voor dataverzameling voor Audience Manager bij van de AppMeasurement JavaScript-bibliotheek naar de Web SDK JavaScript-bibliotheek</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Voor meer informatie over dataverzamelingen, raadpleegt u het [overzicht van dataverzamelingen](../../collection/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| `isRequired`-parameter is nu beschikbaar voor geneste klantgegevensvelden in Destination SDK | Wanneer u een bestemming in de Destination SDK configureert, kunt u nu [geneste klantgegevensvelden instellen indien nodig](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). Op deze manier kunnen gebruikers die uw bestemming instellen, niet doorgaan met hun activeringsstroom totdat ze een waarde voor dat veld hebben geselecteerd. |
| Edge-segmentatie is niet langer een verplichte vereiste bij het instellen van een Adobe Target-bestemming met Web SDK | Voorheen moest bij het configureren van een [Adobe Target-bestemming](/help/destinations/catalog/personalization/adobe-target-connection.md) met Web SDK de gegevensstroom worden ingeschakeld voor personalisatie en Edge-segmentatie. De vereiste voor het inschakelen van gegevensstroom voor Edge-segmentatie [is nu verwijderd](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). Houd er rekening mee dat u met dit integratiepatroon alleen kunt profiteren van een subset van personalisatiegebruiksscenario&#39;s als u Adobe Target gebruikt met Real-Time CDP. Meer informatie over de [gebruikssecenario&#39;s die door het integratietype worden toegelaten](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases). |
| [!BADGE Beta]{type=Informative} Meerdere doelgroepen en datasets uit activeringsworkflows verwijderen | U kunt nu meerdere soorten doelgroepen en datasets selecteren en verwijderen uit workflows voor bestemmingsactivering. Zie de documentatie over [bestemmingsgegevens](../../destinations/ui/destination-details-page.md#bulk-remove) en [het exporteren van datasets](../../destinations/ui/export-datasets.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Identiteitsservice {#identity-service}

Met Identity Service van Adobe Experience Platform krijgt u een uitgebreid beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen, zodat u in real-time een impactvolle, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Afschaffing van de `/orgs/{ORG}/`-eindpunten in de API | De volgende eindpunten in de [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) zijn afgeschaft:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> U kunt de `/idnamespace/identities`- en `/idnamespace/identities/{ID}`-eindpunten gebruiken om dezelfde taken uit te voeren en alle naamruimten in een organisatie of een specifieke naamruimte in een organisatie op te halen. |

{style="table-layout:auto"}

Voor meer informatie over Identity Service, raadpleegt u het [overzicht van Identity Service](../../identity-service/home.md).

## Bewaking {#monitoring}

Gebruik het controledashboard in de gebruikersinterface van Experience Platform om het traject van uw gegevens vanuit bronnen, Identity Service, Real-Time Customer Profile, doelgroepen en bestemmingen te controleren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Uitbreiding voor het controledashboard | U kunt nu het controledashboard voor verschillende gegevenstypes op basis van uw zakelijke gebruiksscenario gebruiken. Gebruik het controledashboard om activiteiten op het gebied van persoons-, account- en prospectgegevens in bronnen, doelgroepen en bestemmingen te controleren. |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u de handleiding over [het gebruik van het controledashboard](../../dataflows/ui/monitor.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake]. U kunt willekeurige datasets van [!DNL Data Lake] combineren en de queryresultaten vastleggen als nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Query-quarantine | Isoleer automatisch mislukte query-uitvoeringen om onderbrekingen te voorkomen en consistente prestaties te behouden. Zie de documentatie over [query-quarantaine](../../query-service/ui/query-schedules.md#quarantine) voor meer informatie. |
| Query annuleren | Neem de controle over de uitvoering van query&#39;s en verbeter uw productiviteit door langlopende query&#39;s te annuleren. Zie de documentatie voor het [annuleren van query&#39;s](../../query-service/ui/user-guide.md#cancel-query) voor meer informatie. |
| Geplande query-waarschuwingen | Blijf op de hoogte van proactieve meldingen tijdens het plannen van query&#39;s, zodat u over een efficiënt en tijdig taakbeheer beschikt. U kunt zich [abonneren op meldingen wanneer u een query maakt](../../query-service/ui/query-schedules.md#alerts-for-query-status) of de inline acties voor bestaande geplande query&#39;s gebruikt. Zie de documentatie over het [abonneren op meldingen met inline acties](../../query-service/ui/monitor-queries.md#alert-subscription) voor meer informatie. |
| Verbeterde geplande query-navigatie | Navigeer eenvoudig tussen querysjablonen en geplande uitvoeringen voor een hogere productiviteit. Zie de documentatie over [geplande query-uitvoeringen weergeven](../../query-service/ui/query-schedules.md#scheduled-query-runs) voor meer informatie. |
| Uitgebreide query-uitvoer | Krijg toegang tot maximaal 500 rijen met queryresultaten in de console voor een diepgaandere analyse van uw gegevens. Raadpleeg de documentatie over het [aantal resultaten](../../query-service/ui/user-guide.md#result-count) voor meer informatie. |
| Afschaffing van de verouderde versie van Query-editor | Vanaf 30 april 2024 is de verbeterde Query-editor de standaardeditor voor alle gebruikers. De verouderde editor wordt op 24 mei 2024 afgeschaft en is niet meer beschikbaar voor gebruik. Zie het [handboek voor Query-editor](../../query-service/ui/user-guide.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over Query-services raadpleegt u het [overzicht van Query-services](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om digitale ervaringstoepassingen wereldwijd te verrijken. Bedrijven gebruiken vaak meerdere digitale ervaringstoepassingen parallel en moeten de ontwikkeling, het testen en de implementatie van deze toepassingen verzorgen en tegelijkertijd de operationele naleving waarborgen. Om aan deze behoefte te voldoen biedt Experience Platform sandboxes die één Experience Platform-instantie opsplitsen in afzonderlijke virtuele omgevingen, zodat digitale ervaringstoepassingen kunnen worden ontwikkeld en verbeterd.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [Sandbox-tools](../../sandboxes/ui/sandbox-tooling.md) | Gebruik sandbox-tools om alle ondersteunde objecttypen te [exporteren](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) naar een volledig sandboxpakket en [importeer](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) het pakket vervolgens in verschillende sandboxes om objectconfiguraties te repliceren. |

{style="table-layout:auto"}

Voor meer informatie over sandboxes, lees het [ overzicht van sandboxes](../../sandboxes/home.md).

## Segmentatieservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, prospects, gebruikers of organisaties) segmenteren in doelgroepen. U kunt doelgroepen maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile]-gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Experience Platform] en zijn gemakkelijk toegankelijk via elke Adobe-oplossing.

**Bijgewerkte functie**

| Functie | Beschrijving |
| ------- | ----------- |
| Levenscyclusstatussen van doelgroepen | De levenscyclusstatussen van doelgroepen zijn gestroomlijnd om het levenscyclusbeheer te vereenvoudigen. Voor meer informatie over deze levenscyclusstatussen, raadpleegt u de [veelgestelde vragen over de segmentatieservice](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van de segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Nieuwe bronnen**

| Nieuwe bronnen | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Gebruik de [[!DNL PathFactory] -bron](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) om uw bezoeker, sessie, en paginaweergavegegevens van [!DNL PathFactory] met Experience Platform te integreren. Raadpleeg het [[!DNL PathFactory] -overzicht](../../sources/connectors/marketing-automation/pathfactory.md) voor informatie over hoe u aan de slag kunt gaan. |
| [!DNL Teradata Vantage] | Gebruik de [[!DNL Teradata Vantage] bron](../../sources/tutorials/ui/create/databases/teradata-vantage.md) om gegevens uit hybride multi-cloudomgevingen aan Experience Platform toe te voegen. Raadpleeg het [[!DNL Teradata Vantage] overzicht](../../sources/connectors/databases/teradata-vantage.md) voor informatie over hoe u aan de slag kunt gaan. |

{style="table-layout:auto"}

**Nieuwe en bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates voor IP-adressen voor opname op de toelatingslijst in VA7 | De volgende IP-adressen zijn toegevoegd aan de lijst van IP-adressen om aan uw lijst van toegestane adressen voor VA7 (Noord-Amerika) toe te voegen: <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Voor een uitvoerige lijst van IP-adressen om aan uw lijst met toegestane adressen toe te voegen, raadpleegt u de [documentatie over toegestane IP-adressen](../../sources/ip-address-allow-list.md). |
| Ondersteuning voor nieuwe verificatietypen met de [!DNL Azure Event Hubs]-bron | U kunt nu uw [!DNL Event Hubs]-bron met Experience Platform verbinden met behulp van [!DNL Azure Active Directory Authentication] of [!DNL Scoped Azure Active Directory Authentication]. Raadpleeg de handleiding over [verbinding maken [!DNL Event Hubs]  met Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) voor meer informatie. |
| Updates voor het ophalen van [!DNL Data Landing Zone]-aanmeldingsgegevens | U kunt nu de rechterrail in de werkruimte voor bronnen gebruiken om uw [!DNL Data Landing Zone]-aanmeldingsgegevens op te halen. U kunt nu ook de rechterrail gebruiken om uw aanmeldingsgegevens te vernieuwen. Raadpleeg de [[!DNL Data Landing Zone] handleiding voor de gebruikersinterface](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) voor meer informatie. |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Voor meer informatie over bronnen, raadpleegt u het [overzicht van bronnen](../../sources/home.md).
