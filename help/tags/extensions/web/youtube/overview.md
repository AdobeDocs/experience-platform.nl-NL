---
title: Overzicht van YouTube Video Tracking Extension
description: Meer informatie over de YouTube Video Tracking-tagextensie in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
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

Gebruik [&quot;bedt een speler in gebruikend een \&lt;iframe \> markering&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) codefragment van de de ontwikkelaarsdocs van Google in HTML van elke Web-pagina waar een videospeler moet teruggeven.

Deze extensie, versie 2.0.1, ondersteunt het insluiten van een of meer YouTube-video&#39;s op één webpagina door het invoegen van een `id`-kenmerk met een unieke waarde in de iframe-scripttag en het toevoegen van `enablejsapi=1` en `rel=0` aan het einde van de `src`-kenmerkwaarde, als deze nog niet is opgenomen. Bijvoorbeeld:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Deze extensie is ook ontworpen om dynamisch te controleren op een unieke ID-kenmerkwaarde, zoals `player1`, ongeacht of de parameters van de query `enablejsapi` en `rel` bestaan en of de verwachte waarden juist zijn. Dientengevolge, kan de het manuscriptmarkering van YouTube aan een Web-pagina met of zonder het `id` attribuut worden toegevoegd en of `enablejsapi` en `rel` de parameters van het vraagkoord of niet inbegrepen zijn.

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

* **Positie afspeelkop:** neemt de positie van de afspeelkop in seconden op de videotijdlijn op wanneer deze wordt aangeroepen binnen een tagregel.
* **Video-id:** geeft de YouTube-id op die aan de video is gekoppeld.
* **Videonaam:** geeft de beschrijvende of vriendelijke naam van de video op.
* **Video-URL:** Geeft de URL van YouTube.com voor de video die momenteel is geladen/afgespeeld.
* **Videoduur:** registreert de totale duur, in seconden, van de videoinhoud.
* **Extensieversie:** dit gegevenselement legt de YouTube Tracking Extension-versie vast, bijvoorbeeld &quot;Video Tracking_YouTube_2.0.0&quot;.

## Gebeurtenissen

Er zijn acht gebeurtenissen beschikbaar binnen de uitbreiding, slechts vereist het Volgen van het Actiepunt van de Douane configuratie.

* **Video gereed:** activeert wanneer de video wordt begeleid en klaar is om te worden afgespeeld.
* **Start video:** activeert wanneer de video voor het eerst wordt gestart en wanneer  `player.getCurrentTime() === 0`
* **Video opnieuw afspelen:** activeert wanneer de video wordt afgespeeld en opnieuw wordt afgespeeld na de eerste start. Deze trigger wordt bij elke replay geactiveerd.
* **Video pauzeren:** triggers wanneer de video wordt gepauzeerd.
* **Video hervatten:** activeert wanneer de video wordt hervat en wanneer  `player.getCurrentTime() !== 0`
* **Aangepaste actiedrempel:** triggers wanneer de video het opgegeven drempelpercentage voor de video bereikt. Wanneer een video bijvoorbeeld 60 seconden is en het opgegeven actiepunt 50% is, wordt de gebeurtenis geactiveerd wanneer de positie van de afspeelkop gelijk is aan 30 seconden. Actiepunttracering is van toepassing op zowel het eerste afspelen als het opnieuw afspelen. Wanneer de gebruiker een actiepunt zoekt, wordt de gebeurtenis niet gestart. Actiepuntgebeurtenissen worden alleen geactiveerd wanneer de afspeelkop de berekende actiepuntlocatie op de tijdlijn overschrijdt en de videospeler wordt afgespeeld.
* **Videobuffer:** activeert wanneer de speler een bepaalde hoeveelheid gegevens downloadt voordat de video wordt afgespeeld.
* **Video beëindigd:** Triggers wanneer een video volledig voltooit.

## Gebruik

Er kan één tagregel worden ingesteld voor elke videogebeurtenis (de zeven hierboven vermelde gebeurtenissen). Maak een specifieke tagregel voor elke gebeurtenis die u wilt bijhouden. Als u een gebeurtenis niet wilt volgen, laat u gewoon weg om er een regel voor te maken.

Regels hebben drie acties:

* **Variabelen instellen:de Adobe Analytics-variabelen** instellen (toewijzen aan alle of sommige opgenomen gegevenselementen).
* **Verzend baken:** verzend het baken van Adobe Analytics als douane verbinding het volgen vraag, en verstrek een &quot;Naam van de Verbinding&quot;waarde.
* **variabelen wissen:de Adobe Analytics-variabelen** wissen.

## Voorbeeld van labelregel voor &quot;Video Start&quot;

De volgende video-extensieobjecten moeten worden opgenomen.

* **Gebeurtenissen**: &quot;Video starten&quot; (Deze gebeurtenis zorgt dat de regel wordt geactiveerd wanneer de bezoeker een YouTube-video begint af te spelen.)

* **Voorwaarde**: Geen

* **Handelingen**: Met de handeling Variabelen instellen in de  **extensie** Analytics kunt u het volgende toewijzen:

   * De gebeurtenis voor het starten van de video,
   * Een eigenschap/eVar voor het gegevenselement Videoduur
   * Een eigenschap/eVar voor het gegevenselement Video-id
   * Een eigenschap/eVar voor het gegevenselement Videonaam
   * Een eigenschap/eVar voor het URL-gegevenselement Video

   Dan, omvat de &quot;Send Beacon&quot;actie (`s.tl`) met verbindingsnaam &quot;videobegin,&quot;die door een &quot;Duidelijke actie van Variabelen&quot;wordt gevolgd.

>[!TIP]
> 
>Voor implementaties waarbij meerdere eVars of props voor elk video-element niet kunnen worden gebruikt, kunnen de waarden van gegevenselementen binnen het Platform worden samengevoegd, worden geparseerd in classificatierapporten met behulp van het gereedschap Classificatieregel Builder, zoals wordt uitgelegd in [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) en vervolgens worden toegepast als een segment in Analysis Workspace.

Als u videogegevenswaarden wilt samenvoegen, maakt u een nieuw gegevenselement met de naam &quot;Videometagegevens&quot; en programmeert u dit om alle videogegevenselementen (hierboven vermeld) te verzamelen en samen te voegen. Bijvoorbeeld:

```javascript
var r = ””;

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
