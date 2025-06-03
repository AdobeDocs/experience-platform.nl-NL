---
title: Details van het door de klant gebruikte kwaliteitsscoremodel
description: Leer meer over het AI-model dat wordt gebruikt voor de AI van de Klant.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: 6623c7dad0fc4ddb7cb79e8f474b824915f130fc
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Details van het door de klant gebruikte kwaliteitsscoremodel

## Modeloverzicht {#model-overview}

* **Modelnaam en versie**: Het Scoremodel van de Volheid van AI van de Klant
* **Model doel**: Het model wordt ontworpen om marketers en de teams van de klantenovereenkomst van actionable inzichten te voorzien door de waarschijnlijkheid te voorspellen dat een consument een bepaalde actie, zoals het maken van een aankoop, het ondertekenen omhoog voor een abonnement, of het in dienst nemen van een e-mailcampagne zal uitvoeren. De output staat ondernemingen toe om publiekssegmentatie te optimaliseren en consumenteninteractie te personaliseren die op voorspeld gedrag wordt gebaseerd.
* **Beoogde gebruikers**: De primaire gebruikers van dit model zijn marketing beroeps, gegevensanalisten, en de teams van de klantenovereenkomst die hefboomwerking [ Real-Time CDP ](../../../rtcdp/home.md) om gegeven-gedreven marketing strategieën te drijven.
* **de gevallen van het Gebruik**: Dit model wordt hoofdzakelijk gebruikt voor de segmentatie van de consument, gerichte marketing, en karnvoorspelling. Bedrijven gebruiken dit model om de aankoopintentie van de consument te voorspellen, marketingcampagnes te optimaliseren en de inspanningen op het gebied van personalisatie te verbeteren. Een e-commercebedrijf kan het model bijvoorbeeld gebruiken om klanten met een hoge intentie te identificeren en hen exclusieve promoties aan te bieden.
* **Pijnpunten**: De verkopers worstelen vaak met het identificeren van de juiste consumenten om betrokkenheidsinspanningen te richten en te optimaliseren. Dit model vermindert giswerk door een gegevensgestuurde benadering van de doelgerichtheid van de consument te bieden, waarbij ervoor wordt gezorgd dat marketingmiddelen efficiënt worden toegewezen.
* **Potentieel misbruik**: Het model zou niet voor hoog-risico gebruiksgevallen, zoals financieel krediet scoring, medische diagnostiek, of wettelijke beoordelingen moeten worden gebruikt. Bovendien mag het model niet worden gebruikt bij het voorspellen van persoonlijk gevoelig gedrag (zoals gezondheidsomstandigheden, politieke voorkeuren).

## Modeldetails {#model-details}

* **Model type**: Dit is een onder toezicht lerend classificatiemodel dat de waarschijnlijkheid voorspelt van een gebeurtenis die (zoals aankoop, churn, overeenkomst) gegeven historische consumentengegevens voorkomt. Het wordt getraind gebruikend gradient-versterkende beslissingsbomen (GBDT) met logistieke regressie aan modelaandrangscores.
* **Input**: Het model verwerkt het gedragsgegevens van de consument, demografische attributen, en historische interactie. Dit omvat gegevens zoals de frequentie van het websitebezoek, de aankoopgeschiedenis in het verleden, de betrokkenheid bij marketing e-mails, en demografische informatie.
* **Output**: De modeloutput een score tussen 0 en 100, waar de hogere waarden op een hogere waarschijnlijkheid wijzen van de voorspelde gebeurtenis die onder de gescoorde bevolkingscohort voorkomt. Bovendien biedt het belangrijke scores voor functies, zodat marketers kunnen zien welke factoren de voorspelling beïnvloedden.

**input van het Voorbeeld**

```json
{ 
  "customer_id": 12345, 
  "past_purchases": 3, 
  "last_visit_days": 7,
  "email_click_rate": 0.4 
}
```

**output van het Voorbeeld**

```json
{ 
  "customer_id": 12345,
  "SCORE": 89 
}
```

## Modeltraining {#model-training}

* **de gegevens van de Opleiding en preprocessing**: De trainingsdataset voor elke klant wordt rechtstreeks afkomstig van hun eigen gegevens binnen Adobe Experience Platform. Dit omvat de historische interacties van de klant, transactiegegevens, gedragsbetrokkenheidslogboeken en demografische informatie zoals verzameld en opgeslagen in hun Adobe Experience Platform-instantie. De dataset gebruikt klant-specifieke gegevens over hun gekozen tijdskader, die hun unieke seizoensgebonden tendensen en betrokkenheidspatronen vangen. Vóór gebruik, ondergaat de dataset van elke klant preprocessing die aan hun gegevenskenmerken wordt aangepast, met inbegrip van ontbrekende waardebehandeling, categoriale het coderen, eigenschapschaling, outlier opsporing, en eigenschapengineering om optimale kwaliteit en bruikbaarheid voor hun specifiek gebruiksgeval te verzekeren
* **Specificaties van de Opleiding**: De modelhefboomwerkingen [!DNL LightGBM] gebruikend [!DNL GBM], die voor gestructureerde gegevens worden geoptimaliseerd. Het wordt getraind op historische reeksen van klantgebeurtenissen om voorspellende gedragspatronen te identificeren.
* **de kaders van de Opleiding**: Het model werd ontwikkeld gebruikend [!DNL LightGBM], en [!DNL scikit-learn], en op de wolkeninfrastructuur van Adobe AI getraind.
* **de infrastructuur van de Opleiding**: [!DNL Databricks] clusters.

## Modelevaluatie {#model-evaluation}

* **de metriek en de procedures van de Evaluatie**: De doeltreffendheid van het model wordt gemeten gebruikend [!DNL AUC-ROC]. Aangezien de AI van de Klant zich op een zeer brede waaier van klantengebruiksgevallen richt, kan het werkende waaier niet worden gekend. We gebruiken dus een metrische [!DNL AUC] die onafhankelijk is van bereik en budget.
* **de gegevens van de Evaluatie en preprocessing**: De gegevens van de evaluatie omvatten holdout consumentenverslagen en zijn preprocessing gelijkaardig aan opleidingsgegevens met eigenschapnormalisatie, het coderen, en schoonmaakstappen om inputformaatverwachtingen aan te passen. Nadat het resultaatvenster is overgegaan, kunnen wij een definitieve prestatiesevaluatie uitvoeren.

## Modelimplementatie {#model-deployment}

* **Modelplaatsing**: Het model wordt ontvangen op de diensten van Adobe Experience Platform AI en met diverse toepassingen van Adobe geïntegreerd. Het is beschikbaar via API-eindpunten, zodat u naadloze toegang hebt tot realtime voorspellingen en batchverwerking voor alle workflows voor marketing en betrokkenheid van consumenten.
* **Model controle**: Het model wordt onophoudelijk gecontroleerd via model controle om de verschuiving van de opleidingsopstelling te zien. Periodieke treinen (één keer in drie maanden) worden automatisch uitgevoerd.
* **Model ipdate**: Het model wordt opnieuw opgeleid eens in verscheidene maanden (maximum eens in 6 maanden) gebruikend bijgewerkte gegevens van de consumenteninteractie om voortdurende relevantie te verzekeren. Periodieke omscholing helpt het verschuiven van gegevens en seizoensschommelingen te beperken, wat een invloed kan hebben op de voorspellende nauwkeurigheid.

## Uitlegbaarheid {#explainability}

**Model verklarbaarheid**: De modelhefboomwerkingen [!DNL SHapley Additive Explanations] (SCHAP) om het effect van elke inputeigenschap op zijn voorspellingen te kwantificeren, die transparantie verstrekken in hoe de attributen van de consument de aandrijvingsscores beïnvloeden. De waarden van SHAP laten zowel globale interpretabiliteit toe, die de meest invloedrijke factoren over alle voorspellingen identificeert, als lokale interpretabiliteit, die individuele voorspellingen voor specifieke consumenten verklaren. Het model ondersteunt ook [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Fairness en afwijking {#fairness-and-bias}

* **Model billijkheid**: Dit model wordt getraind op anonymized gedragsgegevens verbonden aan koekjesidentiteitskaarts, zonder toegang tot beschermde demografische attributen zoals leeftijd, geslacht, of etniciteit. Als zodanig is het niet mogelijk de billijkheid van gevoelige groepen rechtstreeks te meten. Tot de inspanningen voor het beperken van vooronderstellingen behoren het normaliseren van de frequentie van de gebruikersactiviteit, het onderdrukken van al te dominante kenmerken en het uitvoeren van controles voor het kalibreren van de score bij cohorten. Wij zijn verantwoordelijk voor de recentieverhouding en controleren de belichtingsafwijking door modelvoorspellingen over willekeurig holdout-verkeer te evalueren. Er zijn doorlopende evaluaties beschikbaar om de versterking en feedback van voorkeuren tijdens de implementatie van het model te detecteren en te verminderen.
* **de vooroordelen van Gegevens**: De dataset is hoofdzakelijk afkomstig van high-engagement gebruikers, die selectievooroordelen kunnen introduceren. Om dit te beperken, past het model steekproefstrategieën toe. Afhankelijk van het gebruiksgeval, zouden de klanten moeten overwegen hoe de potentiële vooroordelen in modeloutput zich kunnen richten op of hun voorgenomen toepassing beïnvloeden.

## Robuustheid {#robustness}

**Model robuustheid**: Het model handhaaft sterke generalisering aan nieuwe consumentenverslagen. De prestaties blijven stabiel in verschillende consumentensegmenten, maar vertonen een lichte verslechtering wanneer het gedrag van de gebruiker aanzienlijk afwijkt van historische patronen.

## Ethische overwegingen {#ethical-considerations}

**Ethische overwegingen verbonden aan het model**: Dit model is bedoeld voor het op de markt brengen van gebruiksgevallen, en de klanten zouden verhoogde voorzichtigheid moeten uitoefenen als het toepassen van het in gevoelige of gereglementeerde domeinen zoals krediet of werkgelegenheid. De output is probabilistisch en afgeleid van gedragsgegevens, die historische of representatievooroordelen kunnen weerspiegelen. Klanten worden aangemoedigd om menselijk toezicht toe te passen. Adobe Experience Platform volgt de verantwoordelijke AI-richtlijnen, waarbij ervoor wordt gezorgd dat modellen vóór de implementatie onderworpen worden aan vertekende controles, aan een billijkheidstest en aan menselijk toezicht. Voor meer informatie, herzie de [ Beginselen van de Ethiek van Adobe AI ](https://www.adobe.com/content/dam/cc/en/ai-ethics/pdfs/Adobe-AI-Ethics-Principles.pdf?msockid=0d85c8269eb36f0801d0ddb49fd16ebc).