---
title: Opmerkingen bij de release Adobe Analytics Extension
description: De meest recente release bevat informatie over de Adobe Analytics-tagextensie in Adobe Experience Platform.
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: cc04a40b2fb649511950ed80af7028a19154dcdd
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 5%

---

# Opmerkingen bij de release Adobe Analytics-extensie

Hieronder volgt een lijst met releaseopmerkingen voor de Adobe Analytics-tagextensie.

>[!NOTE]
>
>De extensie van de tag Analytics indien vaak bijgewerkt als reactie op updates van de [JavaScript-bibliotheek voor meting van app](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html). Zie de [Opmerkingen bij de release AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html) voor meer informatie over de hieronder vermelde specifieke versies.

## 23 september 2022

**Adobe Analytics Extension 1.9.1**

**Functies**:

* Bijgewerkt naar AppMeasurement v2.23.0.
* De extensie kan nu hoge entropie verzamelen [gebruiker-agent cliëntwenken](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints) zoals ondersteund door de nieuwste versie van AppMeasurement.

## 28 februari 2022

**Adobe Analytics Extension 1.9.0**

**Bugfixes**:

* Enkele foutopsporingsinstructies zijn verwijderd uit AppMeturement.

## 29 november 2021

**Adobe Analytics Extension 1.8.8**

**Bugfixes**:

* Bijgewerkte AppMeasurement naar v2.22.3.

## 16 september 2021

**Adobe Analytics Extension 1.8.7**

**Bugfixes**:

* Bijgewerkte AppMeasurement naar v2.2.2.2.
* Verwijderd afgekeurd buildInfo.environment

## 24 augustus 2021

**Adobe Analytics Extension 1.8.6**

**Bugfixes**:

* Bijgewerkt [AppMeasurement naar v2.22.1](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html).
* Bijgewerkte fallback linkName om logica van de Activity Map te weerspiegelen in plaats van innerHTML te gebruiken.

## 6 augustus 2020

**Adobe Analytics Extension 1.8.5**

**Bugfixes**:

* De onjuiste cookienaam in de instellingen van de AAM module werd ingesteld toen dit veld leeg bleef. Dit is nu gecorrigeerd.

**Functies**:

* Bijgewerkt [AppMeasurement tot 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html).
* De kleine verandering UI zodat het extra plaatsen nu samengevouwen in een accordeon in plaats van checkbox verschijnt.

## 2 juni 2020

**Adobe Analytics Extension 1.8.4**

**Bugfixes**:

* Probleem verholpen waarbij de winkelwagengebeurtenissen (prodView, scAdd, scView, enz.) niet werden weergegeven tijdens de vervolgkeuzelijst met gebeurtenissen. Al deze moeten nu selecteerbaar zijn in het vervolgkeuzemenu.

**Functies**:

* U kunt de activiteitenkaart in de uitbreiding nu uitzetten zonder het moeten douanecode gebruiken. De activiteitenkaart laadt als een afzonderlijke module (ongeveer zoals de AAM module) en u kunt het uitzetten als u wilt.
* De interface is verbeterd door hiërarchische variabelen en andere opties te minimaliseren.
* Er is een veld toegevoegd waarin u aankoop-id&#39;s kunt instellen via de interface voor extensieconfiguratie.

## 10 maart 2020

**Adobe Analytics Extension 1.8.3**

**Bugfixes**:

* Oplossing van een bug die de regelconfiguratie beïnvloedde die een fout zou werpen wanneer u probeerde om variabelen te plaatsen als u een douanebibliotheek gebruikte en uw rapportsuites niet in Analytics werden gevormd.
* Bij het maken van een eVar was er een fout die u niet de optie zou geven om te &#39;dupliceren van&#39; een proxy of andersom. Dit is nu opgelost om het gedrag in vorige versies te weerspiegelen.

**Functies**:

* Bijgewerkt [AppMeasurement tot 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)

## 2 maart 2020

**Adobe Analytics Extension 1.8.2**

**Bugfixes**:

* Probleem verholpen waarbij de onjuiste syntaxis werd gebruikt voor numerieke gebeurtenissen en geserialiseerde valuta

**Functies**:

* Bijgewerkt [AppMeasurement naar 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)
* De DIL-bibliotheek in de module Audience Manager is bijgewerkt naar 9.4
* De lengte van invoervelden in de extensie vergroten
* Vars en props in de extensie- en actieconfiguraties geven nu de vriendelijke naam van Analytics weer
* Selectievakje toegevoegd in de sectie &#39;Cookies&#39; van de extensieconfiguratie waarmee u beveiligde cookies kunt schrijven
* Drie nieuwe configuraties aan de module van de Audience Manager toegevoegd. Een instelling toegevoegd voor het inschakelen van logbestanden, voor het inschakelen van URL-doelen en voor het inschakelen van cookie-doelen

## 13 november 2019

**Adobe Analytics Extension 1.8.1**

**Bugfixes**:

* Probleem verholpen waarbij premiumgebeurtenissen en -props niet konden worden opgeslagen.

## 1 november 2019

**Adobe Analytics Extension 1.8.0**

**Bugfixes**:

* Probleem verholpen waarbij een klein aantal klanten de opties van de rapportsuite in de vervolgkeuzelijst niet kon zien
* Probleem verholpen waarbij bepaalde variabelen niet correct werden ingesteld bij gebruik van ECID

**Functies**:

* Hiermee sorteert u gebeurtenissen, regeleinden en gebeurtenissen numeriek in de weergave Extensie
* Wijzigingen in het achtergrondschema aangebracht ter ondersteuning van Magento-contextgegevens

## 6 september 2019

**Adobe Analytics Extension 1.7.8**

**Bugfixes**:

* Probleem verholpen waarbij sommige gebruikers de opties van de rapportsuite niet zagen in de vervolgkeuzelijst
* Probleem verholpen waarbij gebeurtenissen niet correct werden geactiveerd

## 5 september 2019

**Adobe Analytics Extension 1.7.7**

**Functies**:

* Bijgewerkte AppMeasurement aan 2.17
* Bijgewerkte module van het Beheer van het Publiek om DIL 9.3 te steunen
* Bijgewerkte veldbreedten voor meer ruimte

**Bugfixes**:

* Het probleem met de instelling opt-in/opt-out is opgelost.
* Probleem verholpen waarbij variabelen niet correct werden ingesteld bij gebruik van ECID

## 18 juli 2019

**Adobe Analytics Extension 1.7.6**

**Functies**:

* De Adobe Analytics-extensie is bijgewerkt om DIL 9.2 voor Audience Manager te ondersteunen

* Bijgewerkte extensie voor ondersteuning [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0)
* Het volgende selectievakje is verwijderd omdat het niet meer wordt ondersteund: &quot;Koppel de IFRAME voor het publiceren van de bestemming niet aan de DOM- of branddoelen&quot;

## 4 juni 2019

**Adobe Analytics Extension 1.7.5**

**Functies**:

* De Adobe Analytics-extensie is bijgewerkt naar [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=en#version-2.14.0) dat een oplossing bevat voor een bekende clearVars-kwestie
* Een Exchange-koppeling toegevoegd aan de extensie. De Exchange-lijst kan worden bereikt door het vervolgkeuzemenu te selecteren en &#39;&#39;extensie info&#39;&#39; te kiezen

**Bugfixes**:

* Probleem verholpen in de interface die het onjuiste eval liet zien dat uit een lijst werd geschrapt
* Oplossing voor een probleem waarvoor een SSL-traceringsserver nodig was toen u meerdere rapportsuites probeerde toe te voegen. Wanneer u meerdere rapportsuites toevoegt, is een trackingserver vereist, maar is het veld SSL-tracking-server optioneel.

## 15 april 2019

**Adobe Analytics Extension 1.7.4**

**Bugfixes**:

* Gerolde extensie terug nadat een bug is gevonden in appMeasurement 2.13.0. appMeasurement 2.13.0 veroorzaakte een probleem dat de ECID niet verstuurde. Als u 1.7.3 installeerde, raden we u aan een upgrade naar 1.7.4 uit te voeren om dit probleem te voorkomen. De clearVars wordt uitgevoerd totdat een bijgewerkte versie van appMeasurement wordt uitgebracht.

## 12 april 2019

**Adobe Analytics Extension 1.7.3**

**Bugfixes**:

* De Adobe Analytics-extensie is bijgewerkt naar appMeasurement 2.13.0 en bevat een correctie voor een bekend clearVars-probleem.

## 21 maart 2019

**Adobe Analytics Extension 1.7.2**

**Functies**:

* De Adobe Analytics-extensie is bijgewerkt naar DIL 9.1.
* De Adobe Analytics-extensie is bijgewerkt naar appMeasurement 2.12.
* De Adobe Analytics-extensieweergave is bijgewerkt naar React Spectrum.
* Wanneer het vormen van uw rapportsuites in de configuratiepagina zult u nu een dropdown aan alle rapportsuites in uw bedrijf zien om het voor u gemakkelijker te maken om de aangewezen rapportreeks te selecteren.

## 7 maart 2019

**Adobe Analytics Extension 1.7.1**

**Bugfixes**:

* De extensie werd teruggedraaid naar versie 1.6 nadat een bug in versie 1.7 werd gevonden.

## 11 februari 2019

**Adobe Analytics Extension 1.6**

**Functies**:

* De Adobe Analytics-extensie voor DIL 9.0 is bijgewerkt en biedt nu ondersteuning voor opt-in.
* De Adobe Analytics-extensie voor AppMeasurement 2.11 is bijgewerkt om de opt-in te ondersteunen.

**Bugfixes**:

* Oplossing voor een conflict met Prototype JS. De extensie Analytics ondersteunt nu standaard prototype.js-bibliotheken.

## 9 november 2018

**Adobe Analytics Extension 1.5.1**

**Bugfixes**:

* De DIL-module is gedowngraded naar 7.0 om een probleem op te lossen dat problemen veroorzaakte met analysatiebakens die niet werden geactiveerd

## 5 november 2018

**Adobe Analytics Extension 1.5**

**Functies**:

* De Adobe Analytics-extensie is bijgewerkt om DIL 8.0 in Audience Manager te ondersteunen
* Scheidte het veld &quot;Serialize from value&quot; in twee velden, &quot;Event ID&quot; en &quot;Event Value&quot;. Hiermee wordt het probleem verholpen dat een waarde toewijst in plaats van een gebeurtenis met serienummering te coderen
   * Opmerking: als u het huidige veld gebruikt om een id toe te voegen met een tekenreeks (bijvoorbeeld Event7=3:abc123) u zult uw input moeten bijwerken om identiteitskaart op het gebied van de &quot;identiteitskaart van de Gebeurtenis&quot;te weerspiegelen

**Bugfixes**:

* Probleem verholpen waarbij de valutacode niet correct kon worden gevuld

## 11 oktober 2018

**Adobe Analytics Extension 1.4**

**Functies**:

* De naam van het volgende cookie is gemigreerd naar de extensieconfiguratie.

**Bugfixes**:

* Probleem verholpen, zodat ingestelde variabelen niet vastlopen wanneer geen trackerProperties-object beschikbaar is.

## 5 juni 2018

**Adobe Analytics Extension 1.3**

**Functies**:

* Bijgewerkte Adobe Analytics-extensie voor ondersteuning van AppMeasurement 2.9.
* De functie &#39;Tracker globaal toegankelijk maken&#39; in de Adobe Analytics-extensie is toegevoegd, waardoor de tracker wereldwijd onder het bereik van `windows.s`.

**Bugfixes**:

* Het probleem waarbij de lijstweergave werd hersteld bij het terugkeren vanuit de detailweergave, is opgelost.
* Enkele fouten verholpen om het laden van bronnen in de revisiekiezer te verbeteren
* Probleem verholpen waarbij meerdere regels s.events overschrijvingen in de Adobe Analytics-extensie

## 20 maart 2018

**Adobe Analytics Extension 1.2**

**Functies**:

* Werkt AppMeasurement.js tot 2.8.0 bij
* Voegt steun voor server-kant door:sturen toe

## 8 februari 2018

**Adobe Analytics Extension 1.1**

**Functies**:

* AppMeasurement is bijgewerkt naar versie 2.6
* De geïnitialiseerde analysecontracker wordt nu weergegeven via een gedeelde module in de Adobe Experience Platform-tagextensie, zodat andere extensies code kunnen bevatten om ermee te werken.

**Bugfixes**:

* Correctie van een fout in de Adobe Analytics-extensie die ervoor zorgde dat &quot;Fout, ontbrekende ID van rapportsuite in initialisatie van AppMeasurement&quot; werd weergegeven in de browserconsole.
