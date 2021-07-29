---
title: Overzicht van extensie voor het bijhouden van video in BrightStor
description: Meer informatie over de extensie van de tag BrightStor Video Tracking in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 0%

---

# Overzicht van de extensie BrightStor Video Tracking

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## Voorwaarden

Voor elke tag-eigenschap in Adobe Experience Platform moeten de volgende extensies zijn geïnstalleerd en geconfigureerd in het scherm Extensie:

* Adobe Analytics
* Experience Cloud Bezoeker-id-service
* Geïnstalleerde kernextensies

Gebruik het codefragment &quot;In-Page embed code (Advanced)&quot; in de HTML van elke Web-pagina waar een videospeler moet teruggeven. Het HTML-fragment &quot;In-Page Embed code (Advanced)&quot; vindt u in de [Heldercove-documentatie](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). De volgende koppeling biedt meer informatie over [hoe u ingesloten code kunt genereren voor zowel voorvertoning als gepubliceerde videospelers](https://studio.support.brightcove.com/players/generating-player-embed-code.html).

Deze extensie versie 1.1.0 biedt ondersteuning voor het insluiten van meerdere BrightStorCove-video&#39;s op één webpagina. Als er meerdere `id`-eigenschappen zijn binnen de geavanceerde insluittags, moet u ervoor zorgen dat ze allemaal unieke waarden hebben. Bijvoorbeeld `player1`, `player2`, enzovoort.

>[!NOTE]
>
>Op pagina&#39;s met meerdere video&#39;s gebruikt elke video dezelfde configuratieset in de tagregel die op die pagina wordt uitgevoerd. Als u bijvoorbeeld een regel maakt met een gebeurtenis die een video activeert die 50% voltooid is, activeert elke video op de pagina de regel bij het 50%-actiepunt.

Als de webpagina die deze extensie gebruikt, communiceert met de video voordat het betreffende script volledig is geladen, kunt u twee handelingen uitvoeren om het probleem op te lossen. Ten eerste kan de tagbibliotheek synchroon worden geladen en ten tweede plaatst u het element `<script type="text/javascript">\_satellite.pageBottom();\</script\>` vóór de video die op de pagina wordt ingesloten.

Raadpleeg de [documentatie van de BrightStor API](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) voor meer informatie over de componentmethoden en -gebeurtenissen die in deze extensie worden gebruikt.

## Gegevenselementen

Er zijn zeven gegevenselementen beschikbaar binnen de uitbreiding, geen waarvan configuratie vereist.

* **Positie afspeelkop:** wanneer dit gegevenselement wordt aangeroepen binnen een tagregel, wordt het in seconden vastgelegd, de positie van de afspeelkop op de videotijdlijn.
* **Video-account-id:** dit gegevenselement neemt de id op van de BrightStor ARCserve-account die de video heeft gepubliceerd.
* **Videoduur:** dit gegevenselement registreert de totale duur, in seconden, van de video-inhoud. Bovendien kan binnen Analytics een Berekende Metrisch worden gecreeerd om het aantal in seconden, in notulen of uren om te zetten.
* **Ondersteuning voor video-advertentie:** dit gegevenselement geeft aan of advertenties in de video worden ondersteund of niet.
* **Video-id:** dit gegevenselement geeft de BrightStor-id aan die aan de video is gekoppeld.
* **Videonaam:** Dit gegevenselement geeft de beschrijvende of vriendelijke naam van de video op.
* **Videotags:** dit gegevenselement geeft de specifieke scripts op die aan de video zijn gekoppeld.

## Gebeurtenissen

Er zijn zeven gebeurtenissen beschikbaar binnen de uitbreiding, slechts vereist het Volgen van het Actiepunt van de Douane configuratie.

* **Aangepast actiepunt bijhouden:** deze gebeurtenis wordt geactiveerd wanneer de video het opgegeven drempelpercentage voor de video bereikt. Wanneer een video bijvoorbeeld 60 seconden lang is en het opgegeven actiepunt 50% is, wordt de gebeurtenis geactiveerd met het teken van 30 seconden.

>[!NOTE]
>
>Deze gebeurtenis wordt telkens gestart wanneer dit actiepunt wordt bereikt. Als de gebruiker bijvoorbeeld het 50%-teken bereikt en de video opzoekt voordat het 50%-teken het 50%-teken bereikt, wordt de trigger opnieuw geactiveerd.

* **Video voltooid:** Deze gebeurtenis activeert wanneer een video volledig is voltooid.
* **Video geladen metagegevens:** deze gebeurtenis wordt geactiveerd wanneer de speler initiële informatie over de duur en de afmetingen heeft ontvangen.
* **Video pauzeren:** Deze gebeurtenis wordt geactiveerd wanneer de video wordt gepauzeerd.
* **Video hervatten:** deze gebeurtenis activeert wanneer de video-inhoud wordt hervat na een pauze-gebeurtenis.
* **Videoscherm wijzigen:** de gebeurtenis wordt geactiveerd wanneer de video in- of uitschakelt naar de modus Volledig scherm.
* **Video starten:** Deze gebeurtenis start wanneer video-inhoud voor het eerst wordt gestart.

## Gebruik

Er kan één tagregel worden ingesteld voor elke videogebeurtenis (de zeven hierboven vermelde gebeurtenissen). Maak een specifieke tagregel voor elke gebeurtenis die u wilt bijhouden. Als u een gebeurtenis niet wilt volgen, laat u gewoon weg om er een regel voor te maken.

De regels hebben drie acties:

1. Stel de Adobe Analytics-variabelen in. (Maak gegevenselementen voor alle of sommige van de hierboven vermelde gegevenselementen.)
1. Verzend het baken van Adobe Analytics.
1. Wis de Adobe Analytics-variabelen.

## Voorbeeld van labelregel voor &quot;Video Start&quot;

De volgende video-uitbreidingsobjecten moeten worden opgenomen:

* **Gebeurtenissen**

   1. &quot;Video Start&quot;: Deze gebeurtenis zorgt ervoor dat de regel wordt geactiveerd wanneer de bezoeker een BrightStor-video begint af te spelen.

* **Condition**

   1. Geen

* **Acties**

   1. Stel in de handeling &#39;Variabelen instellen&#39; van Analytics de volgende optie in:

      * De gebeurtenis voor **Video Start** (voorbeeld: event17)
      * A prop/eVar for the **Video Name** data element (example: eVar10)
      * A prop/eVar for the **Video Duration** data element (example: eVar 11)
      * A prop/eVar for for the **Current Video Place** data element (voorbeeld: eVar12)
   1. De handeling Analytics &quot;Send Beacon&quot; (`s.tl`)
   1. De actie Analytics &quot;Clear Variables&quot;


>[!TIP]
>
>Voor degenen die misschien geen veelvoudige eVars of steunen voor elk videoelement willen verstrekken, is er een alternatieve methode. Waarden voor gegevenselementen kunnen worden samengevoegd in de gebruikersinterface voor gegevensverzameling. Daarna worden ze geparseerd in classificatierapporten met het gereedschap Classificatieregel Builder. Raadpleeg de documentatie [Classification Rule Builder](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) voor meer informatie. Tot slot worden zij in Analysis Workspace als een segment toegepast.
>
>Hiertoe maakt u een nieuw gegevenselement, bijvoorbeeld &quot;Video MetaData&quot;, en programmeert u dit om alle videogegevenselementen (hierboven vermeld) aan elkaar te koppelen.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
