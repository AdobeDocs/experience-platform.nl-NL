---
title: Algemeen overzicht van de uitbreiding van SDK van het Web
description: Meer informatie over de extensie Common Web SDK Plugins in Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# Algemeen overzicht van de uitbreiding van SDK-insteekmodules voor web

>[!IMPORTANT]
>
>De extensie is bedoeld voor gebruik met de extensie Adobe Experience Platform Web SDK. Om informatie over de versie te zien die bedoeld is om met AppMeasurement te worden gebruikt, verwijs naar het overzicht over de [ Gemeenschappelijke uitbreiding van de Insteekmodules van Analytics ](../plugins/overview.md).

Dit document behandelt hoe te om de de markeringsuitbreiding van de Insteekmodules van SDK van het Web te vormen en het te gebruiken om de [ uitbreiding van SDK van het Web van Adobe Experience Platform ](../web-sdk/overview.md) te verhogen.

## De extensie Algemene Web SDK-insteekmodules configureren

Deze sectie verstrekt een verwijzing voor de opties beschikbaar wanneer het vormen van de uitbreiding van de Insteekmodules van SDK van het Web.

>[!IMPORTANT]
>
>De gemeenschappelijke uitbreiding van de Insteekmodules van SDK van het Web is bedoeld om de uitbreiding van SDK van het Web van Adobe Experience Platform te versterken, nochtans, te hoeven u niet om het geïnstalleerd voor de uitbreiding te hebben om zoals verwacht te werken.

## Insteekmodules toevoegen aan de Adobe Experience Platform Web SDK-extensie

Geen configuratie is noodzakelijk om een stop in uw bibliotheek buiten het gebruiken van de volgende inheemse gegevenselementen te initialiseren of toe te voegen die door de Gemeenschappelijke uitbreiding van de Insteekmodules van SDK van het Web worden verstrekt:

* [getAndPersistValue`](#getAndPersistValue)
* [getGeoCoordinates`](#getGeoCoordinates)
* [` getNewRepeat`](#getNewRepeat)
* [getPagename`](#getPagename)
* [getPreviousValue`](#getPreviousValue)
* [` getQueryParam`](#getQueryParam)
* [getTimeParting`](#getTimeParting)
* [getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [getValOnce`](#getValOnce)
* [getVisitDuration`](#getVisitDuration)
* [` getVisitNum`](#getVisitNum)
* [&quot;pFo&quot;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Met dit gegevenselement kunt u cookies instellen en door de gebruiker gegenereerde waarden in cookies opslaan. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getAndPersistValue` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html) instellen en configureren. In het gegevenselement `getAndPersistValue` wordt een waarde opgeslagen in een cookie die later tijdens een bezoek kan worden opgehaald.

Het gegevenselement `getAndPersistValue` bevat de volgende argumenten:

* `vtp` (vereist): de waarde die van pagina naar pagina moet blijven bestaan
* `cn` (optioneel): De naam van het cookie dat de waarde moet opslaan. Als dit argument niet is ingesteld, krijgt het cookie de naam `"s_gapv"`
* `ex` (optioneel): Het aantal dagen voordat de cookie vervalt. Als dit argument `0` is of niet is ingesteld, verloopt het cookie aan het einde van het bezoek (30 minuten inactiviteit).

Als de variabele in het argument `vtp` is ingesteld, wordt het cookie door het gegevenselement ingesteld en wordt de cookiewaarde geretourneerd. Als de variabele in het argument `vtp` niet is ingesteld, retourneert het gegevenselement alleen de cookiewaarde.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Voor deze insteekmodule is locatietoegang op de client vereist, maar er wordt geen uitzondering gegenereerd als deze niet wordt opgehaald.

Hiermee kunt u de [`getGeoCoordinates` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html) instellen en configureren. Met het gegevenselement `getGeoCoordinates` worden de breedte en lengte van bezoekersapparaten vastgelegd.

Het gegevenselement `getGeoCoordinates` gebruikt geen argumenten. Deze geeft een van de volgende waarden:

* `"geo coordinates not available"`: voor apparaten waarvoor geen gegevens over de geolocatie beschikbaar zijn op het moment dat de plug-in wordt uitgevoerd. Deze waarde komt vaak voor bij de eerste treffer van het bezoek, vooral wanneer bezoekers eerst toestemming moeten geven om hun locatie te volgen.
* `"error retrieving geo coordinates"`: Wanneer de plug-in fouten aantreft bij het ophalen van de locatie van het apparaat
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Waar [ LATITUDE ]/[ LONGITUDE ] de breedte en de lengtegraad, respectievelijk zijn

### `getNewRepeat`

>[!IMPORTANT]
>
>Met dit gegevenselement worden cookies ingesteld. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getNewRepeat` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html) instellen en configureren. Het gegevenselement `getNewRepeat` bepaalt of een bezoeker van de site een nieuwe bezoeker of een herhaalde bezoeker binnen een gewenst aantal dagen is.

Het gegevenselement `getNewRepeat` gebruikt de volgende argumenten:

* `d` (geheel getal, optioneel): Het minimale aantal dagen dat is vereist tussen bezoeken waarbij bezoekers worden teruggezet naar `"New"` . Als dit argument niet is ingesteld, wordt het standaard ingesteld op 30 dagen.

Dit gegevenselement retourneert de waarde van `"New"` als de cookie die door het gegevenselement is ingesteld, niet bestaat of is verlopen. De waarde `"Repeat"` wordt geretourneerd als het cookie dat door het gegevenselement is ingesteld, bestaat en de tijd sinds de huidige hit en de tijd die in het cookie is ingesteld, langer is dan 30 minuten. Deze methode keert de zelfde waarde voor een volledig bezoek terug.

### `getPageName`

Hiermee kunt u de [`getPageName` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html) instellen en configureren. Met het gegevenselement `getPageName` kunt u een leesbare, vriendelijke opgemaakte versie van de huidige URL maken.

Het gegevenselement `getPageName` gebruikt de volgende argumenten:

* `si` (optioneel, tekenreeks): een id die wordt ingevoegd aan het begin van de tekenreeks die de id van de site vertegenwoordigt. Deze waarde kan een numerieke id of een vriendelijke naam zijn. Wanneer deze niet is ingesteld, wordt standaard het huidige domein gebruikt.
* `qv` (optioneel, tekenreeks): een door komma&#39;s gescheiden lijst met parameters van queryreeksen die, indien aanwezig in de URL, aan de tekenreeks worden toegevoegd
* `hv` (optioneel, tekenreeks): een door komma&#39;s gescheiden lijst met parameters in de URL-hash die, indien aanwezig in de URL, aan de tekenreeks worden toegevoegd
* `de` (optioneel, tekenreeks): het scheidingsteken voor het opsplitsen van afzonderlijke delen van de tekenreeks. Heeft als standaardwaarde een pipe (`|`).

Het gegevenselement retourneert een tekenreeks met een gebruiksvriendelijke versie van de URL. Deze tekenreeks wordt doorgaans toegewezen aan de variabele `pageName` , maar kan ook in andere variabelen worden gebruikt.

### `getPreviousValue`

>[!IMPORTANT]
>
>Met dit gegevenselement kunt u cookies instellen en door de gebruiker gegenereerde waarden in cookies opslaan. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getPreviousValue` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html) instellen en configureren. Het gegevenselement `getPreviousValue` stelt een variabele in op een waarde die bij een vorige hit is ingesteld.

Het gegevenselement `getPreviousValue` gebruikt de volgende argumenten:

* `v` (tekenreeks, vereist): De variabele met de waarde die u wilt doorgeven aan de volgende afbeeldingsaanvraag. Een veelgebruikte variabele is `s.pageName` om de vorige paginawaarde op te halen.
* `c` (tekenreeks, optioneel): de naam van het cookie waarin de waarde wordt opgeslagen.  Als dit argument niet is ingesteld, wordt standaard ingesteld op `"s_gpv"` .

Wanneer u dit gegevenselement aanroept, wordt de tekenreekswaarde in het cookie geretourneerd. De insteekmodule stelt vervolgens de vervaldatum van het cookie opnieuw in en wijst hieraan de variabelewaarde toe vanuit het argument `v` . Het cookie verloopt na 30 minuten inactiviteit.

### `getQueryParam`

Hiermee kunt u de [`getQueryParam` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html) instellen en configureren. Het gegevenselement `getQueryParam` extraheert de waarde van elke querytekenreeksparameter in een URL. Het is nuttig om campagnecodes, zowel intern als extern, uit het landen van pagina URLs te halen. Het is ook nuttig wanneer het halen van onderzoekstermijnen of andere parameters van het vraagkoord. Dit gegevenselement verstrekt robuuste eigenschappen in het ontleden van complexe URLs, met inbegrip van knoeiboel en URLs die veelvoudige parameters van het vraagkoord bevatten.

Het gegevenselement `getQueryParam` gebruikt de volgende argumenten:

* `qsp` (vereist): een door komma&#39;s gescheiden lijst met querytekenreeksparameters die moet worden gezocht binnen de URL. Het is niet hoofdlettergevoelig.
* `de` (optioneel): Het scheidingsteken dat moet worden gebruikt wanneer meerdere parameters van de queryreeks overeenkomen. Heeft als standaardwaarde een lege tekenreeks.
* `url` (optioneel): Een aangepaste URL, tekenreeks of variabele waaruit de parameterwaarden voor de queryreeks moeten worden geëxtraheerd. Wordt standaard ingesteld op `window.location` .

Wanneer dit gegevenselement wordt aangeroepen, wordt een waarde geretourneerd die afhankelijk is van de bovenstaande argumenten en de URL:

* Wanneer geen overeenkomende parameter voor een querytekenreeks wordt gevonden, retourneert de methode een lege tekenreeks.
* Wanneer een overeenkomende parameter voor een querytekenreeks wordt gevonden, retourneert de methode de parameterwaarde voor de queryreeks.
* Als een overeenkomende parameter voor een querytekenreeks wordt gevonden maar de waarde leeg is, retourneert de methode `true` .
* Wanneer meerdere overeenkomende parameters voor queryreeksen worden gevonden, retourneert de methode een tekenreeks met elke parameterwaarde die door de tekenreeks in het argument `de` wordt gescheiden.

### `getTimeParting`

Hiermee kunt u de [`getTimeParting` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html) instellen en configureren. In het gegevenselement `getTimeParting` worden de details vastgelegd van het tijdstip waarop een meetbare activiteit op uw site plaatsvindt. Dit gegevenselement is waardevol wanneer u metriek door om het even welke herhaalbare verdeling van tijd over een bepaalde datumwaaier wilt breken. U kunt bijvoorbeeld de conversiekoersen vergelijken tussen twee verschillende dagen van de week, zoals alle zondag en alle donderdag. U kunt periodes van de dag ook vergelijken, zoals alle ochtenden tegenover alle avonden.

Het gegevenselement `getTimeParting` gebruikt het volgende argument:

`t` (Optioneel maar aanbevolen, tekenreeks): de naam van de tijdzone waarnaar de lokale tijd van de bezoeker moet worden omgezet.  Wordt standaard ingesteld op UTC/GMT. Verwijs naar de [ Lijst van TZ de tijdstreken van de gegevensbestandtijd ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) op Wikipedia voor een volledige lijst van geldige waarden.

Veelvoorkomende geldige waarden zijn:

* `"America/New_York"` for Eastern Time
* `"America/Chicago"` voor Central Time
* `"America/Denver"` voor Mountain Time
* `"America/Los_Angeles"` voor Pacific Time

Het roepen van dit gegevenselement keert een koord terug dat het volgende door een pijp (`|`) wordt afgebakend:

* Het lopende jaar
* De huidige maand
* De dag van de maand
* De dag van de week
* De huidige tijd (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Met dit gegevenselement worden cookies ingesteld. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getTimeSinceLastVisit` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html) instellen en configureren. Het gegevenselement `getTimeSinceLastVisit` houdt in hoelang een bezoeker heeft geduurd om na zijn laatste bezoek terug te keren naar uw site.

Het gegevenselement `getTimeSinceLastVisit` gebruikt geen argumenten. Het retourneert de hoeveelheid tijd die is verstreken sinds de bezoeker voor het laatst naar de site is gekomen. Deze tijd wordt als volgt geplakt:

* De tijd tussen 30 minuten en een uur sinds het laatste bezoek is ingesteld op de dichtstbijzijnde halftijdse benchmark. Bijvoorbeeld `"30.5 minutes"` , `"53 minutes"`
* De tijd tussen een uur en een dag wordt afgerond aan de dichtstbijzijnde benchmark van kwartier. Bijvoorbeeld `"2.25 hours"` , `"7.5 hours"`
* Tijd langer dan een dag wordt afgerond naar de dichtstbijzijnde dagbenchmark. Bijvoorbeeld `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Als een bezoeker niet eerder heeft bezocht of de verstreken tijd langer is dan twee jaar, wordt de waarde ingesteld op `"New Visitor"` .

### `getValOnce`

>[!IMPORTANT]
>
>Met dit gegevenselement kunt u cookies instellen en door de gebruiker gegenereerde waarden in cookies opslaan. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getValOnce` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html) instellen en configureren. Met het gegevenselement `getValOnce` voorkomt u dat een variabele meerdere keren op dezelfde waarde wordt ingesteld.

Het gegevenselement `getValOnce` gebruikt de volgende argumenten:

* `vtc` (required, string): De variabele die gecontroleerd moet worden en controleert of deze eerder op een identieke waarde was ingesteld
* `cn` (optioneel, tekenreeks): de naam van het cookie dat de te controleren waarde bevat. Heeft als standaardwaarde `"s_gvo"`
* `et` (optioneel, geheel getal): De vervaldatum van de cookie in dagen (of minuten, afhankelijk van het argument `ep` ). De standaardwaarde is `0` , die aan het einde van de browsersessie vervalt.
* `ep` (optioneel, tekenreeks): stel dit argument alleen in als het argument `et` ook is ingesteld. Stel dit argument in op `"m"` als u het argument `et` in minuten in plaats van dagen wilt laten verlopen. De standaardwaarde is `"d"` , die het argument `et` instelt in dagen.

Wanneer het argument `vtc` en de waarde van het cookie overeenkomen, retourneert deze methode een lege tekenreeks. Wanneer het argument `vtc` en de waarde van het cookie niet overeenkomen, retourneert de methode het argument `vtc` als een tekenreeks.

### `getVisitDuration`

>[!IMPORTANT]
>
>Met dit gegevenselement worden cookies ingesteld. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getVisitDuration` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html) instellen en configureren. Het gegevenselement `getVisitDuration` houdt de hoeveelheid tijd in minuten bij die de bezoeker tot dat punt op de site is geweest.

Het gegevenselement `getVisitDuration` gebruikt geen argumenten. Deze geeft een van de volgende waarden:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (waarbij `[x]` het aantal minuten is dat is verstreken sinds de bezoeker de site heeft aangeland)

### `getVisitNum`

>[!IMPORTANT]
>
>Met dit gegevenselement worden cookies ingesteld. Raadpleeg de specifieke documentatie van de plug-in voor meer informatie.

Hiermee kunt u de [`getVisitNum` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html) instellen en configureren. Het gegevenselement `getVisitNum` retourneert het bezoeknummer voor alle bezoekers die binnen het gewenste aantal dagen naar de site komen.

Het gegevenselement `getVisitNum` gebruikt de volgende argumenten:

* `rp` (optioneel, geheel getal OF tekenreeks): Het aantal dagen voordat de teller van het bezoeknummer opnieuw wordt ingesteld.  Wordt standaard ingesteld op `365` wanneer niet ingesteld.
   * Wanneer dit argument `"w"` is, wordt de teller aan het einde van de week opnieuw ingesteld (deze zaterdag om 23:59 uur)
   * Wanneer dit argument `"m"` is, wordt de teller aan het einde van de maand (de laatste dag van deze maand) opnieuw ingesteld
   * Wanneer dit argument `"y"` is, wordt de teller aan het einde van het jaar opnieuw ingesteld (31 december)
* `erp` (optioneel, Boolean): Wanneer het argument `rp` een getal is, bepaalt dit argument of de vervaldatum van het bezoeknummer moet worden verlengd. Als deze optie is ingesteld op `true` , worden bij volgende treffers naar uw site de teller van het bezoeknummer opnieuw ingesteld. Indien ingesteld op `false` , worden volgende treffers voor uw site niet uitgebreid wanneer de teller van het bezoeknummer opnieuw wordt ingesteld. Wordt standaard ingesteld op `true` . Dit argument is niet geldig wanneer het argument `rp` een tekenreeks is.

Het aantal bezoekers neemt toe wanneer de bezoeker na 30 minuten inactiviteit terugkeert naar uw site. Als deze methode wordt aangeroepen, wordt een geheel getal geretourneerd dat het huidige bezoeknummer van de bezoeker vertegenwoordigt.

### `p_fo` (Alleen pagina eerst)

Hiermee kunt u de [`p_fo` plug-in Analytics ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html) instellen en configureren. Het gegevenselement `p_fo` is een hulpprogramma dat controleert of een specifiek JavaScript-object bestaat. Als het object niet bestaat, maakt de plug-in het object en wordt `true` geretourneerd. Als het JavaScript-object al op de pagina aanwezig is, wordt `false` geretourneerd. Dit gegevenselement is nuttig om code precies één keer op een pagina uit te voeren.

Het gegevenselement `p_fo` gebruikt de volgende argumenten:

* `on` (required, string): De naam van het JavaScript-object dat het data-element maakt als het object nog niet bestaat op de pagina.

Wanneer het object nog niet bestaat, retourneert deze methode `true` en wordt het object gemaakt. Wanneer het object al bestaat, retourneert deze methode `false` .
