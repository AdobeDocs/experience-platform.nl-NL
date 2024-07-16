---
title: Opmerkingen bij de release van Adobe Experience Platform, maart 2024
description: Aanvullende informatie van maart 2024 voor Adobe Experience Platform.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 19 maart 2024**

>[!TIP]
>
>Gebruik de [ verklarende woordenlijst van Adobe Experience Platform ](/help/landing/glossary.md) vertrouwd te worden met terminologie die in Real-time Customer Data Platform en Adobe Experience Platform wordt gebruikt. Als u een bepaalde term die u zoekt niet kunt vinden, gebruikt u de feedbackopties op de pagina om te vragen dat nieuwe termen aan de verklarende woordenlijst worden toegevoegd.

Updates voor bestaande functies in Experience Platform:

- [Catalogusservice](#catalog-service)
- [Gegevensverzameling](#data-collection)
- [Gegevensvoorbereiding](#data-prep)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie van gegevens en de gegevensverbinding in Adobe Experience Platform. Terwijl alle gegevens die in Experience Platform worden opgenomen in het gegevensmeer als dossiers en folders worden opgeslagen, houdt de Catalogus de meta-gegevens en de beschrijving van die dossiers en folders voor raadpleging en controledoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Meer handelingen | Om verrichtingen flexibeler te maken en u te helpen uw gegevens beheren, kunt u de &quot;Meer acties&quot;eigenschap van de detailsmening nu gebruiken om extra taken op een dataset uit te voeren. U kunt of de dataset schrappen of het voor gebruik met het Profiel van de Klant in real time van de detailspagina van een gekozen dataset toelaten.<br>**Nota:** als u een dataset voor de opname van het Profiel toelaat, moet het schema van de dataset met het Profiel van de Klant in real time compatibel zijn.<br>![ de werkruimte Datasets met het [!UICONTROL ... More] dropdown benadrukte menu.](../2024/assets/march/more-actions.png " de werkruimte van Datasets met het Meer dropdown benadrukte menu."){width="100" zoomable="yes"}.<br> leest de [ gids van de datasetgebruiker ](../../catalog/datasets/user-guide.md) documentatie voor optelinformatie. |

{style="table-layout:auto"}

Voor meer informatie over de Dienst van de Catalogus, verwijs naar het [ overzicht van de Dienst van de Catalogus ](../../catalog/home.md).

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe mapfuncties voor Adobe Analytics | U kunt nu de volgende functies gebruiken om gebeurtenisgegevens uit Adobe Analytics te extraheren: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Voor meer informatie over deze functies, lees de [ Prep functies van Gegevens gids ](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

Voor meer informatie over de Prep van Gegevens, lees het [ Overzicht van de Prep van Gegevens ](../../data-prep/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe eigenschappen**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensies | [!DNL Merkury] Tagextensie | De [[!DNL Merkury]  markeringsuitbreiding ](https://exchange.adobe.com/apps/ec/600027/merkury-tag) verstrekt industrie belangrijke gelijke tarieven voor anonieme websitebezoekers aan a [!DNL Merkury] identiteitskaart. Merken kunnen de kracht van de tag [!DNL Merkury] en de Adobe benutten om persoonlijke webbeleving in real-time te bieden. Bovendien zorgt de tag [!DNL Merkury] voor de groei van digitale gegevens van eerste bedrijven en van gekoppelde online en offline klantprofielen. |

{style="table-layout:auto"}

Om meer over gegevensinzameling te leren, te lezen gelieve het [ overzicht van de gegevensinzameling ](../../tags/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe en bijgewerkte bestemmingen** {#new-updated-destinations}

| Doel | Type | Beschrijving |
| ----------- | --------- | ----------- |
| [ (Beta) Verbinding Acxiom Data Enhancement ](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Nieuw | Gebruik deze connector om first-party profielen van Real-Time CDP naar Acxiom te activeren voor gegevensverrijking en gebruik via marketingkanalen. Vervolgens kunt u de Acxiom-bron gebruiken om de profielen met verbeterde gegevens te importeren en ermee te werken in Real-Time CDP. |
| [ (Beta) Verbinding voor Acxiom-perspectiefonderdrukking ](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Nieuw | Exporteer uw eersteklas publiek naar de Acxiom-bestemming, zodat Acxiom bekende of omgezette klanten kan onderdrukken. Dan, gebruik de [ Acxiom het prospecteren van gegevensinvoer ](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) bronschakelaar om perspectieflijsten van Acxiom in te voeren en te activeren, met uw bekende of omgezette verwijderde klanten. |
| [ verbinding van de Advertentie van Amazon ](../../destinations/catalog/advertising/amazon-ads.md) | Bijwerken | Bij het exporteren van gegevens naar de bestemming Amazon Ads kunt u de gegevens nu doorsturen naar de Amazon-DSP of de Amazon-Marketing Cloud (nieuw). |
| [ LiveRamp onboarding verbinding ](../../destinations/catalog/advertising/liveramp-onboarding.md) | Bijwerken | Het doel LiveRamp on boarding heeft nu ondersteuning voor leveringen aan instanties van Europa en Australië [!DNL LiveRamp] [!DNL SFTP] . De maximale geëxporteerde bestandsgrootte is ook verhoogd tot 10 miljoen rijen (van 5 miljoen, eerder). |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor datatype Experience Platform UI-map | Pas verder uw gegevensstructuur van het Model van de Gegevens van de Ervaring (XDM) aan door kaartgebieden in Platform UI te bepalen. U kunt nu kaartvelden maken in de Schema-editor om flexibele gegevensstructuren te modelleren of sleutelwaardeparen efficiënt op te slaan. Selecteer &quot;Kaart&quot;van het drop-down Type wanneer het bepalen van een nieuw gebied om subfields te vormen en hen toe te wijzen aan gebiedsgroepen. Ondersteunde typen toewijzingswaarden zijn tekenreeks en geheel getal.<br>![ de Redacteur van Schema met de benadrukte gebieden van het type en van het de waardetype van de Kaart.](../2024/assets/march/maps.png " de Redacteur van Schema met de benadrukte gebieden van het type en van het de waardetype van de Kaart."){width="100" zoomable="yes"}<br> leren hoe te [ kaartgebieden in UI ](../../xdm/ui/fields/map.md) bepalen, de gids UI zien. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Segmenteringsservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) segmenteren naar het publiek. U kunt een publiek maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze soorten publiek worden centraal geconfigureerd en onderhouden op [!DNL Platform] en zijn gemakkelijk toegankelijk voor elke Adobe.

**Nieuwe eigenschap**

| Functie | Beschrijving |
| ------- | ----------- |
| Bulkacties | De publieksinventarisatie ondersteunt nu acties in grote hoeveelheden. Met bulkacties kunt u snel meerdere soorten publiek selecteren om deze naar een map te verplaatsen, tags toe te passen, toegangslabels toe te passen of te verwijderen. <br> ![ Bulk acties in de werkruimte van het publiek UI.](../2024/assets/march/bulk-actions.png " Bulk acties in de werkruimte van het publiek UI."){width="100" zoomable="yes"} <br> voor meer informatie over deze eigenschap, lees het [ Poortoverzicht van het Poortpubliek van het Poortpubliek ](../../segmentation/ui/audience-portal.md#bulk-actions). |

{style="table-layout:auto"}

Meer over de Dienst van de Segmentatie leren, lees het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe en bijgewerkte bronnen**

| Functie | Type | Beschrijving |
| --- | --- | --- |
| [!BADGE  Beta ] {type=Informative} [!DNL Acxiom Data Ingestion] | Nieuw | Gebruik de [[!DNL Acxiom Data Ingestion]  bron ](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) om [!DNL Acxiom] gegevens in Real-time Customer Data Platform in te voeren en eerste-partijprofielen te verrijken. Vervolgens kunt u met uw [!DNL Acxiom] verrijkte first-party-profielen het publiek verbeteren en activeren via verschillende marketingkanalen. <br> ![ de Ingestiebron van Gegevens van Acxiom.](../2024/assets/march/acxiom-data-ingestion.png " Nieuwe Ingestiebron van Gegevens van Acxiom."){width="100" zoomable="yes"} <br> leest het [[!DNL Acxiom Data Ingestion]  overzicht ](../../sources/connectors/data-partners/acxiom-data-ingestion.md) voor informatie over hoe te begonnen worden. |
| [!BADGE  Beta ] {type=Informative} [!DNL Stripe] | Nieuw | Gebruik de [[!DNL Stripe]  bron ](../../sources/connectors/payments/stripe.md) om gegevens in te voeren die tijdens de koopstroom door uw klanten in Experience Platform worden gevangen. Als u deze gegevens eenmaal hebt ingevoerd, kunt u deze gebruiken om persoonlijke aanbiedingen te maken en rijkere zakelijke inzichten te ontgrendelen. <br> ![ de bron van het Stripe.](../2024/assets/march/stripe.png " Nieuwe bron van het Stripe."){width="100" zoomable="yes"} <br> leest het [[!DNL Stripe]  overzicht ](../../sources/connectors/payments/stripe.md) voor informatie over hoe te begonnen worden. |
| UI-ondersteuning voor [!DNL Snowflake Streaming] | Nieuw | U kunt [[!DNL Snowflake Streaming]  bron ](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) in het Experience Platform nu gebruiken UI, om gegevens van uw [!DNL Snowflake] gegevensbestand te stromen. <br> ![ de Snowflake die bron stroomt.](../2024/assets/march/snowflake-streaming.png " Nieuwe Snowflake die bron stroomt."){width="100" zoomable="yes"} <br> leest het [[!DNL Snowflake Streaming]  overzicht ](../../sources/connectors/databases/snowflake-streaming.md) voor informatie over hoe te begonnen worden. |

{style="table-layout:auto"}

Voor meer informatie over bronnen, lees het [ overzicht van bronnen ](../../sources/home.md).
