---
title: Details van het model voor optimalisatie voor de verzendtijd
description: Meer informatie over het AI-model dat wordt gebruikt voor Send-Time Optimization in Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: 481108135ee6ed5b90547e4e95799ab99edb210e
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# Details van het model voor optimalisatie voor de verzendtijd

## Modeloverzicht {#model-overview}

* **modelnaam en versie**: De Optimalisering van de Send-Time
* **Model versiedatum**: September 2024
* **Model doel**: Het model van de Optimalisering van de Optimalisatie van de Send-Time van Adobe Journey Optimizer kiest optimale verzendt tijd voor e-mail en duw berichten om klantenovereenkomst te maximaliseren, die op het historische open en klikgedrag van uw klanten wordt gebaseerd.
* **Beoogde gebruikers**: De primaire gebruikers van dit model zijn marketing beroeps, productmanagers, en de teams van de klantenovereenkomst die hefboomwerking Adobe Journey Optimizer om gegeven-gedreven marketing strategieën te drijven.
* **de gevallen van het Gebruik**: De optimalisering van de Send-Time wordt het best gebruikt op minder-urgente marketing mededelingen - bijvoorbeeld, een wekelijkse advertentie, promotieinformatie over een nieuw product, of informatie over een maand-lange verkoop. Send-Time optimalisatie is alleen beschikbaar voor ingebouwde e-mail- en push-actietypen van Journey Optimizer en is momenteel niet beschikbaar voor berichten die via aangepaste handelingen worden verzonden of voor andere actietypen.
* **Potentieel misbruik**: De Optimalisering van de Send-Time zou niet voor dringende, tijdgevoelige operationele berichten - bijvoorbeeld, een ordesbevestiging, een bericht van het wachtwoordterugstellen, of een bericht van de de veranderingsverandering van de vlieggate moeten worden gebruikt.

## Modeldetails {#model-details}

* **Model type**: Het model van de Optimalisatie van de Send-Time neemt de gegevens van het de klantengedrag van Adobe Journey Optimizer van uw organisatie op en kijkt open op gebruikersniveau en klikt gebeurtenissen om te voorspellen wanneer uw klanten het meest waarschijnlijk met uw overseinen in dienst zullen nemen. Openen en klikken op gebruikersniveau voor elk uur van de week worden gewogen en worden gecombineerd met algemene gebruikersgedragingen en algemene gebruikersgedragingen met een [!DNL Bayesian] -schatter. De [!DNL Bayesian] -voorspellingen voor elk uur van de week worden vervolgens gerangschikt, wat resulteert in een &#39;warmteoverzicht&#39; voor elke metrische waarde (e-mail wordt geopend, er wordt geklikt op e-mail en de push wordt geopend), voor elke klant, om de uren van de week te voorspellen dat het contact met elke gebruiker het meest en het minst waarschijnlijk zal resulteren in het gewenste betrokkenheidsresultaat.
* **Input**: De optimalisering van de Send-Tijd gebruikt de gegevens van de gebruikerstimezone op het `timeZone` gebied binnen de [!UICONTROL Preference Details] gebiedsgroep, indien verstrekt, om timezone van een gebruiker te bepalen. Als timezone van een gebruiker niet beschikbaar op het `timeZone` gebied is, probeert de optimalisering van de Send-Time om timezone van de gebruiker af te leiden, die op de gemeenschappelijkste timezone wordt gebaseerd aanpassen aan het eerste postadres dat in het profiel van de gebruiker wordt opgeslagen gebruikend het [ postadresgegevenstype ](../../../xdm/data-types/postal-address.md). De Optimalisering van de Send-Tijd maakt voorspellingen voor elke gebruiker die op drie soorten gedragsgegevens wordt gebaseerd:
   * Het algemene gedrag van de gebruikers voor het openen en klikken.
   * Het gedrag voor openen en klikken van gebruikers in dezelfde tijdzone.
   * Het gedrag van de afzonderlijke gebruiker bij het openen en klikken.
* **Output**: Deze voorspellingen worden gewogen en gecombineerd gebruikend een [!DNL Bayesian] benadering, resulterend in een &quot;warmtekaart&quot;voor elke metrische (e-mail opent, klikt e-mail, en de duw opent), voor elke klant, die op de uren van de week wijst die het contacteren van die gebruiker het meest en minst waarschijnlijk is om in de gewenste betrokkenheidsuitkomst (open/klik) te resulteren, zoals geïllustreerd in het onderstaande voorbeeld:

![ Send-Time de warmtekaart van de Optimalisering.](../../images/models/send-time-optimization.png)

* **de input en output van het Voorbeeld**: Om het effect van het model op profielrijkdom te minimaliseren, worden de modelscores opgeslagen en samengeperst in drie attributen van het Profiel die in `_experience.intelligentServices.journeyAI.sendTimeOptimization` worden opgeslagen, en worden ontworpen om menselijk leesbaar niet te zijn.

## Modeltraining {#model-training}

* **de gegevens van de Opleiding en preprocessing**: De trainingsdataset voor elke organisatie wordt voortgebracht slechts uit hun eigen gegevens binnen Adobe Experience Platform.
   * Zodra de functie Send-Time Optimization voor uw organisatie wordt toegelaten, wordt het model getraind op e-mail en duw, verzendt, open, en klikt gebeurtenissen over alle reizen en acties van uw organisatie de afgelopen 16 weken - ongeacht of die acties Send-Time Optimalisering gebruiken. Hierdoor is Send-Time Optimization in staat om te profiteren van alle gegevens die door uw klanten worden gegenereerd.
   * Modellen worden aanvankelijk opgeleid en wekelijks gescurfd. Na 16 weken worden de modellen opnieuw opgeleid en maandelijks opnieuw gecorreleerd. Modelscore omvat alle klantprofielen - zowel bestaand als nieuw - sinds de laatste scoring.
   * De berichten die door Send-Time Optimization worden verzonden ontvangen één van beiden van het volgende:
      * Een &quot;exploratie&quot;bericht verzendt tijd, geselecteerd om verschillende verzendtijden te testen en waar te nemen hoe de klanten antwoorden
      * Een &quot;geoptimaliseerd&quot;bericht verzendt tijd, selecteerde om te maximaliseren klik/open tarieven. 5% van de verzendgebeurtenissen ontvangt een &#39;exploratie&#39;-verzendtijd en 95% van de verzendgebeurtenissen is &#39;geoptimaliseerd&#39;.
   * De exploratie verzendt tijden wordt geselecteerd in willekeurige volgorde van verzendtijden die door uw gevormde maximum wachttijd ter beschikking worden gesteld. Bijvoorbeeld, in het geval dat een bericht om 9 AM Woensdag met Send-Time Optimalisering wordt geselecteerd en een maximum wachttijd van 3 uur wordt aangezet, verzendt de Exploratie tijden voor het bericht gelijkelijk tussen 9 AM, 10 AM, 11 AM en 12 PM.

## Modelevaluatie {#model-evaluation}

* **modelevaluatie**: De optimalisering van de Send-Time kan e-mail kliktarief en duw open tarief in de waaier van ongeveer 2% tot 10% over alle berichten verhogen die door een organisatie worden geoptimaliseerd.
   * Als een organisatie bijvoorbeeld e-mailberichten verzendt zonder dat de tijd is geoptimaliseerd en u gemiddeld 5,0% klikt, kan dezelfde set e-mailberichten met optimalisatie van de verzendtijd gemiddeld maar liefst 5,5% klikken (5,0% * (1+10%) = 5,5%).
   * Wegens variabiliteit binnen kleine steekproefgrootte, kan een voordeel van Optimalisering Send-Time niet waarneembaar zijn op enig bericht verzendt.
   * Organisaties zullen waarschijnlijk meer baat hebben bij het gebruik van Send-Time Optimization wanneer:
      * Bestaande reizen maken gebruik van vaste en niet goed geoptimaliseerde verzendtijden;
      * Variabiliteit in klantengedrag (klikken en openen) komt overeen met de locatie van de klant en de voorkeuren van de klant;
      * Organisaties gebruiken Send-Time Optimization voor een groter deel van e-mail &amp; push-berichten;
      * Organisaties kiezen maximale wachttijden binnen het aanbevolen bereik van 6-12 uur.

## Modelimplementatie {#model-deployment}

* **Model update**: De modellen worden aanvankelijk opgeleid en gegraveerd wekelijks. Na 16 weken worden de modellen opnieuw opgeleid en maandelijks opnieuw gecorreleerd. Modelscore omvat alle klantprofielen - zowel bestaand als nieuw sinds de laatste scoring.

## Fairness en afwijking {#fairness-and-bias}

* **Model billijkheid**: De onjuiste gevolgtrekking van timezone van een gebruiker kan in een bericht resulteren dat vroeger dan optimaal voor een bepaalde gebruiker of later dan optimaal voor een bepaalde gebruiker wordt verzonden. Nochtans, zullen alle gebruikers in een mededeling die Send-Time Optimalisering gebruikt uiteindelijk een bericht ontvangen en de kans hebben om met een bericht in wisselwerking te staan. Bovendien maakt dit model geen gebruik van demografische gegevens of proxy&#39;s van gebruikers voor demografische gegevens. Alleen gegevens over gebruikersgedrag en tijdzone van gebruikers worden gebruikt. Daarom zijn de zorgen over billijkheid beperkt en beperkt.
* **de vooroordelen van Gegevens**: De onjuiste gevolgtrekking van timezone van een gebruiker kan in een bericht resulteren dat vroeger dan optimaal voor een bepaalde gebruiker of later dan optimaal voor een bepaalde gebruiker wordt verzonden. Nochtans, zullen alle gebruikers in een mededeling die Send-Time Optimalisering gebruikt uiteindelijk een bericht ontvangen en de kans hebben om met een bericht in wisselwerking te staan. Bovendien maakt dit model geen gebruik van demografische gegevens of proxy&#39;s van gebruikers voor demografische gegevens. Alleen gegevens over gebruikersgedrag en tijdzone van gebruikers worden gebruikt. Daarom zijn de zorgen over vertekeningen beperkt en beperkt.

## Robuustheid {#robustness}

* **Model robuustheid**: De profielen zonder voldoende gegevens van de interactiegebeurtenis (vaak het geval voor nieuwe profielen) zullen of onmiddellijk verzendt tijd, een exploratie verzendt tijd binnen het geselecteerde venster, of verzendt tijd die op best-presterende verzendt tijd over alle klanten wordt gebaseerd.

## Ethische overwegingen {#ethical-considerations}

* **Ethische overwegingen verbonden aan het model**: De onjuiste gevolgtrekking van timezone van een gebruiker kan in een bericht resulteren dat vroeger dan optimaal voor een bepaalde gebruiker of later dan optimaal voor een bepaalde gebruiker wordt verzonden. Nochtans, zullen alle gebruikers in een mededeling die Send-Time Optimalisering gebruikt uiteindelijk een bericht ontvangen en de kans hebben om met een bericht in wisselwerking te staan. Bovendien maakt dit model geen gebruik van demografische gegevens of proxy&#39;s van gebruikers voor demografische gegevens. Alleen gegevens over gebruikersgedrag en tijdzone van gebruikers worden gebruikt. Daarom zijn ethische overwegingen beperkt en beperkt.
