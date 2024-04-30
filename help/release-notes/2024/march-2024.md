---
title: Opmerkingen bij de release van Adobe Experience Platform, maart 2024
description: Aanvullende informatie van maart 2024 voor Adobe Experience Platform.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: 708bb791ad85b6ee8f3671ffc574e4f27fdddd0a
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 19 maart 2024**

>[!TIP]
>
>Gebruik de [Adobe Experience Platform glossary](/help/landing/glossary.md) om vertrouwd te raken met de terminologie die in Real-time Customer Data Platform en Adobe Experience Platform wordt gebruikt. Als u een bepaalde term die u zoekt niet kunt vinden, gebruikt u de feedbackopties op de pagina om te vragen dat nieuwe termen aan de verklarende woordenlijst worden toegevoegd.

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
| Meer handelingen | Om verrichtingen flexibeler te maken en u te helpen uw gegevens beheren, kunt u de &quot;Meer acties&quot;eigenschap van de detailsmening nu gebruiken om extra taken op een dataset uit te voeren. U kunt of de dataset schrappen of het voor gebruik met het Profiel van de Klant in real time van de detailspagina van een gekozen dataset toelaten.<br>**Opmerking:** als u een dataset voor de opname van het Profiel toelaat, moet het schema van de dataset met het Profiel van de Klant in real time compatibel zijn.<br>![De werkruimte Datasets met de [!UICONTROL ... More] vervolgkeuzemenu gemarkeerd.](../2024/assets/march/more-actions.png "De werkruimte Datasets met het vervolgkeuzemenu Meer gemarkeerd."){width="100" zoomable="yes"}.<br>Lees de [gebruikershandleiding voor gegevenssets](../../catalog/datasets/user-guide.md) documentatie voor aanvullende informatie. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie over Catalog Service de [Overzicht van Catalog Service](../../catalog/home.md).

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe mapfuncties voor Adobe Analytics | U kunt nu de volgende functies gebruiken om gebeurtenisgegevens uit Adobe Analytics te extraheren: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Lees voor meer informatie over deze functies de [Handleiding voor functies Data Prep](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

Voor meer informatie over de Prep van Gegevens, lees [Overzicht van Data Prep](../../data-prep/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden, waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

**Nieuwe functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensies | [!DNL Merkury] Tagextensie | De [[!DNL Merkury] tagextensie](https://exchange.adobe.com/apps/ec/600027/merkury-tag) biedt toonaangevende prijzen voor anonieme websitebezoekers aan een [!DNL Merkury] ID. Merken kunnen de kracht van de [!DNL Merkury] tag en Adobe om persoonlijke website-ervaringen in real-time te bieden. Daarnaast worden de [!DNL Merkury] -tag maakt de groei van digitale gegevens van eerste bedrijven mogelijk, samen met gekoppelde online en offline klantprofielen. |

{style="table-layout:auto"}

Voor meer informatie over gegevensverzameling leest u de [overzicht van gegevensverzameling](../../tags/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe en bijgewerkte bestemmingen** {#new-updated-destinations}

| Doel | Type | Beschrijving |
| ----------- | --------- | ----------- |
| [(bèta) Verbinding Acxiom-gegevens verbeteren](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Nieuw | Gebruik deze connector om first-party profielen van Real-Time CDP naar Acxiom te activeren voor gegevensverrijking en gebruik via marketingkanalen. Vervolgens kunt u de Acxiom-bron gebruiken om de profielen met verbeterde gegevens te importeren en ermee te werken in Real-Time CDP. |
| [(bèta) Acxiom-perspectiefonderdrukkingsverbinding](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Nieuw | Exporteer uw eersteklas publiek naar de Acxiom-bestemming, zodat Acxiom bekende of omgezette klanten kan onderdrukken. Gebruik vervolgens de [Acxiom gegevens te exporteren](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) bronaansluiting voor het opnemen en activeren van perspectieflijsten van Acxiom, waarbij uw bekende of omgezette klanten zijn verwijderd. |
| [Amazon Ads-verbinding](../../destinations/catalog/advertising/amazon-ads.md) | Bijwerken | Bij het exporteren van gegevens naar de bestemming Amazon Ads kunt u de gegevens nu doorsturen naar de Amazon-DSP of de Amazon-Marketing Cloud (nieuw). |
| [Verbinding LiveRamp aan boord](../../destinations/catalog/advertising/liveramp-onboarding.md) | Bijwerken | De bestemming LiveRamp aan boord heeft nu ondersteuning voor leveringen aan Europa en Australië [!DNL LiveRamp] [!DNL SFTP] instanties. De maximale geëxporteerde bestandsgrootte is ook verhoogd tot 10 miljoen rijen (van 5 miljoen, eerder). |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor datatype Experience Platform UI-map | Pas verder uw gegevensstructuur van het Model van de Gegevens van de Ervaring (XDM) aan door kaartgebieden in Platform UI te bepalen. U kunt nu kaartvelden maken in de Schema-editor om flexibele gegevensstructuren te modelleren of sleutelwaardeparen efficiënt op te slaan. Selecteer &quot;Kaart&quot;van het drop-down Type wanneer het bepalen van een nieuw gebied om subfields te vormen en hen toe te wijzen aan gebiedsgroepen. Ondersteunde typen toewijzingswaarden zijn tekenreeks en geheel getal.<br>![De Schema-editor met de velden Type- en Kaartwaardetype gemarkeerd.](../2024/assets/march/maps.png "De Schema-editor met de velden Type- en Kaartwaardetype gemarkeerd."){width="100" zoomable="yes"}<br> Leren hoe te [kaartvelden definiëren in de gebruikersinterface](../../xdm/ui/fields/map.md), zie de UI-gids. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Nieuwe functie**

| Functie | Beschrijving |
| ------- | ----------- |
| Bulkacties | De publieksinventarisatie ondersteunt nu acties in grote hoeveelheden. Met bulkacties kunt u snel meerdere soorten publiek selecteren om deze naar een map te verplaatsen, tags toe te passen, toegangslabels toe te passen of te verwijderen. <br> ![Bulkhandelingen in de gebruikersinterface van soorten publiek.](../2024/assets/march/bulk-actions.png "Bulkhandelingen in de gebruikersinterface van soorten publiek."){width="100" zoomable="yes"} <br>Voor meer informatie over deze functie leest u de [Handleiding voor segmentatieservice](../../segmentation/ui/overview.md#bulk-actions). |

{style="table-layout:auto"}

Meer over de Dienst van de Segmentatie leren, lees [Overzicht van segmentatieservice](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe en bijgewerkte bronnen**

| Functie | Type | Beschrijving |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | Nieuw | Gebruik de [[!DNL Acxiom Data Ingestion] bron](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) tot toevoegen [!DNL Acxiom] gegevens naar Real-time Customer Data Platform en verrijken profielen van eerste partijen. Vervolgens kunt u uw [!DNL Acxiom]- verrijkte first-party profielen om publiek te verbeteren en over marketing kanalen te activeren. <br> ![De bron van acxiom-gegevensinname.](../2024/assets/march/acxiom-data-ingestion.png "Nieuwe Acxiom-gegevensbron."){width="100" zoomable="yes"} <br> Lees de [[!DNL Acxiom Data Ingestion] overzicht](../../sources/connectors/data-partners/acxiom-data-ingestion.md) voor informatie over hoe te beginnen. |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | Nieuw | Gebruik de [[!DNL Stripe] bron](../../sources/connectors/payments/stripe.md) om gegevens die tijdens de aanschafstroom door uw klanten zijn vastgelegd, in Experience Platform in te voeren. Als u deze gegevens eenmaal hebt ingevoerd, kunt u deze gebruiken om persoonlijke aanbiedingen te maken en rijkere zakelijke inzichten te ontgrendelen. <br> ![De fragmentbron.](../2024/assets/march/stripe.png "Nieuwe bron van Stripe."){width="100" zoomable="yes"} <br> Lees de [[!DNL Stripe] overzicht](../../sources/connectors/payments/stripe.md) voor informatie over hoe te beginnen. |
| UI-ondersteuning voor [!DNL Snowflake Streaming] | Nieuw | U kunt nu de opdracht [[!DNL Snowflake Streaming] bron](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) in de interface van het Experience Platform om gegevens van uw [!DNL Snowflake] database. <br> ![De Snowflake Streaming-bron.](../2024/assets/march/snowflake-streaming.png "Nieuwe bron voor streaming Snowflake."){width="100" zoomable="yes"} <br> Lees de [[!DNL Snowflake Streaming] overzicht](../../sources/connectors/databases/snowflake-streaming.md) voor informatie over hoe te beginnen. |

{style="table-layout:auto"}

Lees voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
