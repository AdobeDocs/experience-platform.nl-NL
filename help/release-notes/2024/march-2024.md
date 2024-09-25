---
title: Aanvullende informatie van maart 2024 voor Adobe Experience Platform
description: Aanvullende informatie van maart 2024 voor Adobe Experience Platform.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: ht
source-wordcount: '1189'
ht-degree: 100%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum:19 maart 2024**

>[!TIP]
>
>Gebruik de [verklarende woordenlijst van Adobe Experience Platform](/help/landing/glossary.md) om vertrouwd te raken met terminologie die in Real-time Customer Data Platform en Adobe Experience Platform wordt gebruikt. Als u een specifieke term niet kunt vinden, kunt u via de feedbackopties op de pagina een verzoek indienen om nieuwe termen aan de woordenlijst toe te voegen.

Updates van bestaande functies in Experience Platform:

- [Catalogusservice](#catalog-service)
- [Dataverzameling](#data-collection)
- [Gegevensvoorbereiding](#data-prep)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Catalogusservice {#catalog-service}

Catalogusservice is het systeem voor het vastleggen van de locatie en herkomst van gegevens binnen Adobe Experience Platform. Alle gegevens die in Experience Platform worden opgenomen, worden in een datalake opgeslagen als bestanden en mappen. De catalogus bevat daarentegen de metagegevens en beschrijvingen van die bestanden en mappen voor opzoek- en controledoeleinden.

| Functie | Beschrijving |
| --- | --- |
| Meer acties | Om bewerkingen flexibeler te maken en u te helpen uw gegevens te beheren, kunt u nu de functie Meer acties vanuit de detailweergave gebruiken om extra taken op een dataset uit te voeren. U kunt de dataset verwijderen of inschakelen voor gebruik met realtime-klantenprofiel via de pagina Meer informatie van een gekozen dataset.<br>**Opmerking:** als u een dataset inschakelt voor profielopname, moet het schema van de dataset compatibel zijn met realtime-klantenprofiel.<br>![De werkruimte Datasets met het vervolgkeuzemenu [!UICONTROL ... More] gemarkeerd.](../2024/assets/march/more-actions.png "De werkruimte Datasets met het vervolgkeuzemenu Meer gemarkeerd."){width="100" zoomable="yes"}.<br>Raadpleeg het [handboek voor datasets](../../catalog/datasets/user-guide.md) voor aanvullende informatie. |

{style="table-layout:auto"}

Voor meer informatie over de catalogusservice, raadpleegt u het [Overzicht van de Catalogusservice](../../catalog/home.md).

## Gegevensvoorbereiding {#data-prep}

Met gegevensvoorbereiding kunnen gegevenstechnici gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience-datamodel).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe toewijzingsfuncties voor Adobe Analytics | U kunt nu de volgende functies gebruiken om gebeurtenisgegevens uit Adobe Analytics te extraheren: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Voor meer informatie over deze functies, raadpleegt u de [Handleiding voor Gegevensvoorbereidingsfuncties](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

Voor meer informatie over gegevensvoorbereiding, raadpleegt u het [Overzicht van Gegevensvoorbereiding](../../data-prep/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensies | [!DNL Merkury]Tagextensie | De [[!DNL Merkury] tagextensie](https://exchange.adobe.com/apps/ec/600027/merkury-tag) verstrekt toonaangevende gelijke tarieven voor anonieme websitebezoekers met een [!DNL Merkury]-ID. Merken kunnen de kracht van de [!DNL Merkury]-tag en Adobe benutten om in realtime gepersonaliseerde website-ervaringen te bieden. Bovendien maakt de [!DNL Merkury]-tag de groei van digitale first-party-gegevens mogelijk, samen met verbonden online- en offline-klantprofielen. |

{style="table-layout:auto"}

Voor meer informatie over dataverzameling, raadpleegt u het [overzicht van de dataverzameling](../../tags/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms die een naadloze activering van gegevens uit Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe en bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Type | Beschrijving |
| ----------- | --------- | ----------- |
| [(Beta) Acxiom Data Enhancement-verbinding](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Nieuw | Met deze connector kunt u first-partyprofielen van Real-Time CDP activeren naar Acxiom voor gegevensverrijking en gebruik in alle marketingkanalen. Vervolgens kunt u de Acxiom-bron gebruiken om de profielen met uitgebreide gegevens te importeren en ermee te werken in Real-Time CDP. |
| [(Beta) Acxiom Prospect Suppression-verbinding](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Nieuw | Exporteer uw first-party doelgroepen naar de Acxiom-bestemming, zodat Acxiom bekende of geconverteerde klanten kan onderdrukken. Gebruik vervolgens de [Acxiom-bronconnector voor het importeren van prospectiegegevens](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) om prospectlijsten van Acxiom op te nemen en te activeren. Uw bekende of geconverteerde klanten worden hierbij verwijderd. |
| [Amazon Ads-verbinding](../../destinations/catalog/advertising/amazon-ads.md) | Bijwerken | Wanneer u gegevens naar de Amazon Ads-bestemming exporteert, kunt u de gegevens nu naar de Amazon DSP of de Amazon Marketing Cloud (nieuw) doorsturen. |
| [LiveRamp Onboarding-verbinding](../../destinations/catalog/advertising/liveramp-onboarding.md) | Bijwerken | De LiveRamp Onboarding-bestemming biedt nu ondersteuning voor leveringen aan [!DNL LiveRamp] [!DNL SFTP]-instanties in Europa en Australië. De maximale grootte van het geëxporteerde bestand is ook verhoogd naar 10 miljoen rijen (voorheen was dit 5 miljoen). |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het gegevenstype voor toewijzing in de Experience Platform-gebruikersinterface | U kunt de gegevensstructuur van uw Experience-datamodel (XDM) verder aanpassen door ktoewijzingsvelden te definiëren in de Platform-gebruikersinterface. U kunt nu toewijzingsvelden maken in de Schema-editor om flexibele gegevensstructuren te modelleren of sleutelwaardeparen efficiënt op te slaan. Selecteer Toewijzen in de vervolgkeuzelijst Type wanneer u een nieuw veld definieert om subvelden te configureren en deze toe te wijzen aan veldgroepen. De ondersteunde typen toewijzingswaarden zijn tekenreeks en geheel getal.<br>![De schema-editor met de velden Type en Type toewijzingswaarde gemarkeerd.](../2024/assets/march/maps.png "De schema-editor met de velden Type en Type toewijzingswaarde gemarkeerd."){width="100" zoomable="yes"}<br>Raadpleeg de handleiding voor de gebruikersinterface voor meer informatie over het [definiëren van toewijzingsvelden in de gebruikersinterface](../../xdm/ui/fields/map.md). |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, raadpleegt u het [XDM-systeemoverzicht](../../xdm/home.md).

## Segmentatieservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, prospects, gebruikers of organisaties) in doelgroepen segmenteren. U kunt een doelgroep maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile]-gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform] en zijn eenvoudig toegankelijk via elke Adobe-oplossing.

**Nieuwe functie**

| Functie | Beschrijving |
| ------- | ----------- |
| Bulkacties | De doelgroep-inventory ondersteunt nu bulkacties. Met bulkacties kunt u snel meerdere doelgroepen selecteren om ze naar een map te verplaatsen, tags toe te passen, toegangslabels toe te passen of te verwijderen. <br> ![Bulkacties in de werkruimte van de Audience-gebruikersinterface.](../2024/assets/march/bulk-actions.png "Bulkacties in de werkruimte van de Audience-gebruikersinterface."){width="100" zoomable="yes"} <br> Voor meer informatie over deze functie, leest u het [Audience Portal-overzicht](../../segmentation/ui/audience-portal.md#bulk-actions). |

{style="table-layout:auto"}

Voor meer informatie over de Segmentatieservice, raadpleegt u het [Overzicht van de Segmentatieservice](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe en bijgewerkte bronnen**

| Functie | Type | Beschrijving |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | Nieuw | Gebruik de [[!DNL Acxiom Data Ingestion] bron](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) om [!DNL Acxiom]-gegevens aan het Real-Time Customer Data Platform toe te voegen en first-party profielen te verrijken. Vervolgens kunt u uw met [!DNL Acxiom] verrijkte first-party profielen gebruiken om uw doelgroepen te verbeteren en deze te activeren via marketingkanalen. <br> ![De gegevensopnamebron van Acxiom.](../2024/assets/march/acxiom-data-ingestion.png "Nieuwe gegevensopnamebron van Acxiom."){width="100" zoomable="yes"} <br> Raadpleeg het [[!DNL Acxiom Data Ingestion] overzicht](../../sources/connectors/data-partners/acxiom-data-ingestion.md) voor informatie over hoe u aan de slag kunt gaan. |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | Nieuw | Gebruik de [[!DNL Stripe] bron](../../sources/connectors/payments/stripe.md) om gegevens die uw klanten tijdens het aankoopproces hebben vastgelegd, op te nemen in het Experience Platform. Zodra u deze gegevens hebt verwerkt, kunt u ze gebruiken om gepersonaliseerde aanbiedingen te maken en meer inzicht in uw bedrijf te krijgen. <br> ![De Stripe-bron.](../2024/assets/march/stripe.png "De nieuwe Stripe-bron."){width="100" zoomable="yes"} <br> Raadpleeg het [[!DNL Stripe] overzicht](../../sources/connectors/payments/stripe.md) voor informatie over hoe u aan de slag kunt gaan. |
| Ondersteuning voor gebruikersinterface voor [!DNL Snowflake Streaming] | Nieuw | U kunt nu de [[!DNL Snowflake Streaming] bron](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) in de gebruikersinterface van het Experience Platform gebruiken om gegevens te streamen vanuit uw [!DNL Snowflake]-database. <br> ![De bron van Snowflake Streaming.](../2024/assets/march/snowflake-streaming.png "Nieuwe bron van Snowflake Streaking."){width="100" zoomable="yes"} <br> Raadpleeg het [[!DNL Snowflake Streaming] overzicht](../../sources/connectors/databases/snowflake-streaming.md) voor informatie over hoe u aan de slag kunt gaan. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie over bronnen, het [overzicht van bronnen](../../sources/home.md).
