---
title: Algemeen overzicht van de uitbreiding van SDK van het Web
description: Meer informatie over de extensie Common Web SDK Plugins in Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 0%

---

# Algemeen overzicht van de uitbreiding van de Insteekmodules van SDK van het Web

>[!IMPORTANT]
>
>De extensie is bedoeld voor gebruik met de extensie Adobe Experience Platform Web SDK. Voor informatie over de versie die bedoeld is om te worden gebruikt met AppMeasurement, raadpleegt u het overzicht over de [Common Analytics Plugins-extensie](../plugins/overview.md).

Dit document behandelt hoe te om de de marktextensie van de Insteekmodules van SDK van het Web te vormen en het te gebruiken om het [Adobe Experience Platform Web SDK-extensie](../sdk/overview.md).

## De extensie Algemene Web SDK-insteekmodules configureren

Deze sectie verstrekt een verwijzing voor de opties beschikbaar wanneer het vormen van de uitbreiding van de Insteekmodules van SDK van het Web.

>[!IMPORTANT]
>
>De gemeenschappelijke uitbreiding van de Insteekmodules van SDK van het Web is bedoeld om de uitbreiding van SDK van het Web van Adobe Experience Platform te versterken, nochtans, te hoeven u niet om het geïnstalleerd voor de uitbreiding te hebben om zoals verwacht te werken.

## Insteekmodules toevoegen aan de Adobe Experience Platform Web SDK-extensie

Geen configuratie is noodzakelijk om een stop in uw bibliotheek buiten het gebruiken van de volgende inheemse gegevenselementen te initialiseren of toe te voegen die door de Gemeenschappelijke uitbreiding van de Insteekmodules van SDK van het Web worden verstrekt:

* [`getAndPersistValue`](#getAndPersistValue)
* [`getGeoCoordinates`](#getGeoCoordinates)
* [`getNewRepeat`](#getNewRepeat)
* [getPagename`](#getPagename)
* [`getPreviousValue`](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [`getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [`getValOnce`](#getValOnce)
* [`getVisitDuration`](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [&quot;pFo&quot;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Met dit gegevenselement kunt u cookies instellen en door de gebruiker gegenereerde waarden in cookies opslaan. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getAndPersistValue` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). De `getAndPersistValue` in data-element wordt een waarde opgeslagen in een cookie die later tijdens een bezoek kan worden opgehaald.

De `getAndPersistValue` data element biedt de volgende argumenten:

* `vtp` (vereist): De waarde die van pagina tot pagina moet worden behouden
* `cn` (optioneel): De naam van het cookie waarin de waarde wordt opgeslagen. Als dit argument niet is ingesteld, krijgt het cookie de naam `"s_gapv"`
* `ex` (optioneel): Het aantal dagen voordat de cookie vervalt. Als dit argument `0` of niet is ingesteld, verloopt het cookie aan het einde van het bezoek (30 minuten inactiviteit).

Als de variabele in de `vtp` Het argument is ingesteld, dan stelt het gegevenselement de cookie in en retourneert de cookiewaarde. Als de variabele in de `vtp` -argument niet is ingesteld, retourneert het gegevenselement alleen de waarde van het cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Voor deze insteekmodule is locatietoegang op de client vereist, maar er wordt geen uitzondering gegenereerd als deze niet wordt opgehaald.

Hiermee kunt u de [`getGeoCoordinates` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). De `getGeoCoordinates` in het gegevenselement worden de breedte en lengte van bezoekersapparaten vastgelegd.

De `getGeoCoordinates` data element does not use any arguments. Deze geeft een van de volgende waarden:

* `"geo coordinates not available"`: Voor apparaten waarvoor geen gegevens over de geolocatie beschikbaar zijn op het moment dat de plug-in wordt uitgevoerd. Deze waarde komt vaak voor bij de eerste treffer van het bezoek, vooral wanneer bezoekers eerst toestemming moeten geven om hun locatie te volgen.
* `"error retrieving geo coordinates"`: Wanneer de plug-in fouten aantreft bij het ophalen van de locatie van het apparaat
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Wanneer [LATITUDE]/[LONGITUDE] zijn respectievelijk de lengte- en breedtegraad

### `getNewRepeat`

>[!IMPORTANT]
>
>Dit gegevenselement stelt cookies in. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getNewRepeat` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). De `getNewRepeat` gegevenselement bepaalt of een bezoeker van de site een nieuwe bezoeker of een herhaalde bezoeker binnen een gewenst aantal dagen is.

De `getNewRepeat` gegevenselement gebruikt de volgende argumenten:

* `d` (geheel getal, optioneel): Het minimumaantal dagen tussen bezoeken die bezoekers terugbrengen naar `"New"`. Als dit argument niet is ingesteld, wordt het standaard ingesteld op 30 dagen.

Dit gegevenselement retourneert de waarde van `"New"` als de cookie die door het gegevenselement is ingesteld, niet bestaat of is verlopen. De waarde van `"Repeat"` als de cookie die door het gegevenselement is ingesteld, bestaat en de tijd sinds de huidige hit en de tijd die in het cookie is ingesteld, langer is dan 30 minuten. Deze methode keert de zelfde waarde voor een volledig bezoek terug.

### `getPageName`

Hiermee kunt u de [`getPageName` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). De `getPageName` Met gegevenselement maakt u een leesvriendelijke, opgemaakte versie van de huidige URL.

De `getPageName` gegevenselement gebruikt de volgende argumenten:

* `si` (optioneel, tekenreeks): Een id die wordt ingevoegd aan het begin van de tekenreeks die de id van de site vertegenwoordigt. Deze waarde kan een numerieke id of een vriendelijke naam zijn. Wanneer deze niet is ingesteld, wordt standaard het huidige domein gebruikt.
* `qv` (optioneel, tekenreeks): Een door komma&#39;s gescheiden lijst met parameters van queryreeksen die, indien gevonden in de URL, worden toegevoegd aan de tekenreeks
* `hv` (optioneel, tekenreeks): Een door komma&#39;s gescheiden lijst met parameters gevonden in de URL-hash die, indien gevonden in de URL, aan de tekenreeks wordt toegevoegd
* `de` (optioneel, tekenreeks): Het scheidingsteken voor het opsplitsen van afzonderlijke delen van de tekenreeks. Heeft als standaardwaarde een pijp (`|`).

Het gegevenselement retourneert een tekenreeks met een gebruiksvriendelijke versie van de URL. Deze tekenreeks wordt doorgaans toegewezen aan de `pageName` variabele, maar kan ook in andere variabelen worden gebruikt.

### `getPreviousValue`

>[!IMPORTANT]
>
>Met dit gegevenselement kunt u cookies instellen en door de gebruiker gegenereerde waarden in cookies opslaan. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getPreviousValue` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). De `getPreviousValue` data element sets a variable to a value set on a previous hit.

De `getPreviousValue` gegevenselement gebruikt de volgende argumenten:

* `v` (tekenreeks, vereist): De variabele met de waarde die u wilt doorgeven aan de volgende afbeeldingsaanvraag. Een veelgebruikte variabele is `s.pageName` om de vorige paginawaarde op te halen.
* `c` (tekenreeks, optioneel): De naam van het cookie waarin de waarde wordt opgeslagen.  Als dit argument niet is ingesteld, wordt standaard ingesteld op `"s_gpv"`.

Wanneer u dit gegevenselement aanroept, wordt de tekenreekswaarde in het cookie geretourneerd. De insteekmodule stelt vervolgens de vervaldatum van het cookie opnieuw in en wijst er de variabelewaarde aan toe vanuit de `v` argument. Het cookie verloopt na 30 minuten inactiviteit.

### `getQueryParam`

Hiermee kunt u de [`getQueryParam` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). De `getQueryParam` data element extraheert de waarde van om het even welke parameter van het vraagkoord in een URL. Het is nuttig om campagnecodes, zowel intern als extern, uit het landen van pagina URLs te halen. Het is ook nuttig wanneer het halen van onderzoekstermijnen of andere parameters van het vraagkoord. Dit gegevenselement verstrekt robuuste eigenschappen in het ontleden van complexe URLs, met inbegrip van knoeiboel en URLs die veelvoudige parameters van het vraagkoord bevatten.

De `getQueryParam` gegevenselement gebruikt de volgende argumenten:

* `qsp` (vereist): Een door komma&#39;s gescheiden lijst met parameters voor queryreeksen die moet worden gezocht binnen de URL. Het is niet hoofdlettergevoelig.
* `de` (optioneel): Het scheidingsteken dat moet worden gebruikt als meerdere parameters van queryreeksen overeenkomen. Heeft als standaardwaarde een lege tekenreeks.
* `url` (optioneel): Een aangepaste URL, tekenreeks of variabele waaruit de parameterwaarden voor de queryreeks moeten worden geëxtraheerd. Standaardwaarden: `window.location`.

Wanneer dit gegevenselement wordt aangeroepen, wordt een waarde geretourneerd die afhankelijk is van de bovenstaande argumenten en de URL:

* Wanneer geen overeenkomende parameter voor een querytekenreeks wordt gevonden, retourneert de methode een lege tekenreeks.
* Wanneer een overeenkomende parameter voor een querytekenreeks wordt gevonden, retourneert de methode de parameterwaarde voor de queryreeks.
* Als een overeenkomende parameter voor een querytekenreeks wordt gevonden maar de waarde leeg is, wordt de methode geretourneerd `true`.
* Als er meerdere overeenkomende parameters voor queryreeksen worden gevonden, retourneert de methode een tekenreeks met elke parameterwaarde die door de tekenreeks in het dialoogvenster `de` argument.

### `getTimeParting`

Hiermee kunt u de [`getTimeParting` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). De `getTimeParting` data element vangt de details van de tijd aan wanneer om het even welke meetbare activiteit op uw plaats plaatsvindt. Dit gegevenselement is waardevol wanneer u metriek door om het even welke herhaalbare verdeling van tijd over een bepaalde datumwaaier wilt breken. U kunt bijvoorbeeld de conversiekoersen vergelijken tussen twee verschillende dagen van de week, zoals alle zondag en alle donderdag. U kunt periodes van de dag ook vergelijken, zoals alle ochtenden tegenover alle avonden.

De `getTimeParting` data element uses the following argument:

`t` (Optioneel maar aanbevolen, tekenreeks): De naam van de tijdzone waarnaar de lokale tijd van de bezoeker moet worden omgezet.  Wordt standaard ingesteld op UTC/GMT-tijd. Zie de [Lijst met tijdzones van TZ-databases](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) op Wikipedia voor een volledige lijst van geldige waarden.

Veelvoorkomende geldige waarden zijn:

* `"America/New_York"` voor Oost Tijd
* `"America/Chicago"` voor Central Time
* `"America/Denver"` voor Mountain Time
* `"America/Los_Angeles"` voor Pacific Time

Wanneer dit gegevenselement wordt aangeroepen, wordt een tekenreeks geretourneerd die het volgende bevat dat is gescheiden door een pipe (`|`):

* Het lopende jaar
* De huidige maand
* De dag van de maand
* De dag van de week
* De huidige tijd (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Dit gegevenselement stelt cookies in. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getTimeSinceLastVisit` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). De `getTimeSinceLastVisit` data element traceert hoelang een bezoeker heeft geduurd om na zijn laatste bezoek terug te keren naar uw site.

De `getTimeSinceLastVisit` data element does not use any arguments. Het retourneert de hoeveelheid tijd die is verstreken sinds de bezoeker voor het laatst naar de site is gekomen. Deze tijd wordt als volgt geplakt:

* De tijd tussen 30 minuten en een uur sinds het laatste bezoek is ingesteld op de dichtstbijzijnde halftijdse benchmark. Bijvoorbeeld, `"30.5 minutes"`, `"53 minutes"`
* De tijd tussen een uur en een dag wordt afgerond aan de dichtstbijzijnde benchmark van kwartier. Bijvoorbeeld, `"2.25 hours"`, `"7.5 hours"`
* Tijd langer dan een dag wordt afgerond naar de dichtstbijzijnde dagbenchmark. Bijvoorbeeld, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Als een bezoeker niet eerder is bezocht of de verstreken tijd langer is dan twee jaar, wordt de waarde ingesteld op `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Met dit gegevenselement kunt u cookies instellen en door de gebruiker gegenereerde waarden in cookies opslaan. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getValOnce` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). De `getValOnce` Met gegevenselement wordt voorkomen dat een variabele meerdere keren op dezelfde waarde wordt ingesteld.

De `getValOnce` gegevenselement gebruikt de volgende argumenten:

* `vtc` (vereist, tekenreeks): De variabele die moet worden gecontroleerd en gecontroleerd of deze eerder is ingesteld op een identieke waarde
* `cn` (optioneel, tekenreeks): De naam van het cookie dat de te controleren waarde bevat. Standaardwaarden: `"s_gvo"`
* `et` (optioneel, geheel getal): De vervaldatum van de cookie in dagen (of minuten, afhankelijk van de `ep` argument). Standaardwaarden: `0`, die aan het einde van de browsersessie verloopt
* `ep` (optioneel, tekenreeks): Stel dit argument alleen in als de `et` argument is ook ingesteld. Stel dit argument in op `"m"` als u de `et` argument om in minuten in plaats van dagen te verlopen. Standaardwaarden: `"d"`, waarin de `et` argument in dagen.

Als de `vtc` argument- en cookiewaarde komen overeen, retourneert deze methode een lege tekenreeks. Als de `vtc` argument- en cookiewaarde komen niet overeen, de methode retourneert de waarde `vtc` argument als tekenreeks.

### `getVisitDuration`

>[!IMPORTANT]
>
>Dit gegevenselement stelt cookies in. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getVisitDuration` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). De `getVisitDuration` het gegevenselement volgt de hoeveelheid tijd in notulen dat de bezoeker op de plaats tot dat punt is geweest.

De `getVisitDuration` data element does not use any arguments. Deze geeft een van de volgende waarden:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` waarbij `[x]` het aantal minuten dat is verstreken sinds de bezoeker op de site is aangeland)

### `getVisitNum`

>[!IMPORTANT]
>
>Dit gegevenselement stelt cookies in. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getVisitNum` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). De `getVisitNum` het gegevenselement retourneert het bezoeknummer voor alle bezoekers die binnen het gewenste aantal dagen naar de site komen .

De `getVisitNum` gegevenselement gebruikt de volgende argumenten:

* `rp` (optioneel, geheel getal OF tekenreeks): Het aantal dagen voordat de teller van het bezoeknummer opnieuw wordt ingesteld.  Standaardwaarden: `365` wanneer niet ingesteld.
   * Wanneer dit argument `"w"`, de tellerherstelt aan het einde van de week (deze zaterdag om 23:59 uur)
   * Wanneer dit argument `"m"`, de tellerherstelt aan het einde van de maand (de laatste dag van deze maand)
   * Wanneer dit argument `"y"`, de tegenposten aan het einde van het jaar (31 december)
* `erp` (optioneel, Booleaans): Wanneer de `rp` argument is een getal, dit argument bepaalt of de vervaldatum van het bezoeknummer moet worden verlengd. Indien ingesteld op `true`, worden bij volgende treffers naar uw site de teller van het bezoeknummer opnieuw ingesteld. Indien ingesteld op `false`, worden volgende hits op uw site niet uitgebreid wanneer de teller van het bezoeknummer opnieuw wordt ingesteld. Standaardwaarden: `true`. Dit argument is niet geldig wanneer het `rp` argument is een tekenreeks.

Het aantal bezoekers neemt toe wanneer de bezoeker na 30 minuten inactiviteit terugkeert naar uw site. Als deze methode wordt aangeroepen, wordt een geheel getal geretourneerd dat het huidige bezoeknummer van de bezoeker vertegenwoordigt.

### `p_fo` (Alleen pagina eerste)

Hiermee kunt u de [`p_fo` Plug-in Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). De `p_fo` data-element is een hulpprogramma dat controleert of er een specifiek JavaScript-object bestaat. Als het object niet bestaat, maakt de plug-in het object en wordt deze geretourneerd `true`. Als het JavaScript-object al op de pagina aanwezig is, wordt het geretourneerd `false`. Dit gegevenselement is nuttig om code precies één keer op een pagina uit te voeren.

De `p_fo` gegevenselement gebruikt de volgende argumenten:

* `on` (vereist, tekenreeks): De naam van het JavaScript-object dat het gegevenselement maakt als het object nog niet op de pagina bestaat.

Als het object nog niet bestaat, wordt deze methode geretourneerd `true` en maakt het object. Als het object al bestaat, wordt deze methode geretourneerd `false`.
