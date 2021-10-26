---
title: Overzicht van YouTube Video Tracking Extension
description: Meer informatie over de YouTube Video Tracking-tagextensie in Adobe Experience Platform.
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: bbaf272313d5a8afe33178598063164792f4d8c0
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# Overzicht van YouTube Video Tracking-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

**Vereisten**

Elke markeringseigenschap in Adobe Experience Platform vereist dat de volgende extensies worden geïnstalleerd en geconfigureerd via het scherm Extensies:

* Adobe Analytics
* Experience Cloud Bezoeker-id-service
* Kernextensie

Gebruik de [&quot;Een speler insluiten met een \&lt;iframe> tag&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) codefragment van de ontwikkelaar van Google documenteert in de HTML van elke Web-pagina waar een videospeler moet teruggeven.

Deze extensie, versie 2.0.1, ondersteunt het insluiten van een of meer YouTube-video&#39;s op één webpagina door een `id` kenmerk met een unieke waarde in de scripttag iframe, en toevoegen `enablejsapi=1` en `rel=0` tot het einde van de `src` kenmerkwaarde, als deze nog niet is opgenomen. Bijvoorbeeld:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Deze extensie is ook ontworpen om dynamisch te controleren op een unieke ID-kenmerkwaarde, zoals `player1`, ongeacht of de `enablejsapi` en `rel` de parameters van het vraagkoord bestaan en als hun verwachte waarden correct zijn. Als gevolg hiervan kan de YouTube-scripttag aan een webpagina worden toegevoegd met of zonder de `id` en of de `enablejsapi` en `rel` de parameters van het vraagkoord zijn inbegrepen of niet.

>[!NOTE]
>
>Op pagina&#39;s met meer dan één video gebruikt elke video dezelfde configuratieset in de tagregel die op die pagina wordt uitgevoerd. Als u bijvoorbeeld een regel maakt met een gebeurtenis die 50% video activeert, wordt de regel bij het 50%-actiepunt door elke video op de pagina geactiveerd.

De extensie is gebaseerd op de volgende logica voor het herschrijven van iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Er is dus een kleine flikkering nadat de pagina is geladen. Dit gedrag wordt verwacht.

## Gegevenselementen

Er zijn zes gegevenselementen beschikbaar binnen de uitbreiding, geen waarvan configuratie vereist.

* **Positie afspeelkop:** Registreert de plaats, in seconden, van de playhead positie op de videochronologie, wanneer het binnen een markeringsregel wordt geroepen.
* **Video-id:** Hiermee wordt de YouTube-id opgegeven die aan de video is gekoppeld.
* **Naam video:** Hiermee geeft u de beschrijvende of vriendelijke naam van de video op.
* **Video-URL:** Retourneert de YouTube.com-URL voor de video die momenteel is geladen/afgespeeld.
* **Videoduur:** Registreert de totale duur, in seconden, van de videoinhoud.
* **Extensieversie:** In dit gegevenselement wordt bijvoorbeeld de versie van YouTube Tracking Extension vastgelegd, zoals &quot;Video Tracking_YouTube_2.0.0&quot;.

## Gebeurtenissen

Er zijn acht gebeurtenissen beschikbaar binnen de uitbreiding, slechts vereist het Volgen van het Actiepunt van de Douane configuratie.

* **Video gereed:** De gebeurtenis wordt geactiveerd wanneer de video wordt begeleid en kan worden afgespeeld.
* **Start video:** Triggers wanneer de video voor het eerst wordt gestart en wanneer `player.getCurrentTime() === 0`
* **Video opnieuw afspelen:** De gebeurtenis wordt geactiveerd wanneer de video wordt afgespeeld en wordt opnieuw afgespeeld nadat de video is gestart. Deze trigger wordt bij elke replay geactiveerd.
* **Video pauzeren:** Triggers wanneer de video wordt gepauzeerd.
* **Video hervatten:** Triggers wanneer de video wordt hervat en wanneer `player.getCurrentTime() !== 0`
* **Aangepaste actiedraging:** Triggers wanneer de video het gespecificeerde videodrempelpercentage bereikt. Wanneer een video bijvoorbeeld 60 seconden is en het opgegeven actiepunt 50% is, wordt de gebeurtenis geactiveerd wanneer de positie van de afspeelkop gelijk is aan 30 seconden. Actiepunttracering is van toepassing op zowel het eerste afspelen als het opnieuw afspelen. Wanneer de gebruiker een actiepunt zoekt, wordt de gebeurtenis niet gestart. Actiepuntgebeurtenissen worden alleen geactiveerd wanneer de afspeelkop de berekende actiepuntlocatie op de tijdlijn overschrijdt en de videospeler wordt afgespeeld.
* **Videobuffer:** De gebeurtenis wordt geactiveerd wanneer de speler een bepaalde hoeveelheid gegevens downloadt voordat de video wordt afgespeeld.
* **Video beëindigd:** Triggers wanneer een video volledig is voltooid.

## Gebruik

Er kan één tagregel worden ingesteld voor elke videogebeurtenis (de zeven hierboven vermelde gebeurtenissen). Maak een specifieke tagregel voor elke gebeurtenis die u wilt bijhouden. Als u een gebeurtenis niet wilt volgen, laat u gewoon weg om er een regel voor te maken.

Regels hebben drie acties:

* **Variabelen instellen:** Stel de Adobe Analytics-variabelen in (kaart met alle of sommige opgenomen gegevenselementen).
* **Baken verzenden:** Verzend het baken van Adobe Analytics als een douane verbinding het volgen vraag, en verstrek een waarde van de Naam van de Verbinding &quot;van de Naam&quot;.
* **Variabelen wissen:** Wis de Adobe Analytics-variabelen.

## Voorbeeld van labelregel voor &quot;Video Start&quot;

De volgende video-extensieobjecten moeten worden opgenomen.

* **Gebeurtenissen**: &quot;Video starten&quot; (Deze gebeurtenis zorgt dat de regel wordt geactiveerd wanneer de bezoeker een YouTube-video begint af te spelen.)

* **Voorwaarde**: Geen

* **Handelingen**: Gebruik de **Extensie Analytics** om de actie &quot;Variabelen instellen&quot; toe te wijzen:

   * De gebeurtenis voor het starten van de video,
   * Een eigenschap/eVar voor het gegevenselement Videoduur
   * Een eigenschap/eVar voor het gegevenselement Video-id
   * Een eigenschap/eVar voor het gegevenselement Videonaam
   * Een eigenschap/eVar voor het URL-gegevenselement Video

   Dan omvat de &quot;Send Beacon&quot;actie (`s.tl`) met koppelingsnaam &quot;video start&quot;, gevolgd door de handeling &quot;Variabelen wissen&quot;.

>[!TIP]
> 
>Voor implementaties waarbij meerdere eVars of props voor elk video-element niet kunnen worden gebruikt, kunnen gegevenselementwaarden binnen het Platform worden samengevoegd, geparseerd in classificatierapporten met behulp van het gereedschap Classificatieregel Builder, zoals wordt uitgelegd in [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html)en vervolgens toegepast als een segment in Analysis Workspace.

Als u videogegevenswaarden wilt samenvoegen, maakt u een nieuw gegevenselement met de naam &quot;Videometagegevens&quot; en programmeert u dit om alle videogegevenselementen (hierboven vermeld) te verzamelen en samen te voegen. Bijvoorbeeld:

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
