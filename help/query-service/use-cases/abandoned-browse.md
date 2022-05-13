---
keywords: Experience Platform;query-service;Query-service;query
title: Voorbeeld van gebruik van hoofdletters/kleine letters voor Adobe Experience Platform Query Service
topic-legacy: tutorial
description: Een end-to-end voorbeeld om de veelzijdigheid en de voordelen van de Dienst van de Vraag van Adobe Experience Platform aan te tonen.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 06655e930e447b48089891ca930da89854b8320b
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Voorbeeld van gebruik van hoofdletters/kleine letters voor Adobe Experience Platform [!DNL Query Service]

Dit document en de bijbehorende videopresentatie bieden een end-to-end workflow op hoog niveau waarop wordt getoond hoe Adobe Experience Platform [!DNL Query Service] profiteert van de strategische zakelijke inzichten van uw organisatie. Gebruikend een doorbladerend gebruiksgeval als voorbeeld, illustreert deze gids de volgende belangrijkste concepten:

* Het belangrijkste belang van gegevensverwerking voor het maximaliseren van het potentieel van Adobe Experience Platform
* Manieren om de vraag te bouwen die op uw bestaande gegevensarchitectuur wordt gebaseerd.
* Zorg voor gegevenskwaliteit die aan uw behoeften voldoet, en methoden om eventuele tekortkomingen te beperken.
* Het proces om een vraag te plannen om bij een vastgestelde frequentie voor gebruik stroomafwaarts in segmentatie en bestemmingen voor verpersoonlijking te lopen.
* Het gemak voor marketers om afgeleide kenmerken in hun segmenten op te nemen door de kracht van [!DNL Query Service].

## Doelstellingen {#objectives}

Deze workflowdemonstratie is gebaseerd op verschillende Adobe Experience Platform-services. Als u de stappen wilt volgen, is het raadzaam de volgende functies en services goed te begrijpen:

* De [basisbeginselen van XDM-schemacompositie (Experience Data Model)](../../xdm/schema/composition.md)
* Procedure [gegevenssets maken en gegevens opnemen](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* Procedure [Gegevens opnemen via de Adobe Analytics-bronaansluiting](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)
* [Segmentatie](../../segmentation/home.md)
* [Doelen](../../destinations/home.md)

In het voorbeeld voor het verlaten van een browser wordt het gebruik van Adobe centraal gesteld [!DNL Analytics] gegevens om een bepaald actief publiek te creëren. Het publiek is verfijnd en omvat alle klanten die de afgelopen vier dagen door de website hebben gebladerd, maar geen aankoop hebben gedaan. Elk profiel in het publiek wordt dan gericht met het hoogst-prijs SKU dat uit het gedragspatroon van de klant resulteerde.

De vraag zelf is zeer recept en omvat slechts gegevens die aan de criteria van het gebruiksgeval voor de segmentdefinitie voldoen. Hierdoor worden de prestaties verbeterd doordat de hoeveelheid [!DNL Analytics] gegevens die worden verwerkt. De gegevens worden ook op prijs gesorteerd van het hoogst naar het laagst en de hoogst geprijsde SKU gekozen die de gebruiker aan het doorbladeren was.

De query die in de presentatie wordt gebruikt, is hieronder te zien:

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] Voorbeeld van verlaten bestanden door bladeren met adobe Analytics {#video-example}

De onderstaande videopresentatie biedt een holistische, realistische gebruiksmogelijkheid voor uw Experience Platform-gegevens die zijn toegespitst op [!DNL Query Service] en Adobe analytics integrations.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Voordelen van [!DNL Query Service] {#benefits}

De functies van [!DNL Query Service] voor veel doeleinden. U kunt het gebruiken om complexe logica voor segmentatie aan te passen, voor het berekenen van diverse gepersonaliseerde attributen voor gebruik stroomafwaarts, of om zeer te vereenvoudigen hoe u uw segmenten bouwt.

[!DNL Query Service] laat u toe om beperkingen in uw vragen te omvatten om uw segment het bouwen proces te vereenvoudigen. Dit verbetert de gegevenskwaliteit door ervoor te zorgen de juiste gegevens voor uw segmenten kwalificeren en leidt tot nauwkeuriger publiek. Het handhaven van de kwaliteit van uw vraag resulteert in een nauwkeurig publiek en helpt met gegevensbetrouwbaarheid. U kunt uw publiek ook opslaan door schema&#39;s en douanetabellen te creëren die op attributen worden gebaseerd die uit uw vraag worden afgeleid. Een douanetabel kan voor Profiel worden toegelaten en u kunt deze gegevenspunten voor segmentatie en verpersoonlijking gebruiken. Deze functie helpt marketers die een duidelijk publiek van mensen willen creëren.

Ook, door logica in uw vraag te omvatten die om het even welke terugkomende of statische voorwaarden tevredenstelt, [!DNL Query Service] extraheert de last van uitgebreide segmentatie.

Adobe Experience Platform biedt een gegevensopslagplaats en de benodigde hulpmiddelen om uw gegevens op een efficiënte en betrouwbare manier te activeren. Door gegevens binnen Platform te houden, staat het u toe om attributen af te leiden terwijl het runnen van andere processen en verwijdert de behoefte om gegevens naar derdehulpmiddelen voor manipulatie en verwerking uit te voeren. Dergelijke verwerkingsoverheadkosten kunnen een projectchronologie zeer beïnvloeden wanneer het behandelen van honderden attributen of campagnes. Dit geeft marketers één enkele plaats om tot hun gegevens toegang te hebben en campagnes te bouwen evenals een zeer dynamische manier om hun berichten te segmenteren en te personaliseren.

## Volgende stappen

Door dit document te lezen, moet u nu begrijpen hoe [!DNL Query Service] beïnvloedt niet alleen de kwaliteit van uw gegevens en het gemak van segmentatie maar ook zijn belang binnen uw gegevensarchitectuur voor het volledige werkschema van begin tot eind. Voor meer toepasbare SQL-voorbeelden die Adobe Analytics gebruiken met [!DNL Query Service], zie de [Documentatie met voorbeeldvragen voor Adobe Analytics](../sample-queries/adobe-analytics.md).

Andere documenten die de voordelen van [!DNL Query Service] voor de strategische bedrijfsinzichten van uw organisatie: [beide filters gebruiken](./bot-filtering.md) voorbeeld.

U kunt deze documenten ook gebruiken als u het [!DNL Query Service] functies:

* [Richtlijnen voor het uitvoeren van query&#39;s](../best-practices/writing-queries.md)
* [Richtlijnen voor de organisatie van gegevenselementen](../best-practices/organize-data-assets.md).


