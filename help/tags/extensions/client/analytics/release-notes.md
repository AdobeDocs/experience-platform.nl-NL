---
title: Opmerkingen bij de release Adobe Analytics Extension
description: De meest recente release bevat informatie over de Adobe Analytics-tagextensie in Adobe Experience Platform.
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: c783906b20db2b86d58aea7b3a94bde007c0a465
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 1%

---

# Opmerkingen bij de release Adobe Analytics-extensie

Hieronder volgt een lijst met releaseopmerkingen voor de Adobe Analytics-tagextensie.

>[!NOTE]
>
>De de markeringsuitbreiding van de Analyse als vaak bijgewerkt in antwoord op updates aan de [ bibliotheek van JavaScript van het AppMeasurement ](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html). Verwijs naar de [ nota&#39;s van de de versieversie van het AppMeasurement ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html) voor details op de specifieke hieronder vermelde versies.

## dinsdag 12 augustus 2024

**Uitbreiding 1.9.5 van Adobe Analytics**

**Eigenschappen**:

* Geüpgraded aan [ AppMeasurement aan v2.27.0 ](https://github.com/adobe/appmeasurement/releases/tag/v2.27.0).

## dinsdag 4 maart 2024

**Uitbreiding 1.9.4 van Adobe Analytics**

**Eigenschappen**:

* Geüpgraded aan [ AppMeasurement aan v2.26.0 ](https://github.com/adobe/appmeasurement/releases/tag/v2.26.0).

## 15 september 2023

**Uitbreiding 1.9.3 van Adobe Analytics**

**Eigenschappen**:

* Geüpgraded aan [ AppMeasurement aan v2.25.0 ](https://github.com/adobe/appmeasurement/releases/tag/v2.25.0).


## donderdag 19 juli 2023

**Uitbreiding 1.9.2 van Adobe Analytics**

**Eigenschappen**:

* Geüpgraded aan [ AppMeasurement v2.24.0 ](https://github.com/adobe/appmeasurement/releases/tag/v2.24.0).
* Er is een optionele configuratie toegevoegd (`decodeLinkParameters` default `false` ) die URL&#39;s met dubbele byte gecodeerde tekens decodeert.

**Bugfixes**:

* Toegevoegde extra fout behandeling voor browsers met gebrek high-entropy [ gebruiker-Agent cliëntwenken ](https://experienceleague.adobe.com/docs/analytics/technotes/client-hints.html) API&#39;s.
* Veranderde [ POST ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) inhoud-Type kopbal aan gebruik `x-www-form-urlencoded` door gebrek.

## 23 september 2022

**Uitbreiding 1.9.1 van Adobe Analytics**

**Eigenschappen**:

* Bijgewerkt naar AppMeasurement v2.23.0.
* De uitbreiding kan high-entropy [ gebruiker-agent cliëntwenken ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints) nu verzamelen zoals gesteund door de recentste versie van AppMeasurement.

## 28 februari 2022

**Uitbreiding 1.9.0 van Adobe Analytics**

**Bugfixes**:

* Enkele foutopsporingsinstructies in het AppMeasurement zijn verwijderd.

## 29 november 2021

**Uitbreiding 1.8.8 van Adobe Analytics**

**Bugfixes**:

* Bijgewerkt AppMeasurement naar v2.2.3.

## 16 september 2021

**Uitbreiding 1.8.7 van Adobe Analytics**

**Bugfixes**:

* Bijgewerkt AppMeasurement naar v2.2.2.2.
* Vervangen buildInfo.environment is verwijderd

## woensdag 24 augustus 2021

**Uitbreiding 1.8.6 van Adobe Analytics**

**Bugfixes**:

* Bevorderde [ AppMeasurement aan v2.22.1 ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html).
* Bijgewerkte fallback linkName om logica van de Activity Map te weerspiegelen in plaats van innerHTML te gebruiken.

## vrijdag 6 augustus 2020

**Uitbreiding 1.8.5 van Adobe Analytics**

**Bugfixes**:

* De onjuiste cookienaam in de instellingen van de AAM module werd ingesteld toen dit veld leeg bleef. Dit is nu gecorrigeerd.

**Eigenschappen**:

* Bijgewerkt [ AppMeasurement aan 2.22.0 ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html).
* De kleine verandering UI zodat het extra plaatsen nu samengevouwen in een accordeon in plaats van checkbox verschijnt.

## woensdag 2 juni 2020

**Uitbreiding 1.8.4 van Adobe Analytics**

**Bugfixes**:

* Probleem verholpen waarbij de winkelwagengebeurtenissen (prodView, scAdd, scView, enz.) niet werden weergegeven tijdens de vervolgkeuzelijst met gebeurtenissen. Al deze moeten nu selecteerbaar zijn in de vervolgkeuzelijst.

**Eigenschappen**:

* U kunt de activiteitenkaart in de uitbreiding nu uitzetten zonder het moeten douanecode gebruiken. De activiteitenkaart laadt als een afzonderlijke module (ongeveer zoals de AAM module) en u kunt het uitzetten als u wilt.
* De interface is verbeterd door hiërarchische variabelen en andere opties te minimaliseren.
* Er is een veld toegevoegd waarin u aankoop-id&#39;s kunt instellen via de interface voor extensieconfiguratie.

## woensdag 10 maart 2020

**Uitbreiding 1.8.3 van Adobe Analytics**

**Bugfixes**:

* Oplossing van een bug die de regelconfiguratie beïnvloedde die een fout zou werpen wanneer u probeerde om variabelen te plaatsen als u een douanebibliotheek gebruikte en uw rapportsuites niet in Analytics werden gevormd.
* Bij het maken van een eVar was er een fout die u niet de optie zou geven om te &#39;dupliceren van&#39; een proxy of andersom. Dit is nu opgelost om het gedrag in vorige versies te weerspiegelen.

**Eigenschappen**:

* Bijgewerkt [ AppMeasurement aan 2.20.0 ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)

## dinsdag 2 maart 2020

**Uitbreiding 1.8.2 van Adobe Analytics**

**Bugfixes**:

* Probleem verholpen waarbij de onjuiste syntaxis werd gebruikt voor numerieke gebeurtenissen en geserialiseerde valuta

**Eigenschappen**:

* Bijgewerkt [ AppMeasurement aan 2.18.0 ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)
* De DIL-bibliotheek in de module Audience Manager is bijgewerkt naar 9.4
* De lengte van invoervelden in de extensie vergroten
* Vars en props in de extensie- en actieconfiguraties geven nu de vriendelijke naam van Analytics weer
* Selectievakje toegevoegd in de sectie &#39;Cookies&#39; van de extensieconfiguratie waarmee u beveiligde cookies kunt schrijven
* Drie nieuwe configuraties aan de module van de Audience Manager toegevoegd. Een instelling toegevoegd voor het inschakelen van logbestanden, voor het inschakelen van URL-doelen en voor het inschakelen van cookie-doelen

## 13 november 2019

**Uitbreiding 1.8.1 van Adobe Analytics**

**Bugfixes**:

* Probleem verholpen waarbij premiumgebeurtenissen en -props niet konden worden opgeslagen.

## 1 november 2019

**Uitbreiding 1.8.0 van Adobe Analytics**

**Bugfixes**:

* Probleem verholpen waarbij een klein aantal klanten de opties van de rapportsuite in de vervolgkeuzelijst niet kon zien
* Probleem verholpen waarbij bepaalde variabelen niet correct werden ingesteld bij gebruik van ECID

**Eigenschappen**:

* Hiermee sorteert u gebeurtenissen, regeleinden en gebeurtenissen numeriek in de weergave Extensie
* Wijzigingen in het achtergrondschema aangebracht ter ondersteuning van Magento-contextgegevens

## 6 september 2019

**Uitbreiding 1.7.8 van Adobe Analytics**

**Bugfixes**:

* Probleem verholpen waarbij sommige gebruikers de opties van de rapportsuite niet zagen in de vervolgkeuzelijst
* Probleem verholpen waarbij gebeurtenissen niet correct werden geactiveerd

## 5 september 2019

**Uitbreiding 1.7.7 van Adobe Analytics**

**Eigenschappen**:

* Bijgewerkt AppMeasurement naar 2.17
* Bijgewerkte module van het Beheer van het Publiek om DIL 9.3 te steunen
* Bijgewerkte veldbreedten voor meer ruimte

**Bugfixes**:

* Het probleem met de instelling opt-in/opt-out is opgelost.
* Probleem verholpen waarbij variabelen niet correct werden ingesteld bij gebruik van ECID

## vrijdag 18 juli 2019

**Uitbreiding 1.7.6 van Adobe Analytics**

**Eigenschappen**:

* De Adobe Analytics-extensie is bijgewerkt om DIL 9.2 voor Audience Manager te ondersteunen

* Bijgewerkte uitbreiding om [ AppMeasurement 2.15.0 te steunen ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0)
* Het volgende selectievakje is verwijderd, omdat het niet meer wordt ondersteund: &quot;Koppel het doel-publicatie-IFRAME niet aan de DOM- of branddoelen&quot;

## woensdag 4 juni 2019

**Uitbreiding 1.7.5 van Adobe Analytics**

**Eigenschappen**:

* Bijgewerkt de Uitbreiding van Adobe Analytics aan [ AppMeasurement 2.14.0 ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.14.0) die een moeilijke situatie aan een bekende clearVars kwestie omvat
* Een Exchange-koppeling toegevoegd aan de extensie. De Exchange-lijst kan worden bereikt door het vervolgkeuzemenu te selecteren en &quot;extensie info&quot; te kiezen

**Bugfixes**:

* Probleem verholpen in de interface die het onjuiste eval liet zien dat uit een lijst werd geschrapt
* Oplossing voor een probleem waarvoor een SSL-traceringsserver nodig was toen u meerdere rapportsuites probeerde toe te voegen. Wanneer u meerdere rapportsuites toevoegt, is een trackingserver vereist, maar is het veld SSL-tracking-server optioneel.

## dinsdag 15 april 2019

**Uitbreiding 1.7.4 van Adobe Analytics**

**Bugfixes**:

* De uitgerolde extensie is hersteld nadat een fout is gevonden in appMeasurement 2.13.0. appMeasurement 2.13.0 veroorzaakte een probleem dat de ECID niet verstuurde. Als u 1.7.3 hebt geïnstalleerd, raden we u aan te upgraden naar 1.7.4 om dit probleem te voorkomen. De clearVars wordt uitgevoerd totdat een bijgewerkte versie van appMeasurement wordt uitgebracht.

## zaterdag 12 april 2019

**Uitbreiding 1.7.3 van Adobe Analytics**

**Bugfixes**:

* De Adobe Analytics-extensie is bijgewerkt naar appMeasurement 2.13.0 en bevat een correctie voor een bekend clearVars-probleem.

## vrijdag 21 maart 2019

**Uitbreiding 1.7.2 van Adobe Analytics**

**Eigenschappen**:

* De Adobe Analytics-extensie is bijgewerkt naar DIL 9.1.
* De Adobe Analytics-extensie is bijgewerkt naar appMeasurement 2.12.
* De Adobe Analytics-extensieweergave is bijgewerkt naar React Spectrum.
* Wanneer het vormen van uw rapportsuites in de configuratiepagina zult u nu een dropdown aan alle rapportsuites in uw bedrijf zien om het voor u gemakkelijker te maken om de aangewezen rapportreeks te selecteren.

## vrijdag 7 maart 2019

**Uitbreiding 1.7.1 van Adobe Analytics**

**Bugfixes**:

* De extensie werd teruggedraaid naar versie 1.6 nadat een bug in versie 1.7 werd gevonden.

## 11 februari 2019

**Uitbreiding 1.6 van Adobe Analytics**

**Eigenschappen**:

* De Adobe Analytics-extensie voor DIL 9.0 is bijgewerkt en biedt nu ondersteuning voor opt-in.
* De Adobe Analytics-extensie voor AppMeasurement 2.11 is bijgewerkt om de opt-in te ondersteunen.

**Bugfixes**:

* Oplossing voor een conflict met Prototype JS. De extensie Analytics ondersteunt nu standaard prototype.js-bibliotheken.

## 9 november 2018

**Uitbreiding 1.5.1 van Adobe Analytics**

**Bugfixes**:

* De DIL-module is gedowngraded naar 7.0 om een probleem op te lossen dat problemen veroorzaakte met analysatiebakens die niet werden geactiveerd

## 5 november 2018

**Uitbreiding 1.5 van Adobe Analytics**

**Eigenschappen**:

* De Adobe Analytics-extensie is bijgewerkt om DIL 8.0 in Audience Manager te ondersteunen
* Scheidte het veld &quot;Serialize from value&quot; in twee velden, &quot;Event ID&quot; en &quot;Event Value&quot;. Hiermee wordt het probleem verholpen dat een waarde toewijst in plaats van een gebeurtenis met serienummering te coderen
   * Opmerking: als u het huidige veld gebruikt om een id toe te voegen met een tekenreeks (bijvoorbeeld Event7=3:abc123) u zult uw input moeten bijwerken om identiteitskaart op het gebied van &quot;Gebeurtenis identiteitskaart&quot;te weerspiegelen

**Bugfixes**:

* Probleem verholpen waarbij de valutacode niet correct kon worden gevuld

## vrijdag 11 oktober 2018

**Uitbreiding 1.4 van Adobe Analytics**

**Eigenschappen**:

* De naam van het volgende cookie is overgebracht naar de extensieconfiguratie.

**Bugfixes**:

* Probleem verholpen, zodat ingestelde variabelen niet vastlopen wanneer geen trackerProperties-object beschikbaar is.

## woensdag 5 juni 2018

**Uitbreiding 1.3 van Adobe Analytics**

**Eigenschappen**:

* Bijgewerkte Adobe Analytics-extensie ter ondersteuning van AppMeasurement 2.9.
* De functie &#39;Tracker globaal toegankelijk maken&#39; in de Adobe Analytics-extensie is toegevoegd, waardoor de tracker globaal onder `windows.s` kan worden geplaatst.

**Bugfixes**:

* Het probleem waarbij de lijstweergave werd hersteld bij het terugkeren vanuit de detailweergave, is opgelost.
* Enkele fouten verholpen om het laden van bronnen in de revisiekiezer te verbeteren
* Probleem verholpen waarbij meerdere regels s.events overschrijvingen in de Adobe Analytics-extensie

## woensdag 20 maart 2018

**Uitbreiding 1.2 van Adobe Analytics**

**Eigenschappen**:

* Updates AppMeasurement.js tot 2.8.0
* Voegt steun voor server-kant door:sturen toe

## 8 februari 2018

**Uitbreiding 1.1 van Adobe Analytics**

**Eigenschappen**:

* AppMeasurement is bijgewerkt naar versie 2.6
* De geïnitialiseerde analysecontracker wordt nu weergegeven via een gedeelde module in de Adobe Experience Platform-tagextensie, zodat andere extensies code kunnen bevatten om ermee te werken.

**Bugfixes**:

* Correctie van een fout in de extensie Adobe Analytics die ervoor zorgde dat &quot;Fout, ontbrekende ID van rapportsuite in initialisatie van AppMeasurement&quot; werd weergegeven in de browserconsole.
