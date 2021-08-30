---
title: Reactor-API
description: Met de Reactor-API kunnen ontwikkelaars programmatisch alle bronnen voor tags in Adobe Experience Platform beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 0%

---

# [!DNL Reactor] API-handleiding

De Reactor-API bevat verschillende eindpunten waarmee u programmatisch alle bronnen voor tags in Adobe Experience Platform kunt beheren.

Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over het verifiëren van de API.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de [Reactor-API-referentie](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Bedrijven

Een bedrijf vertegenwoordigt de organisatie van een markeringsgebruiker, typisch een zaken. Deze bedrijven komen overeen met 1:1 met IMS Organisatie-id&#39;s. API-gebruikers hebben alleen zichtbaarheid in de bedrijven waartoe zij toegang hebben.

Zie [bedrijfseindgids](./endpoints/companies.md) om te leren hoe te om beschikbare bedrijven in API te bekijken.

## Properties

Een eigenschap is een container die de meeste andere bronnen bevat die beschikbaar zijn in de Reactor-API. De enige middelen die niet in het bezit zijn van een bezit zijn controlegebeurtenissen, bedrijven, uitbreidingspakketten, en profielen. Een bezit behoort tot precies één bedrijf, en een bedrijf kan vele eigenschappen hebben.

Zie [eigenschappen eindpuntgids](./endpoints/properties.md) om te leren hoe te om eigenschappen in API te beheren.

## Gegevenselementen

Een gegevenselement werkt als een variabele die naar een belangrijk stuk gegevens binnen uw toepassing verwijst. De elementen van gegevens worden gebruikt binnen regels en uitbreidingsconfiguraties. Wanneer de regel wordt geactiveerd bij uitvoering in een browser of toepassing, wordt de waarde van het gegevenselement opgelost en gebruikt binnen de regel.

Zie [de eindgids van gegevenselementen ](./endpoints/data-elements.md) leren hoe te om gegevenselementen in API te beheren.

## Regels

De regels controleren het gedrag van de middelen in een opgestelde bibliotheek. Een regel is een groep van één of meerdere regelcomponenten, en bestaat om de regelcomponenten samen op een logische manier te binden.

Zie [regels eindpuntgids](./endpoints/rules.md) leren hoe te om regels in API te beheren.

## Regelcomponenten

De componenten van de regel zijn de individuele punten die omhoog een regel maken. Regelcomponenten hebben drie basistypen:

* **Gebeurtenissen**: Wat een regel activeert
* **Voorwaarden**: Wat de regel controleert om een actie te bepalen
* **Handelingen**: Wat de regel uitvoert afhankelijk van of aan de voorwaarde wordt voldaan

Zie [regels eindpuntgids](./endpoints/rules.md) leren hoe te om regels in API te beheren.

## Extensiepakketten

Een extensiepakket bestaat uit een groep afzonderlijke mogelijkheden die aan een taggebruiker beschikbaar kunnen worden gesteld. Het meest meestal komen deze mogelijkheden in de vorm van regelcomponenten en gegevenselementen, maar kunnen ook belangrijkste modules en gedeelde modules omvatten. De mogelijkheden van een extensiepakket worden geïnstalleerd als een extensie wanneer deze in een bibliotheek wordt opgenomen.

Zie [de gids van het uitbreidingspakketeindpunt ](./endpoints/extension-packages.md) leren hoe te om uitbreidingspakketten in API te beheren.

## Extensies

Een extensie vertegenwoordigt de geïnstalleerde instantie van een extensiepakket. Met een extensie worden de functies die door een extensiepakket worden gedefinieerd, beschikbaar gemaakt voor een eigenschap. Deze functies worden gebruikt bij het maken van gegevenselementen en regelcomponenten.

Zie [de gids van het uitbreidingseindpunt ](./endpoints/extensions.md) om te leren hoe te om uitbreidingen in API te beheren.

## Bibliotheken

Een bibliotheek is een inzameling van middelen (uitbreidingen, regels, en gegevenselementen) die het gewenste gedrag van een bezit vertegenwoordigen. Bibliotheken worden gecompileerd in builds, en die bouwstijlen worden toegewezen aan verschillende milieu&#39;s aangezien zij neer de het publiceren stroom van het testen aan productie bewegen.

Zie [bibliotheekeindpuntgids](./endpoints/libraries.md) leren hoe te om bibliotheken in API te beheren.

## Builds

Een markeringsbibliotheek wordt gecompileerd in een bouwstijl zodat het aan een milieu voor het testen en plaatsing wordt toegewezen. De inhoud van een bouwstijl varieert afhankelijk van de middelen inbegrepen in de bibliotheek, de configuratie van het milieu waaraan de bouwstijl wordt toegewezen, en het platform van het bezit dat de bouwstijl tot behoort.

Zie [bouwt eindpuntgids](./endpoints/builds.md) om te leren hoe te om bouwstijlen in API te beheren.

## Omgevingen

Een milieu wijst op de specifieke gastheer waar een bouwstijl kan worden opgesteld, en of de bouwstijl als reeks dossiers zou moeten worden opgesteld of in een archiefformaat gecomprimeerd. In Reactor API, zijn de milieu&#39;s gescheiden van gastheren zelf, die door het `/hosts` eindpunt worden beheerd.

Zie [bouwt eindpuntgids](./endpoints/builds.md) om te leren hoe te om bouwstijlen in API te beheren.

## Gastheren

Een gastheer vertegenwoordigt een ontvangen bestemming waar een bibliotheek kan worden geleverd en uiteindelijk worden opgesteld bouwt. Gastheren kunnen Akamai- of SFTP-servers zijn.

Zie [de gids van het gastheereindpunt](./endpoints/hosts.md) leren hoe te om gastheren in API te beheren.

## App-configuraties

Met toepassingsconfiguraties kunnen referenties worden opgeslagen en opgehaald voor later gebruik. Zie de [handleiding voor het eindpunt van toepassingsconfiguraties](./endpoints/app-configurations.md) voor informatie over het beheren van toepassingsconfiguraties in de API.

## Gebeurtenissen van Audit

Een auditgebeurtenis is een record van een specifieke wijziging in een andere tagbron die wordt gegenereerd op het moment dat de wijziging wordt aangebracht. Dit zijn systeemgebeurtenissen waarop kan worden geabonneerd door het gebruik van een callback functie.

Zie [audit gebeurtenissen eindgids](./endpoints/audit-events.md) leren hoe te om controlegebeurtenissen in API te beheren.

## Callbacks

Een callback is een bericht dat het Platform naar een gastheer URL verzendt wanneer een nieuwe controlegebeurtenis wordt geproduceerd. Zie [callbacks eindpuntgids](./endpoints/callbacks.md) leren hoe te om callbacks in API te beheren.

## Notities

Notities zijn tekstuele annotaties die u aan bepaalde tagbronnen kunt toevoegen, zoals gegevenselementen, extensies, bibliotheken, eigenschappen, regels en regelcomponenten. Zie [Notitie eindpuntgids](./endpoints/notes.md) om te leren hoe te om nota&#39;s in API te beheren.

## Profiel

Een profiel bevat alle informatie over de aangemelde gebruiker, met inbegrip van alle Adobe Orgs waartot zij behoren, de productprofielen zij tot binnen elk Org behoren, en de rechten die zij van elk productprofiel hebben.

Zie [profiel eindpuntgids](./endpoints/profile.md) om te leren hoe te om deze informatie in API te bekijken.

## Zoeken

Het `/search` eindpunt verstrekt een manier om middelen te vinden die een gewenste die criteria aanpassen, als vraag wordt uitgedrukt. Alle vragen zijn scoped aan uw huidige bedrijf en toegankelijke eigenschappen. Zie [zoekeindpuntgids](./endpoints/search.md) om te leren hoe gebruik deze functionaliteit.

## Volgende stappen

Begin makend vraag gebruikend de Registratie API van het Schema, lees [begonnen gids](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
