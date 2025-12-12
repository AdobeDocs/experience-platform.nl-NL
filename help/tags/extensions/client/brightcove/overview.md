---
title: Overzicht van extensie voor het bijhouden van video in BrightStor
description: Meer informatie over de extensie van de tag BrightStor Video Tracking in Adobe Experience Platform.
exl-id: d27eff21-2abf-4495-8382-08cab32742e0
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Overzicht van de extensie BrightStor Video Tracking

## Voorwaarden

Voor elke tag-eigenschap in Adobe Experience Platform moeten de volgende extensies zijn geïnstalleerd en geconfigureerd in het scherm Extensie:

* Adobe Analytics
* Experience Cloud Visitor ID Service
* Geïnstalleerde kernextensies

Gebruik het codefragment &quot;In-Page embed code (Advanced)&quot; in de HTML van elke webpagina waar een videospeler moet renderen. Het &quot;In-Pagina inbedt code (Geavanceerd)&quot;fragment van HTML kan in de [ documentatie van de Helderheid worden gevonden ](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). De volgende verbinding verstrekt meer informatie over [ hoe te om ingebedde code voor zowel voorproef als gepubliceerde videospelers ](https://studio.support.brightcove.com/players/generating-player-embed-code.html) te produceren.

Deze extensie versie 1.1.0 biedt ondersteuning voor het insluiten van meerdere BrightStorCove-video&#39;s op één webpagina. Als er meerdere `id` -eigenschappen zijn binnen de geavanceerde insluittags, moet u ervoor zorgen dat ze allemaal unieke waarden hebben. Bijvoorbeeld `player1` , `player2` , enzovoort.

>[!NOTE]
>
>Op pagina&#39;s met meerdere video&#39;s gebruikt elke video dezelfde configuratieset in de tagregel die op die pagina wordt uitgevoerd. Als u bijvoorbeeld een regel maakt met een gebeurtenis die een video activeert die 50% voltooid is, activeert elke video op de pagina de regel bij het 50%-actiepunt.

Als de webpagina die deze extensie gebruikt, communiceert met de video voordat het betreffende script volledig is geladen, kunt u twee handelingen uitvoeren om het probleem op te lossen. Ten eerste kan de tagbibliotheek synchroon worden geladen en ten tweede plaatst u het element `<script type="text/javascript">\_satellite.pageBottom();\</script\>` vóór de video die op de pagina wordt ingesloten.

Zie de [ documentatie van BrightStor API ](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) voor meer informatie over de componentenmethodes en de gebeurtenissen die in deze uitbreiding worden gebruikt.

## Gegevenselementen

Er zijn zeven gegevenselementen beschikbaar binnen de uitbreiding, geen waarvan configuratie vereist.

* **Positie van de Playhead:** wanneer dit gegevenselement binnen een markeringsregel wordt geroepen, registreert het in seconden, de plaats van de playhead positie op de videochronologie.
* **identiteitskaart van de Rekening van de Video:** Dit gegevenselement registreert identiteitskaart van de rekening van de Helderheid die de video publiceerde.
* **VideoDuur:** Dit gegevenselement registreert de totale duur, in seconden, van de videoinhoud. Bovendien kan binnen Analytics een Berekende Metrisch worden gecreeerd om het aantal in seconden, in notulen of uren om te zetten.
* **Video Advertentie Steun:** Dit gegevenselement specificeert of de reclame binnen de video of niet wordt gesteund.
* **Video identiteitskaart:** Dit gegevenselement specificeert BrightStor verbonden aan de video.
* **Naam Video:** Dit gegevenselement specificeert de beschrijvende, of vriendschappelijke naam van de video.
* **VideoMarkeringen:** Dit gegevenselement specificeert de bijzondere manuscripten verbonden aan de video.

## Gebeurtenissen

Er zijn zeven gebeurtenissen beschikbaar binnen de uitbreiding, slechts vereist het Volgen van het Actiepunt van de Douane configuratie.

* **het Volgen van het Punt van het Richtsnoer van de Douane:** Deze gebeurtenis teweegbrengt wanneer de video het gespecificeerde percentage van de videodrempel bereikt. Wanneer een video bijvoorbeeld 60 seconden lang is en het opgegeven actiepunt 50% is, wordt de gebeurtenis geactiveerd met het teken van 30 seconden.

>[!NOTE]
>
>Deze gebeurtenis wordt telkens gestart wanneer dit actiepunt wordt bereikt. Als de gebruiker bijvoorbeeld het 50%-teken bereikt en de video opzoekt voordat het 50%-teken het 50%-teken bereikt, wordt de trigger opnieuw geactiveerd.

* **Voltooide Video:** Deze gebeurtenistrekkers wanneer een video volledig voltooit.
* **Video Geladen Meta-gegevens:** Deze gebeurtenis wordt in brand gestoken wanneer de speler aanvankelijke duur en afmetingsinformatie heeft ontvangen.
* **VideoPauze:** Deze gebeurtenis teweegbrengt wanneer de video wordt gepauzeerd.
* **Video hervat:** Deze gebeurtenis teweegbrengt wanneer de videoinhoud na een pauzegebeurtenis wordt hervat.
* **VideoVerandering van het Scherm:** de gebeurtenistrekkers wanneer de video binnen of uit volledig-schermwijze schakelt.
* **VideoBegin:** Deze gebeurtenis teweegbrengt wanneer de videoinhoud voor het eerst begint.

## Gebruik

Er kan één tagregel worden ingesteld voor elke videogebeurtenis (de zeven hierboven vermelde gebeurtenissen). Maak een specifieke tagregel voor elke gebeurtenis die u wilt bijhouden. Als u een gebeurtenis niet wilt volgen, laat u gewoon weg om er een regel voor te maken.

De regels bestaan uit drie acties:

1. Stel de Adobe Analytics-variabelen in. (Maak gegevenselementen voor alle of sommige van de hierboven vermelde gegevenselementen.)
1. Verzend het baken van Adobe Analytics.
1. Wis de Adobe Analytics-variabelen.

## Voorbeeld van labelregel voor &quot;Video Start&quot;

De volgende video-uitbreidingsobjecten moeten worden opgenomen:

* **Gebeurtenissen**

   1. &quot;Video starten&quot;: deze gebeurtenis zorgt ervoor dat de regel wordt geactiveerd wanneer de bezoeker begint met het afspelen van een BrightStor-video.

* **Condition**

   1. Geen

* **Acties**

   1. Stel in de handeling &#39;Variabelen instellen&#39; van Analytics de volgende optie in:

      * De gebeurtenis voor **VideoBegin** (voorbeeld: event17)
      * Prop/eVar voor het **VideoNaam** gegevenselement (voorbeeld: eVar10)
      * Prop/eVar voor het **gegevenselement van de Duur 0} Video (voorbeeld: eVar11)**
      * Prop/eVar voor **Huidige VideoPlaats** gegevenselement (voorbeeld: eVar12)

   1. De handeling Analytics &quot;Send Beacon&quot; (`s.tl`)
   1. De actie Analytics &quot;Clear Variables&quot;

>[!TIP]
>
>Voor degenen die niet veelvoudige eVars of steunen voor elk video element zouden kunnen willen verstrekken, worden de waarden van het gegevenselement aaneengeschakeld als alternatieve methode. Daarna worden ze geparseerd in classificatierapporten met het gereedschap Classificatieregel Builder. Zie de [ documentatie van de Bouwer van de Regel van de Classificatie van 0} {voor meer informatie. ](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) Tot slot worden zij in Analysis Workspace als een segment toegepast.
>
>Hiertoe maakt u een nieuw gegevenselement, bijvoorbeeld &quot;Video MetaData&quot;, en programmeert u dit om alle videogegevenselementen (hierboven vermeld) aan elkaar te koppelen.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
