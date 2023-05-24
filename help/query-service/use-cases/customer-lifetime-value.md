---
title: Gegevenssignalen bijhouden om de levenswaarde van uw klant te genereren
description: Deze gids verstrekt een demonstratie van begin tot eind op hoe te om Gegevens Distiller en user-defined dashboards met Real-time Customer Data Platform te gebruiken om de waarde van het klantenleven te meten en te visualiseren.
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# De gegevenssignalen van het spoor om uw waarde van het klantenleven te produceren

U kunt Real-time Customer Data Platform gebruiken om de waarde van het klantenleven (CLV) te volgen en die metrisch met user-defined dashboards te visualiseren. Door het gebruik van Gegevens Distiller en user-defined dashboards, kunt u meten hoe waardevol een klant aan uw bedrijf over de gehele lijn van uw verhouding is. Kennis van CLV kan u helpen de strategieën van uw zaken ontwikkelen om nieuwe klanten te verwerven terwijl het handhaven van bestaande degenen en het handhaven van winstmarges.

De volgende infografische weergave toont de cyclus van gegevensverzameling, manipulatie, analyse en actuatie die krachtige gegevens genereert om uw marketingcampagnes te verbeteren.

![De round-trip-infografische gegevens van observatie tot analyse tot actie.](../images/use-cases/infographic-use-case-cycle.png)

Dit gebruiksgeval van begin tot eind toont aan hoe de gegevenssignalen kunnen worden gevangen en worden gewijzigd om de waarde afgeleide van de klantenlevensduur te berekenen. Deze afgeleide attributen kunnen dan op uw het profielgegevens van Real-Time CDP worden toegepast en zijn beschikbaar voor gebruik met user-defined dashboards om een dashboard voor inzicht analyse te bouwen. Via Data Distiller kunt u het Real-Time CDP-gegevensmodel voor inzichten uitbreiden en het op CLV gebaseerde kenmerk en dashboardinzichten gebruiken om een nieuw segment te maken en het te activeren op een gewenst doel. Deze segmenten kunnen dan worden gebruikt om krachtige soorten publiek te creëren om uw volgende marketing campagne te drijven.

Deze gids wordt ontworpen om u te helpen uw klantenervaring beter begrijpen door gegevenssignalen over zeer belangrijke aanraakpunten te meten die CLV drijven en een gelijkaardig gebruiksgeval in uw milieu uitvoeren. Het volledige proces wordt samengevat in de onderstaande afbeelding.

![Een infografisch van de brede stappen die worden vereist om de waarde van het klantenleven te gebruiken.](../images/use-cases/implementation-steps.png)

## Aan de slag {#getting-started}

Voor deze handleiding is een goed begrip vereist van de volgende onderdelen van Adobe Experience Platform:

* [Query-service](../home.md): Verstrekt een gebruikersinterface en een RESTful API waar u SQL vragen kunt gebruiken om uw gegevens te analyseren en te verrijken.
* [Segmenteringsservice](../../segmentation/home.md): Staat u toe om segmenten te bouwen en publiek van uw gegevens van het Profiel van de Klant in real time te produceren.

## Vereisten

Voor deze handleiding hebt u de [Data Distiller](../data-distiller/overview.md) SKU als onderdeel van uw pakketaanbieding. Neem contact op met uw vertegenwoordiger van de Adobe-service als u niet zeker weet of u dit doet.

## Een afgeleid kenmerk maken {#create-derived-attribute}

De eerste stap in het vestigen van uw CLV is een afgeleid attribuut van de gegevenssignalen tot stand te brengen die van gebruikersacties worden gevangen. Deze specifieke gebruikszaak wordt vastgelegd in een afzonderlijk document over een loyaliteitsregeling voor luchtvaartmaatschappijen. Zie de handleiding voor meer informatie over [Gebruik de Dienst van de Vraag om op decile gebaseerde afgeleide attributen voor gebruik met uw profielgegevens tot stand te brengen](./deciles-use-case.md). Het document bevat volledige voorbeelden en uitleg waarin de volgende stappen worden toegelicht:

* Creeer een schema om voor het decile emmering toe te staan.
* Gebruik Query Service om deciles te maken.
* Decile datasets genereren.
* Schakel het schema in voor gebruik in Real-Time Klantprofiel.
* Maak een naamruimte voor de identiteit en markeer deze als primaire id.
* Creeer een vraag om deciles over een raadplegingsperiode te berekenen.

## Het gegevensmodel en de planningsupdates van inzichten uitbreiden {#extend-data-model-and-set-refresh-schedule}

Vervolgens moet u een aangepast gegevensmodel maken of een bestaand Adobe Real-Time CDP-gegevensmodel uitbreiden voor de toepassing van uw CLV-rapporteringsinzichten. Raadpleeg de documentatie voor meer informatie over [bouw een rapporterend gegevensmodel van inzichten door de Dienst van de Vraag voor gebruik met versnelde opslaggegevens en user-defined dashboards](../data-distiller/query-accelerated-store/reporting-insights-data-model.md#build-a-reporting-insights-data-model). De zelfstudie behandelt de volgende stappen:

* Een model maken voor het rapporteren van inzichten met Data Distiller.
* Tabellen, relaties en gegevens vullen.
* Vraag het rapporteringsgegevensmodel van inzicht.
* Vergroot uw gegevensmodel met het Real-Time CDP-gegevensmodel voor inzichten.
* Maak dimensietabellen om uw rapporteringsinzichten-model uit te breiden.
* Vraag uw uitgebreide versnelde opslagrapportering van inzichten gegevensmodel

Raadpleeg de documentatie bij het Real-time Customer Data Platform Insights-gegevensmodel voor meer informatie over [Pas uw SQL vraagmalplaatjes aan om de rapporten van Real-Time CDP voor uw marketing en zeer belangrijke gebruiksgevallen van de prestatiesindicator (KPI) te creëren](../../dashboards/cdp-insights-data-model.md).

Zorg ervoor om een programma te plaatsen om uw model van douanegegevens op een regelmatige kadentie te verfrissen. Dit zorgt ervoor dat de gegevens terug binnen als deel van uw innamepijplijn zoals nodig komen, en bevolkt uw user-defined dashboards. Zie de [naslaggids](../ui/query-schedules.md#create-schedule) om te leren hoe u uw schema instelt.

## Een dashboard maken om inzichten vast te leggen {#build-a-custom-dashboard}

Nu u uw model van douanegegevens hebt gecreeerd, bent u bereid om uw gegevens met douanevragen en user-defined dashboards te visualiseren. Zie het door de gebruiker gedefinieerde dashboards-overzicht voor volledige richtlijnen over hoe u [een aangepast dashboard maken](../../dashboards/user-defined-dashboards.md). De UI-handleiding bevat informatie over:

* Een widget maken.
* De widgetcomposer gebruiken.

Voorbeelden van aangepaste CLV-widgets die gebruik maken van decile-emmers, zijn hieronder te zien.

![Een verzameling aangepaste, op decile gebaseerde CLTV-widgets.](../images/use-cases/deciles-user-defined-dashboard.png)

## Maak en activeer segmenten om een krachtig publiek te maken {#create-and-activate-segments}

De volgende stap is segmenten te bouwen en publiek van uw gegevens van het Profiel van de Klant in real time te produceren. Zie de handleiding van de Bouwer van het Segment UI om te leren hoe te [segmenten in Platform maken en activeren](../../segmentation/ui/segment-builder.md). De gids verstrekt secties over hoe te:

* Maak segmentdefinities met een combinatie van kenmerken, gebeurtenissen en bestaand publiek als bouwstenen.
* Gebruik het canvas en de containers van de regelbouwer om de orde te controleren waarin de segmentregels worden uitgevoerd.
* De schattingen van de mening van uw potentiële publiek, toestaand u om uw segmentdefinities zonodig aan te passen.
* Schakel alle segmentdefinities in voor geplande segmentatie.
* Hiermee kunt u opgegeven segmentdefinities voor streaming segmentatie inschakelen.

Er is ook een [videozelfstudie voor het samenstellen van segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) voor meer informatie.

## Uw segment activeren voor een e-mailcampagne {#activate-segment-for-campaign}

Nadat u het segment hebt gemaakt, kunt u het activeren op een bestemming. Platform biedt ondersteuning voor diverse ESP&#39;s (Email Service Providers) waarmee u uw marketingactiviteiten voor e-mail kunt beheren, zoals het verzenden van promotionele e-mailcampagnes.

Controleer de [Overzicht van e-mailmarketingdoelen](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/overview.html?lang=en#connect-destination) voor een lijst van de gesteunde bestemmingen die u gegevens naar wilt uitvoeren (bijvoorbeeld [Oracle Eloqua](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/oracle-eloqua-api.html?lang=en) pagina).

## Bekijk de geretourneerde analysegegevens van uw campagne {#post-campaign-data-analysis}

De gegevens uit bronnen kunnen nu [incrementeel verwerkt](../essential-concepts/incremental-load.md) als onderdeel van een geplande vernieuwing naar uw gegevensmodel in de versnelde gegevensopslag. Alle responsgebeurtenissen van klanten kunnen in Adobe Experience Platform worden opgenomen, zoals ze plaatsvinden of in batches. Afhankelijk van uw instellingen of bronconnectors, kan uw gegevensmodel één keer of meerdere keren per dag worden vernieuwd. Zie de [overzicht van batch-invoer-API](../../ingestion/batch-ingestion/api-overview.md) of de [overzicht van streaming opname](../../ingestion/streaming-ingestion/overview.md) voor meer informatie .

Zodra uw gegevensmodel wordt bijgewerkt, verstrekken uw douane dashboardwidgets zinvolle signalen die u toestaan om de waarde van het klantenleven te meten en te visualiseren.

![Een aangepaste widget voor het aantal e-mailberichten dat wordt geopend op basis van hun segment- en e-mailcampagne.](../images/use-cases/post-activation-and-email-response-kpis.png)

Er zijn verschillende visualisatieopties beschikbaar voor uw aangepaste analyse.

![De e-mail die wordt geopend door de widget voor campagnemammers.](../images/use-cases/email-opened-by-campaign-buckets.png)

Deze inzichten kunnen u beurtelings helpen uw bedrijfsstrategieën voor verdere campagnes ontwikkelen.

![Een verzameling van vier aangepaste widgets die de resultaten van de e-mailcampagne gedetailleerd weergeven.](../images/use-cases/example-widgets.png)

## Volgende stappen

Door dit document te lezen, hebt u beter inzicht in hoe u Real-time Customer Data Platform kunt gebruiken om de maatstaf van de levensduur van de klant (CLV) te volgen en visualiseren. Als u meer wilt weten over de vele gevallen van zakelijk gebruik die worden beschreven via Query Service en Experience Platform, kunt u het beste de volgende documenten lezen:

* [Een voorbeeld van begin tot eind van verlaten doorbladert gebruiksgeval dat de veelzijdigheid en de voordelen van de Dienst van de Vraag aantoont.](./abandoned-browse.md)
* [De Query-service en het leren van computers gebruiken om beide activiteiten te bepalen en te filteren op basis van echt internetverkeer voor bezoekers](./bot-filtering.md)
* [Hoe te om een gelijke op uw gegevens van het Platform uit te voeren die resultaten van veelvoudige datasets door ongeveer een koord van uw keus combineert.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
