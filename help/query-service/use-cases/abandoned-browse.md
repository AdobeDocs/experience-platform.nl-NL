---
keywords: Experience Platform;query-service;Query-service;query
title: Voorbeeld van gebruik van hoofdletters/kleine letters voor Adobe Experience Platform Query Service
description: Een end-to-end voorbeeld om de veelzijdigheid en de voordelen van de Dienst van de Vraag van Adobe Experience Platform aan te tonen.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Voorbeeld van gebruik van hoofdletters/kleine letters voor Adobe Experience Platform [!DNL Query Service]

Dit document en de bijbehorende videopresentatie bieden een end-to-end workflow op hoog niveau waarin wordt aangetoond hoe Adobe Experience Platform [!DNL Query Service] de strategische zakelijke inzichten van uw organisatie ten goede komt. Gebruikend een doorbladerend gebruiksgeval als voorbeeld, illustreert deze gids de volgende belangrijkste concepten:

* Het belangrijkste belang van gegevensverwerking om het potentieel van Adobe Experience Platform te maximaliseren.
* Manieren om de vraag te bouwen die op uw bestaande gegevensarchitectuur wordt gebaseerd.
* Zorg voor gegevenskwaliteit die aan uw behoeften voldoet, en methoden om eventuele tekortkomingen te beperken.
* Het proces om een vraag te plannen om bij een vastgestelde frequentie voor gebruik stroomafwaarts in segmentatie en bestemmingen voor verpersoonlijking te lopen.
* Het gemak voor marketers om afgeleide datasets in hun publiek door de macht van [!DNL Query Service] op te nemen.

## Doelstellingen {#objectives}

Deze workflowdemonstratie is gebaseerd op verschillende Adobe Experience Platform-services. Als u de stappen wilt volgen, is het raadzaam de volgende functies en services goed te begrijpen:

* De [ grondbeginselen van het Model van de Gegevens van de Ervaring (XDM) schemacompositie ](../../xdm/schema/composition.md)
* Hoe te [ datasets tot stand brengen en gegevens opnemen ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=nl-NL)
* Hoe te om [ gegevens in te voeren gebruikend de Adobe Analytics bronschakelaar ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=nl-NL)
* [Segmentatie](../../segmentation/home.md)
* [Bestemmingen](../../destinations/home.md)

In het voorbeeld voor het verlaten van een browser wordt het gebruik van Adobe [!DNL Analytics] -gegevens centraal gesteld bij het maken van een bepaald actionabel publiek. Het publiek is verfijnd en omvat alle klanten die de afgelopen vier dagen door de website hebben gebladerd, maar geen aankoop hebben gedaan. Elk profiel in het publiek wordt dan gericht met het hoogst-prijs SKU dat uit het gedragspatroon van de klant resulteerde.

De vraag zelf is zeer recept en omvat slechts gegevens die aan de criteria van het gebruiksgeval voor de segmentdefinitie voldoen. Hierdoor worden de prestaties verbeterd doordat de hoeveelheid [!DNL Analytics] gegevens die wordt verwerkt, tot een minimum wordt beperkt. De gegevens worden ook op prijs gesorteerd van het hoogst naar het laagst en de hoogst geprijsde SKU gekozen die de gebruiker aan het doorbladeren was.

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

## [!DNL Query Service] voorbeeld met bladerstopzetting met gebruik van adobe analytics {#video-example}

De onderstaande videopresentatie biedt een holistische, realistische gebruikscase voor uw Experience Platform-gegevens die zijn toegespitst op [!DNL Query Service] - en Adobe-analysemogelijkheden.

>[!VIDEO](https://video.tv.adobe.com/v/3454948?quality=12&learn=on&captions=dut)

## Voordelen van [!DNL Query Service] {#benefits}

De functies die [!DNL Query Service] biedt, zijn voor vele doeleinden. U kunt het gebruiken om complexe logica voor segmentatie, voor het berekenen van diverse gepersonaliseerde attributen voor gebruik stroomafwaarts aan te passen, of zeer te vereenvoudigen hoe u uw publiek bouwt.

Met [!DNL Query Service] kunt u beperkingen in uw query&#39;s opnemen om het proces voor publieksopbouw te vereenvoudigen. Dit verbetert de gegevenskwaliteit door ervoor te zorgen dat de juiste gegevens geschikt zijn voor uw publiek. Het handhaven van de kwaliteit van uw vraag resulteert in een nauwkeurig publiek en helpt met gegevensbetrouwbaarheid. U kunt uw publiek ook opslaan door schema&#39;s en douanetabellen te creëren die op attributen worden gebaseerd die uit uw vraag worden afgeleid. Een douanetabel kan voor Profiel worden toegelaten en u kunt deze gegevenspunten voor segmentatie en verpersoonlijking gebruiken. Deze functie helpt marketers die een duidelijk publiek van mensen willen creëren.

Door logica in uw query op te nemen die voldoet aan terugkerende of statische voorwaarden, extraheert [!DNL Query Service] ook de last van uitgebreide segmentatie.

Adobe Experience Platform biedt een gegevensopslagplaats en de benodigde hulpmiddelen om uw gegevens op een efficiënte en betrouwbare manier te activeren. Door gegevens in Experience Platform te bewaren, staat het u toe om attributen af te leiden terwijl het runnen van andere processen en verwijdert de behoefte om gegevens naar derdehulpmiddelen voor manipulatie en verwerking uit te voeren. Dergelijke verwerkingsoverheadkosten kunnen een projectchronologie zeer beïnvloeden wanneer het behandelen van honderden attributen of campagnes. Dit geeft marketers één enkele plaats om tot hun gegevens toegang te hebben en campagnes te bouwen evenals een zeer dynamische manier om hun berichten te segmenteren en te personaliseren.

## Volgende stappen

Door dit document te lezen, moet u nu begrijpen hoe [!DNL Query Service] niet alleen de kwaliteit van uw gegevens en het gemak van segmentatie beïnvloedt, maar ook het belang ervan binnen uw gegevensarchitectuur voor de volledige end-to-end workflow. Voor meer toepasselijke SQL voorbeelden die Adobe Analytics met [!DNL Query Service] gebruiken, zie het [ Adobe Analytics het handelende gebruik van variabelen case ](./merchandising-variables.md).

Andere documenten die de voordelen van [!DNL Query Service] aan de strategische bedrijfsinzichten van uw organisatie aantonen zijn [ allebei het gebruiken van geval ](./bot-filtering.md) voorbeeld filtreren.

U kunt deze documenten ook gebruiken voor een beter begrip van de functies van [!DNL Query Service] :

* [Richtlijnen voor het uitvoeren van query&#39;s](../best-practices/writing-queries.md)
* [ Begeleiding voor de organisatie van gegevensactiva ](../best-practices/organize-data-assets.md).


