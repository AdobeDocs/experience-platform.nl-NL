---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 22 juni 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Query-service](#query-service)
- [Real-time Customer Data Platform-verbindingen](#data-collection)
- [Bronnen](#sources)

## [!DNL Data Science Workspace] {#dsw}

De Werkruimte van de Wetenschap van gegevens gebruikt machine het leren en kunstmatige intelligentie om inzichten van uw gegevens te ontketenen. De Data Science Workspace is geïntegreerd in Adobe Experience Platform en helpt u om voorspellingen te maken met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen. Een van de manieren waarop de Werkruimte van de Wetenschap van Gegevens dit verwezenlijkt is door het gebruik van JupyterLab. JupyterLab is een webgebaseerde gebruikersinterface voor <a href="https://jupyter.org/" target="_blank">Jupyter-project</a> en is nauw geïntegreerd in Adobe Experience Platform. Het biedt een interactieve ontwikkelomgeving voor gegevenswetenschappers die werken met Jupyter-laptops, -code en -gegevens.

| Functie | Beschrijving |
| --- | --- |
| JupyterLab Launcher | De JupyterLab Launcher bevat nu startteksten voor Spark 3.2-laptops. Starters voor Spark 2.4-laptops worden nu vervangen door Spark 3.2-laptops en maken deel uit van deze release. |
| Vonk 3.2 | Nieuwe Scala (Vonk) en PySpark recepten gebruiken nu Vonk 3.2 |
| Kernels | Scala-laptops (Spark) zijn nu ontworpen via de Scala-kernel. PySpark laptops zijn nu ontworpen via de Python Kernel. De kernel van de Vonk en van PySpark wordt afgekeurd en geplaatst om in een verdere versie worden verwijderd. |
| Ontvangers | Nieuwe PySpark- en Spark-recepten volgen nu de Docker-workflow, vergelijkbaar met Python- en R-recepten. |

{style=&quot;table-layout:auto&quot;}

Voor meer algemene informatie over de Werkruimte van de Wetenschap van Gegevens, zie [overzichtsdocumentatie](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| (bèta) Destination SDK-ondersteuning voor [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) bestandsgebaseerde doelen en [configureerbare bestandsnamen](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | U kunt de Destination SDK nu gebruiken om Google Cloud Storage-doelen te maken en aangepaste bestandsnamen voor geëxporteerde bestanden te definiëren via bestandsnaammacro&#39;s. <br><br> Bestandsgebaseerde doelondersteuning in Adobe Experience Platform Destination SDK staat momenteel in bètaversie. De documentatie en functionaliteit kunnen worden gewijzigd. |
| De kolom van het segment in dataflow looppas aan partijbestemmingen | Voor dataflow looppas aan partijbestemmingen, UI toont nu de naam van het segment verbonden aan elke dataflow looppas. Meer informatie over [dataflow wordt uitgevoerd naar batchdoelen](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations). |

{style=&quot;table-layout:auto&quot;}

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [(bèta) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | De [!DNL Google Ad Manager 360] verbinding maakt batch-upload mogelijk voor [!DNL publisher provided identifiers] (PPID) in [!DNL Google Ad Manager 360], via [!DNL Google Cloud Storage] <br><br>Deze bestemming is momenteel in Bèta en is slechts beschikbaar aan een beperkt aantal klanten. Om toegang tot [!DNL Google Ad Manager 360] verbinding, neem contact op met uw Adobe-vertegenwoordiger en geef uw [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | De Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) de bestemming staat u toe om voor authentiek verklaarde eerste-partijsegmenten met goedgekeurde adverteerders en gebruikers voor campagneactivering met DSP te delen. |

{style=&quot;table-layout:auto&quot;}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL Medication]](https://github.com/adobe/xdm/blob/master/components/classes/medication.schema.json) | Een branche in de gezondheidszorg die details vastlegt over een stof die wordt gebruikt voor medische behandeling, met name een geneesmiddel of geneesmiddel. |
| Klasse | [[!UICONTROL Plan]](https://github.com/adobe/xdm/blob/master/components/classes/plan.schema.json) | Een klasse in de gezondheidszorg die details over een medisch plan, zoals een gezondheidsplan of een verzekeringsplan, vastlegt. |
| Klasse | [[!UICONTROL Provider]](https://github.com/adobe/xdm/blob/master/components/classes/provider.schema.json) | Een klasse in de gezondheidszorg die gegevens over een zorgleverancier vastlegt. |
| Klasse | [[!UICONTROL Payer]](https://github.com/adobe/xdm/blob/master/components/classes/payer.schema.json) | Een branche in de gezondheidszorg die gegevens over een verzekeringsmaatschappij opneemt. |
| Klasse | [[!UICONTROL Live Event Schedule]](https://github.com/adobe/xdm/blob/master/components/classes/live-event-schedule.json) | Een klasse in de sport- en entertainmentindustrie die gegevens vastlegt over een live-evenementenschema, zoals een reisconcertschema of de planning van een sportteam. |
| Klasse | [[!UICONTROL Location]](https://github.com/adobe/xdm/blob/master/components/classes/location.json) | Een sport- en entertainmentbranche die de locatie van een live evenement vastlegt, zoals een concertzaal of sportarena. |
| Veldgroep | [[!UICONTROL Healthcare medication]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json) | Een veldgroep voor de [!UICONTROL Medication] klasse waarin details over de medicatie worden vastgelegd, zoals merknaam, partijnummer en hoeveelheid. |
| Veldgroep | [[!UICONTROL Healthcare Plan Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/plan/healthcare-plan-details.schema.json) | Een veldgroep voor de [!UICONTROL Plan] klasse die details zoals netwerk, type, en actieve status vangt. |
| Veldgroep | [[!UICONTROL Healthcare Provider]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Een veldgroep voor de [!UICONTROL Provider] een klasse die gegevens vastlegt van een individuele gezondheidswerker of een organisatie van gezondheidsinstellingen die een vergunning heeft om medische diagnoses en behandelingen te verrichten. |
| Veldgroep | [[!UICONTROL Healthcare Member Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | Een veldgroep voor de [!UICONTROL XDM Individual Profile] klasse die gegevens vastlegt van een persoon die een dienst of zorg heeft of zal ontvangen, zoals contactinformatie, eerstelijnsarts, en planinformatie. |
| Veldgroep | [[!UICONTROL Sitetool Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json) | Een veldgroep voor de [!UICONTROL XDM ExperienceEvent] klas die informatie vastlegt die verzameld is door scholen zoals chatbot, enquête, enzovoort. |
| Veldgroep | [[!UICONTROL Live Event Ticket Purchase]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-live-event-ticket-purchase.json) | Een veldgroep voor de [!UICONTROL XDM ExperienceEvent] een klasse die de aankoopgeschiedenis vastlegt voor tickets voor een live evenement, zoals een concert of een sportspel. |
| Veldgroep | [[!UICONTROL Sports and Entertainment Event Schedule]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/live-event-schedule/sports-entertainment-event-schedule.schema.json) | Een veldgroep voor de [!UICONTROL Live Event Schedule] klasse die verdere details over het programma, zoals de aantrekkingspagina, de openingstijden van de deur, en meer vangen. |
| Veldgroep | [[!UICONTROL Sports Entertainment Event Venue]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/location/sports-entertainment-event-venue.schema.json) | Een veldgroep voor de [!UICONTROL Location] klasse die nadere details over de plaats van de gebeurtenis, zoals zitcapaciteit en aangewezen marktgebieden (DMAs) vangt. |
| Algemeen schema | (Meerdere) | Er zijn nieuwe algemene schema&#39;s beschikbaar voor doelmeetgegevens voor RTCDP-inzichten. Zie het volgende [pull-verzoek](https://github.com/adobe/xdm/pull/1560) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Gedraging | [[!UICONTROL Time-series Schema]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | Een gebeurtenistype voor een mediastatus toegevoegd. |
| Veldgroep | [[!UICONTROL Lodging Reservation]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json) | Er is een uitcheckeigenschap toegevoegd. |
| Gegevenstype | [[!UICONTROL Media information]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Toegevoegde frames-begin en frames-einde velden. |
| Extensie | [[!UICONTROL Workfront Change Event]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Er zijn twee velden toegevoegd die worden gebruikt voor het opslaan van kenmerken om de gebruiker en de tijd van een gebeurtenis create te identificeren. |
| Extensie | [[!UICONTROL Adobe CJM ExperienceEvent - Message interaction details]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/message-interaction.schema.json) | Abonnement, toestemming, aangepaste e-mail en aanvullende gegevensinformatie toegevoegd in het landingspagina-object. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ad-hocschema-labeling | Beheer toegang tot gevoelige gegevens door etiketten op gegevensgebieden van ad hoc regelingen toe te passen die automatisch door de vraag van de Dienst CTAS van de Vraag worden geproduceerd. U kunt het gebruik van bepaalde gebieden, of datasets, van ad hoc regelingen beperken om toegang tot zowel gevoelige persoonlijke gegevens als persoonlijk identificeerbare informatie te controleren. Door op attribuut-gebaseerde toegangsbeheercapaciteit te gebruiken kunt u ad hoc schemagebieden door de UI van het Platform etiketteren. |
| `FLATTEN` instellen | Wanneer het verbinden met een gegevensbestand door derdehulpmiddelen van BI, `FLATTEN` bij het instellen worden geneste gegevensstructuren afgevlakt in afzonderlijke kolommen, waarbij de kenmerknaam de kolomnaam wordt die de rijwaarden bevat. Dit verbetert de bruikbaarheid van ad-hocschema&#39;s en vermindert de vereiste werkbelasting om gegevens op te halen, te analyseren, om te zetten en te melden in BI hulpmiddelen die geen genestelde gegevensstructuren steunen. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de Diensten van de Vraag, verwijs naar [Overzicht van Query Service](../../query-service/home.md).

## Real-time Customer Data Platform-verbindingen {#data-collection}

Real-time Customer Data Platform Connections biedt een reeks technologieën waarmee u gegevens van de client-side-klantervaring kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| [De configuratie van het Type van toegang voor gegevensstromen](../../edge/datastreams/overview.md#create) | Wanneer u een nieuwe gegevensstroom maakt, kunt u nu selecteren welk type aanvragen door het Edge-netwerk worden geaccepteerd: <ul><li>**[!UICONTROL Mixed Authentication]**: Wanneer deze optie wordt geselecteerd, keurt het Netwerk van de Rand zowel voor authentiek verklaarde als unauthenticated verzoeken goed. Selecteer deze optie als u de SDK van het Web wilt gebruiken of [Mobile SDK](https://aep-sdks.gitbook.io/docs/), samen met de [Server-API](../../server-api/overview.md). </li><li>**[!UICONTROL Authenticated Only]**: Wanneer deze optie wordt geselecteerd, keurt het Netwerk van de Rand slechts voor authentiek verklaarde verzoeken goed. Selecteer deze optie als u alleen de Server-API wilt gebruiken en niet-geverifieerde aanvragen door de [!DNL Edge Network]. </li></ul> |
| [Profielen renderen](../../edge/personalization/rendering-personalization-content.md#applypropositions) in toepassingen van één pagina zonder stijgende metriek. | De zojuist toegevoegde `applyPropositions` met de opdracht kunt u een array met voorstellingen renderen of uitvoeren vanuit [!DNL Target] in toepassingen van één pagina, zonder het verhogen van [!DNL Analytics] en [!DNL Target] metriek. Hierdoor wordt de rapportnauwkeurigheid vergroot. |
| [Id&#39;s delen via mobiel naar web en verschillende domeinen](../../edge/identity/id-sharing.md) | De SDK van het Web van Adobe Experience Platform ondersteunt nu mogelijkheden voor het delen van bezoekers-id&#39;s die u in staat stellen gepersonaliseerde ervaringen nauwkeuriger te leveren, tussen mobiele apps en mobiele webinhoud, en over domeinen. |

Zie voor meer informatie de [Overzicht van Real-Time CDP-verbindingen](../../rtcdp-connections/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| --- | --- |
| Bètaversie van [!DNL Mixpanel] bron | U kunt nu de opdracht [!DNL Mixpanel] bron voor het opnemen van analysegegevens uit uw [!DNL Mixpanel] aan Experience Platform. Zie de [[!DNL Mixpanel] brondocumentatie](../../sources/connectors/analytics/mixpanel.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
