---
title: Details van het model voor optimalisatie voor de verzendtijd
description: Meer informatie over het AI-model dat wordt gebruikt voor Send-Time Optimization in Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: d1c7d1038b45bae4c014e3488f55a427c9cb02ed
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# Details van het model voor optimalisatie voor de verzendtijd

## Modeloverzicht {#model-overview}

* **modelnaam en versie**: De Optimalisering van de Send-Time
* **Model versiedatum**: September 2024
* **Model doel**: Het model van de Optimalisering van de Optimalisatie van de Send-Time van Adobe Journey Optimizer kiest optimale verzendt tijd voor e-mail en duw berichten om consumentenbetrokkenheid te maximaliseren, die op de historische open en klikgedrag van uw consumenten wordt gebaseerd.
* **Beoogde gebruikers**: De primaire gebruikers van dit model zijn marketing beroeps, productmanagers, en de teams van de klantenovereenkomst die hefboomwerking Adobe Journey Optimizer om gegeven-gedreven marketing strategieën te drijven.
* **de gevallen van het Gebruik**: De optimalisering van de Send-Time wordt het best gebruikt op minder-urgente marketing mededelingen - bijvoorbeeld, een wekelijkse advertentie, promotieinformatie over een nieuw product, of informatie over een maand-lange verkoop. Send-Time optimalisatie is alleen beschikbaar voor ingebouwde e-mail- en push-actietypen van Journey Optimizer en is momenteel niet beschikbaar voor berichten die via aangepaste handelingen worden verzonden of voor andere actietypen.
* **Potentieel misbruik**: De Optimalisering van de Send-Time zou niet voor dringende, tijdgevoelige operationele berichten - bijvoorbeeld, een ordesbevestiging, een bericht van het wachtwoordterugstellen, of een bericht van de de veranderingsverandering van de vlieggate moeten worden gebruikt.

## Modeldetails {#model-details}

* **Model type**: Het model van de Optimalisatie van de Send-Time neemt de gegevens van het het consumentengedrag van Adobe Journey Optimizer van uw organisatie op en kijkt open gebruiker-niveau en klik gebeurtenissen om te voorspellen wanneer uw consumenten het meest waarschijnlijk met uw overseinen in dienst zullen nemen. Openen op consumentenniveau en klikken op gedrag voor elk uur van de week worden gewogen en gecombineerd met look-alike en algemeen consumentengedrag met een [!DNL Bayesian] -schatter. De [!DNL Bayesian] -voorspellingen voor elk uur van de week worden vervolgens gerangschikt, wat resulteert in een &#39;warmteoverzicht&#39; voor elke metrische waarde (e-mail wordt geopend, er wordt geklikt op e-mail en de push wordt geopend), zodat elke klant kan voorspellen hoeveel uren van de week contact met elke consument het meest en het minst tot het gewenste resultaat van de service zal leiden.
* **Input**: De optimalisering van de Send-Time gebruikt de gegevens van de consument timezone op het `timeZone` gebied binnen de [!UICONTROL Preference Details] gebiedsgroep, indien verstrekt, om timezone van een consument te bepalen. Als timezone van een consument niet beschikbaar op het `timeZone` gebied is, probeert de optimalisering van de Send-Time om timezone van de consument af te leiden, die op de gemeenschappelijkste tijdzonegelijke aan het eerste postadres wordt gebaseerd dat in het profiel van de consument wordt opgeslagen gebruikend het [ postadresgegevenstype ](../../xdm/data-types/postal-address.md). De Optimalisering van de Send-tijd maakt voorspellingen voor elke consument die op drie soorten gedragsgegevens wordt gebaseerd:
   * Het open en klikgedrag van uw consumenten in het algemeen.
   * Het open en klikkingsgedrag van het blik consumenten in de zelfde tijdzone.
   * Het open en klikgedrag van die individuele consument.
* **Output**: Deze voorspellingen worden gewogen en gecombineerd gebruikend een [!DNL Bayesian] benadering, resulterend in een &quot;warmtekaart&quot;voor elke metrische (e-mail opent, klikt e-mail, en de duw opent), voor elke klant, die op de uren van de week wijst die het contacteren dat de consument het meest en minst waarschijnlijk in het gewenste betrokkenheidsresultaat (open/klik) zal resulteren, zoals geïllustreerd in het onderstaande voorbeeld:

![ Send-Time de warmtekaart van de Optimalisering.](../images/models/send-time-optimization.png)

* **de input en output van het Voorbeeld**: Om het effect van het model op profielrijkdom te minimaliseren, worden de modelscores opgeslagen en samengeperst in drie attributen van het Profiel die in `_experience.intelligentServices.journeyAI.sendTimeOptimization` worden opgeslagen, en worden ontworpen om menselijk leesbaar niet te zijn.

## Modeltraining {#model-training}

* **de gegevens van de Opleiding en preprocessing**: De trainingsdataset voor elke organisatie wordt voortgebracht slechts uit hun eigen gegevens binnen Adobe Experience Platform.
   * Zodra de functie Send-Time Optimization voor uw organisatie wordt toegelaten, wordt het model getraind op e-mail en duw, verzendt, open, en klikt gebeurtenissen over alle reizen en acties van uw organisatie de afgelopen 16 weken - ongeacht of die acties Send-Time Optimalisering gebruiken. Hierdoor is Send-Time Optimization in staat om te profiteren van alle gegevens die door uw consumenten worden gegenereerd.
   * Modellen worden aanvankelijk opgeleid en wekelijks gescurfd. Na 16 weken worden de modellen opnieuw opgeleid en maandelijks opnieuw gecorreleerd. Modelscore omvat alle klantprofielen - zowel bestaand als nieuw - sinds de laatste scoring.
   * De berichten die door Send-Time Optimization worden verzonden ontvangen één van beiden van het volgende:
      * Een &quot;exploratie&quot;bericht verzendt tijd, selecteerde om verschillende verzendtijden te testen en te observeren hoe de consumenten antwoorden.
      * Een &quot;geoptimaliseerd&quot;bericht verzendt tijd, selecteerde om te maximaliseren klik/open tarieven. 5% van de verzendgebeurtenissen ontvangt een &#39;exploratie&#39;-verzendtijd en 95% van de verzendgebeurtenissen is &#39;geoptimaliseerd&#39;.
   * De exploratie verzendt tijden wordt geselecteerd in willekeurige volgorde van verzendtijden die door uw gevormde maximum wachttijd ter beschikking worden gesteld. Bijvoorbeeld, in het geval dat een bericht om 9 AM Woensdag met Send-Time Optimalisering wordt geselecteerd en een maximum wachttijd van 3 uur wordt aangezet, verzendt de Exploratie tijden voor het bericht gelijkelijk tussen 9 AM, 10 AM, 11 AM en 12 PM.

## Modelevaluatie {#model-evaluation}

* **modelevaluatie**: De optimalisering van de Send-Time kan e-mail kliktarief en duw open tarief in de waaier van ongeveer 2% tot 10% over alle berichten verhogen die door een organisatie worden geoptimaliseerd.
   * Als een organisatie bijvoorbeeld e-mailberichten verzendt zonder dat de tijd is geoptimaliseerd en u gemiddeld 5,0% klikt, kan dezelfde set e-mailberichten met optimalisatie van de verzendtijd gemiddeld maar liefst 5,5% klikken (5,0% * (1+10%) = 5,5%).
   * Wegens variabiliteit binnen kleine steekproefgrootte, kan een voordeel van Optimalisering Send-Time niet waarneembaar zijn op enig bericht verzendt.
   * Organisaties zullen waarschijnlijk meer baat hebben bij het gebruik van Send-Time Optimization wanneer:
      * Bestaande reizen maken gebruik van vaste en niet goed geoptimaliseerde verzendtijden;
      * Variaties in consumentengedrag (klikken en openen) komen overeen met de plaats waar de consument zich bevindt en de voorkeur van de consument;
      * Organisaties gebruiken Send-Time Optimization voor een groter deel van e-mail &amp; push-berichten;
      * Organisaties kiezen maximale wachttijden binnen het aanbevolen bereik van 6-12 uur.

## Modelimplementatie {#model-deployment}

* **Model update**: De modellen worden aanvankelijk opgeleid en gegraveerd wekelijks. Na 16 weken worden de modellen opnieuw opgeleid en maandelijks opnieuw gecorreleerd. Modelscore omvat alle consumentenprofielen - zowel bestaand als nieuw sinds de laatste scoring.

## Fairness en afwijking {#fairness-and-bias}

* **Model billijkheid**: De onjuiste gevolgtrekking van timezone van een consument kan in een bericht resulteren dat vroeger dan optimaal voor een bepaalde consument of later dan optimaal voor een bepaalde consument wordt verzonden. Nochtans, zullen alle consumenten in een mededeling die Send-Time Optimalisering gebruikt uiteindelijk een bericht ontvangen en de kans hebben om met een bericht in wisselwerking te staan. Bovendien maakt dit model geen gebruik van demografische gegevens of proxy&#39;s voor consumenten voor demografische gegevens - alleen gegevens over consumentengedrag en tijdzone voor consumenten worden gebruikt. Daarom zijn de zorgen over billijkheid beperkt en beperkt.
* **de vooroordelen van Gegevens**: De onjuiste gevolgtrekking van timezone van een consument kan in een bericht resulteren dat vroeger dan optimaal voor een bepaalde consument of later dan optimaal voor een bepaalde consument wordt verzonden. Nochtans, zullen alle consumenten in een mededeling die Send-Time Optimalisering gebruikt uiteindelijk een bericht ontvangen en de kans hebben om met een bericht in wisselwerking te staan. Bovendien maakt dit model geen gebruik van demografische gegevens of proxy&#39;s voor consumenten voor demografische gegevens - alleen gegevens over consumentengedrag en tijdzone voor consumenten worden gebruikt. Daarom zijn de zorgen over vertekeningen beperkt en beperkt.

## Robuustheid {#robustness}

* **Model robuustheid**: De profielen zonder voldoende gegevens van de interactiegebeurtenis (vaak het geval voor nieuwe profielen) zullen of onmiddellijk verzendt tijd, een exploratie verzendt tijd binnen het geselecteerde venster, of verzendt tijd die op best-presterende verzendt tijd over alle klanten wordt gebaseerd.

## Ethische overwegingen {#ethical-considerations}

* **Ethische overwegingen verbonden aan het model**: De onjuiste gevolgtrekking van timezone van een consument kan in een bericht resulteren dat vroeger dan optimaal voor een bepaalde consument of later dan optimaal voor een bepaalde consument wordt verzonden. Nochtans, zullen alle consumenten in een mededeling die Send-Time Optimalisering gebruikt uiteindelijk een bericht ontvangen en de kans hebben om met een bericht in wisselwerking te staan. Bovendien maakt dit model geen gebruik van demografische gegevens of proxy&#39;s voor consumenten voor demografische gegevens - alleen gegevens over consumentengedrag en tijdzone voor consumenten worden gebruikt. Daarom zijn ethische overwegingen beperkt en beperkt.