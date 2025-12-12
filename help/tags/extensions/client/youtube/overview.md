---
title: Overzicht van YouTube Video Tracking Extension
description: Meer informatie over de YouTube Video Tracking-tagextensie in Adobe Experience Platform.
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 1%

---

# Overzicht van YouTube Video Tracking-extensie

**Vereisten**

Elke markeringseigenschap in Adobe Experience Platform vereist dat de volgende extensies worden geïnstalleerd en geconfigureerd via het scherm Extensies:

* Adobe Analytics
* Experience Cloud Visitor ID Service
* Kernextensie

Gebruik [ &quot;bed een speler in gebruikend een \ &lt;iframe \> markering&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) codefragment van de de ontwikkelaarsdocs van Google in HTML van elke Web-pagina waar een videospeler moet teruggeven.

Deze extensie, versie 2.0.1, ondersteunt het insluiten van een of meer YouTube-video&#39;s op één webpagina door een `id` -kenmerk in te voegen met een unieke waarde in de iFrame-scripttag en `enablejsapi=1` en `rel=0` toe te voegen aan het einde van de `src` -kenmerkwaarde, als dit nog niet het geval is. Bijvoorbeeld:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Deze extensie is ook ontworpen om dynamisch te controleren op een unieke ID-kenmerkwaarde, zoals `player1` , ongeacht of de parameters van de queryreeks `enablejsapi` en `rel` bestaan en of de verwachte waarden juist zijn. Als gevolg hiervan kan de YouTube-scripttag worden toegevoegd aan een webpagina met of zonder het kenmerk `id` en of de parameters van de queryreeks `enablejsapi` en `rel` worden opgenomen of niet.

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

* **Positie van de Playhead:** registreert de plaats, in seconden, van de playhead positie op de videochronologie, wanneer het binnen een markeringsregel wordt geroepen.
* **Video identiteitskaart:** specificeert identiteitskaart van YouTube verbonden aan de video.
* **de Naam van de Video:** specificeert de beschrijvende, of vriendschappelijke naam van de video.
* **Video URL:** keert YouTube.com URL voor momenteel geladen/speel video terug.
* **VideoDuur:** registreert de totale duur, in seconden, van de videoinhoud.
* **Versie van de Uitbreiding:** Dit gegevenselement registreert de volgende versie van de Uitbreiding van YouTube, zoals &quot;Video Tracking_YouTube_2.0.0,&quot;bijvoorbeeld.

## Gebeurtenissen

Er zijn acht gebeurtenissen beschikbaar binnen de uitbreiding, slechts vereist het Volgen van het Actiepunt van de Douane configuratie.

* **Video Klaar:** Trekkers wanneer de video wordt begeleid, en klaar om te spelen.
* **VideoBegin:** Trekkers wanneer de video eerst is begonnen, en wanneer `player.getCurrentTime() === 0`
* **Video Replay:** Trekkers wanneer de video wordt begeleid, en na het aanvankelijke begin opnieuw gespeeld. Deze trigger wordt bij elke replay geactiveerd.
* **VideoPauze:** Trekkers wanneer de video wordt gepauzeerd.
* **Video hervat:** Trekkers wanneer de video wordt hervat, en wanneer `player.getCurrentTime() !== 0`
* **het Volgen van het Richtsnoer van de Douane:** Trekkers wanneer de video het gespecificeerde videodrempelpercentage bereikt. Wanneer een video bijvoorbeeld 60 seconden is en het opgegeven actiepunt 50% is, wordt de gebeurtenis geactiveerd wanneer de positie van de afspeelkop gelijk is aan 30 seconden. Actiepunttracering is van toepassing op zowel het eerste afspelen als het opnieuw afspelen. Wanneer de gebruiker een actiepunt zoekt, wordt de gebeurtenis niet gestart. Actiepuntgebeurtenissen worden alleen geactiveerd wanneer de afspeelkop de berekende actiepuntlocatie op de tijdlijn overschrijdt en de videospeler wordt afgespeeld.
* **Videobuffer:** Trekkers wanneer de speler een bepaalde hoeveelheid gegevens downloadt alvorens het begint speel de video.
* **Video beëindigde:** Trekkers wanneer een video volledig voltooit.

## Gebruik

Er kan één tagregel worden ingesteld voor elke videogebeurtenis (de zeven hierboven vermelde gebeurtenissen). Maak een specifieke tagregel voor elke gebeurtenis die u wilt bijhouden. Als u een gebeurtenis niet wilt volgen, laat u gewoon weg om er een regel voor te maken.

Regels hebben drie acties:

* **Vastgestelde variabelen:** plaats de variabelen van Adobe Analytics (kaart aan alle of sommige inbegrepen gegevenselementen).
* **verzend baken:** verzend het baken van Adobe Analytics als douane verbinding het volgen vraag, en verstrek een waarde &quot;van de Naam van de Verbinding&quot;.
* **Duidelijke variabelen:** ontruim de variabelen van Adobe Analytics.

## Voorbeeld van labelregel voor &quot;Video Start&quot;

De volgende video-extensieobjecten moeten worden opgenomen.

* **Gebeurtenissen**: &quot;Het VideoBegin&quot; (Deze gebeurtenis veroorzaakt de regel om te ontslaan wanneer de bezoeker begint een video van YouTube te spelen.)

* **Voorwaarde**: niets

* **Acties**: Gebruik de **uitbreiding van de Analyse** aan &quot;Reeks Variabelen&quot;actie, om in kaart te brengen:

   * De gebeurtenis voor het starten van de video,
   * Een prop/eVar voor het gegevenselement Videoduur
   * Een proxy/eVar voor het gegevenselement Video-id
   * A prop/eVar for the Video Name data element
   * Een proxy/eVar voor het URL-gegevenselement Video

  Dan, omvat de &quot;Send Beacon&quot;actie (`s.tl`) met verbindingsnaam &quot;videobegin,&quot;door een &quot;Duidelijke actie van Variabelen&quot;wordt gevolgd.

>[!TIP]
> 
>Voor implementaties waar de veelvoudige steunen of eVars voor elk videoelement niet kunnen worden gebruikt, kunnen de waarden van het gegevenselement binnen Experience Platform worden samengevoegd, die in classificatierapporten worden geparseerd gebruikend het hulpmiddel van de Bouwer van de Regel van de Classificatie, zoals die in [ https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html ](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html) wordt verklaard, en dan als segment in Analysis Workspace worden toegepast.

Als u videogegevenswaarden wilt samenvoegen, maakt u een nieuw gegevenselement met de naam &quot;Video Meta-gegevens&quot; en programmeert u dit om alle videogegevenselementen (hierboven vermeld) te verzamelen en samen te voegen. Bijvoorbeeld:

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```

Voor meer informatie over hoe te om en hefboomwerking gegevenselementen effectief binnen Experience Platform tot stand te brengen, lees de [ elementen van gegevenselementen ](../../../ui/managing-resources/data-elements.md) documentatie.
