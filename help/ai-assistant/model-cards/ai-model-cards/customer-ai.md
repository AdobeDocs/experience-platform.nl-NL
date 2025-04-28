---
title: Klanten met AI-kwaliteitsscore
description: Leer meer over het AI-model dat wordt gebruikt voor de AI van de Klant.
hide: true
hidefromtoc: true
exl-id: b2eeb1d2-3c2b-40a0-b5cd-91e99d99a906
source-git-commit: 63d95be281d1bc3867e4e24b9e7aadeecc64ac52
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---

# Klanten met AI-kwaliteitsscore

## Modeloverzicht {#model-overview}

* Het Score-model van AI-betrouwbaarheid van de Klant is ontworpen om marketers en teams voor de betrokkenheid van klanten te voorzien van bruikbare inzichten door de waarschijnlijkheid te voorspellen dat een klant een bepaalde actie zal uitvoeren, zoals een aankoop doen, zich aanmelden voor een abonnement of een e-mailcampagne starten. De output staat ondernemingen toe om publiekssegmentatie te optimaliseren en klanteninteractie aan te passen die op voorspeld gedrag wordt gebaseerd.
* De primaire gebruikers van dit model zijn marketing beroeps, gegevensanalisten, en de teams van de klantenovereenkomst die hefboomwerking [ Real-Time CDP ](../../../rtcdp/home.md) om gegeven-gedreven marketing strategieën te drijven.
* Dit model wordt hoofdzakelijk gebruikt voor klantensegmentatie, gerichte marketing, en karnvoorspelling. De ondernemingen hefboomwerking dit model om klantenkoopintentie te voorspellen, marketing campagnes te optimaliseren, en verpersoonlijkingsinspanningen te verbeteren. Een e-commercebedrijf kan het model bijvoorbeeld gebruiken om klanten met een hoge intentie te identificeren en hen exclusieve promoties aan te bieden.
* Marketers hebben vaak moeite met het identificeren van de juiste klanten om hun betrokkenheid te richten en te optimaliseren. Dit model vermindert giswerk door een gegeven-gedreven benadering van klantgericht te verstrekken, die ervoor zorgt dat de marketing middelen efficiënt worden toegewezen.
* Het model mag niet worden gebruikt voor besluitvorming met een hoog risico, zoals financiële kredietscore, medische diagnostiek of juridische beoordelingen. Bovendien is het niet bedoeld om persoonlijk gevoelig gedrag (bijvoorbeeld gezondheidsomstandigheden, politieke voorkeuren) te voorspellen vanwege potentiële ethische bezwaren.

## Modeldetails {#model-details}

* Dit is een onder toezicht staand classificatiemodel dat de waarschijnlijkheid voorspelt van een gebeurtenis (aankoop, churn, betrokkenheid) op basis van historische klantgegevens. Het wordt getraind gebruikend gradient-versterkende beslissingsbomen (GBDT) met logistieke regressie aan modelaandrangscores.
* Het model verwerkt gedragsgegevens van klanten, demografische kenmerken, en historische interactie. Dit omvat gegevens zoals de frequentie van het websitebezoek, de aankoopgeschiedenis in het verleden, de betrokkenheid bij marketing e-mails, en demografische informatie.
* Het model geeft een score tussen 0 en 100, waarbij hogere waarden een grotere kans op de voorspelde gebeurtenis tussen de gescoodeerde populatiecohort aangeven. Bovendien, verstrekt het eigenschapbelangrijkscores, die gebruikers toestaan om te begrijpen welke factoren de voorspelling beïnvloedden.

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

* De trainingsdataset voor elke klant is rechtstreeks afkomstig uit de eigen gegevens in Experience Platform. Dit omvat de historische interactie van de klant, transactiegegevens, gedragsbetrokkenheidslogboeken en demografische informatie zoals verzameld en opgeslagen in hun Experience Platform-instantie. De dataset gebruikt klant-specifieke gegevens over hun gekozen tijdskader, die hun unieke seizoensgebonden tendensen en betrokkenheidspatronen vangen. Vóór gebruik, ondergaat de dataset van elke klant preprocessing die aan hun gegevenskenmerken wordt aangepast, met inbegrip van ontbrekende waardebehandeling, categoriale het coderen, eigenschapschaling, outlier opsporing, en eigenschaptechniek om optimale kwaliteit en bruikbaarheid voor hun specifiek gebruiksgeval te verzekeren.
* Het model maakt gebruik van [!DNL LightGBM] met [!DNL GBM] , geoptimaliseerd voor gestructureerde gegevens. Het wordt getraind op historische reeksen van klantgebeurtenissen om voorspellende gedragspatronen te identificeren.
* Het model is ontwikkeld met [!DNL LightGBM] en [!DNL scikit-learn] en is opgeleid op het gebied van Adobe AI-cloudinfrastructuur.
* De computerbronnen die voor de modeltraining worden gebruikt, zijn [!DNL Databricks] clusters.

## Modelevaluatie {#model-evaluation}

* De effectiviteit van het model wordt gemeten met [!DNL AUC-ROC] . Aangezien de AI van de Klant zich op een zeer brede waaier van klantengebruiksgevallen richt, kan het werkende waaier niet worden gekend. Daarom wordt de metrische waarde [!DNL AUC] gebruikt omdat deze onafhankelijk is van bereik en budget.
* De gegevens van de evaluatie omvatten holdout klantenverslagen en zijn preprocessing vergelijkbaar met opleidingsgegevens met eigenschapnormalisatie, het coderen, en schoonmaakstappen om inputformaatverwachtingen aan te passen. Nadat het resultaatvenster is verstreken, kan de eindevaluatie worden uitgevoerd.

## Modelimplementatie {#model-deployment}

* Het model wordt gehost op Experience Platform AI-services en is geïntegreerd met verschillende Adobe-toepassingen. Het is beschikbaar via API-eindpunten, zodat u naadloze toegang hebt tot realtime voorspellingen en batchverwerking voor alle workflows voor marketing en betrokkenheid van klanten.
* Het model wordt voortdurend bewaakt via modelbewaking om te zien of de training is verlaten. Periodieke treinen (één keer in drie maanden) worden automatisch uitgevoerd.
* Het model wordt één keer per maand (maximaal één keer per zes maanden) gehertraind met bijgewerkte gegevens over de interactie met de klant om de blijvende relevantie te waarborgen. Periodieke omscholing helpt het verschuiven van gegevens en seizoensschommelingen te beperken, wat een invloed kan hebben op de voorspellende nauwkeurigheid.

## Uitlegbaarheid {#explainability}

Het model gebruikt [!DNL SHapley Additive Explanations] (SHAP) om het effect van elke inputeigenschap op zijn voorspellingen te kwantificeren, die transparantie verstrekken in hoe de klantenattributen de aandrijvingsscores beïnvloeden. De waarden van de SHAP laten zowel globale interpretabiliteit toe, die de meest invloedrijke factoren over alle voorspellingen identificeert, als lokale interpretabiliteit, die individuele voorspellingen voor specifieke klanten verklaren. Het model ondersteunt ook [!DNL Local Interpretable Model-Agnostic Explanations] (LIME).

## Fairness en afwijking {#fairness-and-bias}

* Dit model is getraind op geanonimiseerde gedragsgegevens in verband met cookie-id&#39;s, zonder toegang tot beschermde demografische kenmerken zoals leeftijd, geslacht of etniciteit. Als zodanig is het niet mogelijk de billijkheid van gevoelige groepen rechtstreeks te meten. Tot de inspanningen voor het beperken van vooronderstellingen behoren het normaliseren van de frequentie van de gebruikersactiviteit, het onderdrukken van al te dominante kenmerken en het uitvoeren van controles voor het kalibreren van de score bij cohorten.
* Het model is verantwoordelijk voor de recentieafwijking en de blootstellingsafwijking van de monitor door modelvoorspellingen over het gerandomiseerde holdout-verkeer te evalueren. Er zijn doorlopende evaluaties beschikbaar om de versterking en feedback van voorkeuren tijdens de implementatie van het model te detecteren en te verminderen.
* De dataset is voornamelijk afkomstig van gebruikers met een hoge betrokkenheid, wat selectievertekening kan veroorzaken. Om dit te beperken, past het model steekproefstrategieën toe.

## Robuustheid {#robustness}

Het model handhaaft sterke generalisering aan nieuwe klantenverslagen. De prestaties blijven stabiel voor verschillende klantsegmenten, maar vertonen een lichte verslechtering wanneer het gedrag van de gebruiker aanzienlijk afwijkt van historische patronen.

## Overwegingen met betrekking tot privacy en beveiliging {#privacy-and-security-considerations}

* Het model verwerkt of behoudt geen persoonlijk identificeerbare informatie (PII) en alle gegevens die voor de opleiding worden gebruikt, worden geanonimiseerd en samengevoegd. Het houdt zich aan strikte naleving van het privacybeleid van de GDPR, de CCPA en de interne Adobe. Het model neemt differentiële privacytechnieken, het hakken, anonymization, en tokenization op om privacy te verzekeren.
* Klant-AI houdt zich aan uw voorkeuren voor toestemming. Zodra u [ opstelling hebt en uw toestemmingsbeleid ](../../../data-governance/policies/user-guide.md#create-a-consent-policy) toegelaten, zal AI van de Klant de toestemmingsgegevens respecteren die van u worden verzameld. Alleen gegevens met toestemming worden gebruikt om het model te scoren in volgende uitvoeringen van het model. De nieuwe scores vervangen de oude scores en kunnen in segmentatie worden gebruikt. Deze functie is momenteel alleen beschikbaar voor klanten van het HealthCare Shield- en het Privacy- en beveiligingsschild.

## Ethische overwegingen {#ethical-considerations}

Het model zou in potentie een afwijking in de besluitvorming kunnen introduceren. Om dit te voorkomen, volgt Experience Platform de verantwoordelijke AI-richtsnoeren, waarbij ervoor wordt gezorgd dat modellen vóór de implementatie aan partijaudits, billijkheidstests en menselijk toezicht worden onderworpen.
