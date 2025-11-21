---
title: Reactor-API
description: Met de Reactor-API kunnen ontwikkelaars programmatisch alle bronnen voor tags in Adobe Experience Platform beheren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 3%

---

# [!DNL Reactor] API-handleiding

De Reactor-API bevat verschillende eindpunten waarmee u programmatisch alle bronnen voor tags in Adobe Experience Platform kunt beheren.

Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor belangrijke informatie over hoe te om aan API voor authentiek te verklaren.

Om alle beschikbare eindpunten en verrichtingen te bekijken CRUD, bezoek de [&#x200B; Reactor API verwijzing &#x200B;](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Bedrijven

Een bedrijf vertegenwoordigt de organisatie van een markeringsgebruiker, typisch een zaken. Deze bedrijven passen 1 :1 met organisatie IDs aan. API-gebruikers hebben alleen zichtbaarheid in de bedrijven waartoe zij toegang hebben.

Zie de [&#x200B; gids van het bedrijfseindpunt &#x200B;](./endpoints/companies.md) leren hoe te om beschikbare bedrijven in API te bekijken.

## Properties

Een eigenschap is een container die de meeste andere bronnen bevat die beschikbaar zijn in de Reactor-API. De enige middelen die niet in het bezit zijn van een bezit zijn controlegebeurtenissen, bedrijven, uitbreidingspakketten, en profielen. Een bezit behoort tot precies één bedrijf, en een bedrijf kan vele eigenschappen hebben.

Zie de [&#x200B; eigenschappen eindpuntgids &#x200B;](./endpoints/properties.md) leren hoe te om eigenschappen in API te beheren.

## Gegevenselementen

Een gegevenselement werkt als een variabele die naar een belangrijk stuk gegevens binnen uw toepassing verwijst. De elementen van gegevens worden gebruikt binnen regels en uitbreidingsconfiguraties. Wanneer de regel wordt geactiveerd bij uitvoering in een browser of toepassing, wordt de waarde van het gegevenselement opgelost en gebruikt binnen de regel.

Zie de [&#x200B; gids van het de elementeneindpunt van gegevenselementen &#x200B;](./endpoints/data-elements.md) leren hoe te om gegevenselementen in API te beheren.

## Regels

De regels controleren het gedrag van de middelen in een opgestelde bibliotheek. Een regel is een groep van één of meerdere regelcomponenten, en bestaat om de regelcomponenten samen op een logische manier te binden.

Zie de [&#x200B; gids van het regeleindpunt &#x200B;](./endpoints/rules.md) leren hoe te om regels in API te beheren.

## Regelcomponenten

De componenten van de regel zijn de individuele punten die omhoog een regel maken. Regelcomponenten hebben drie basistypen:

* **Gebeurtenissen**: Wat activeert een regel
* **Voorwaarden**: Wat de regel controleert om een actie te bepalen
* **Acties**: Wat de regel afhankelijk van uitvoert of de voorwaarde wordt voldaan aan

Zie de [&#x200B; gids van het regeleindpunt &#x200B;](./endpoints/rules.md) leren hoe te om regels in API te beheren.

## Extensiepakketten

Een extensiepakket bestaat uit een groep afzonderlijke mogelijkheden die aan een taggebruiker beschikbaar kunnen worden gesteld. Het meest meestal komen deze mogelijkheden in de vorm van regelcomponenten en gegevenselementen, maar kunnen ook belangrijkste modules en gedeelde modules omvatten. De mogelijkheden van een extensiepakket worden geïnstalleerd als een extensie wanneer deze in een bibliotheek wordt opgenomen.

Zie de [&#x200B; gids van de uitbreidingspakketten van de uitbreidingspakketten &#x200B;](./endpoints/extension-packages.md) leren hoe te om uitbreidingspakketten in API te beheren.

## Extensies

Een extensie vertegenwoordigt de geïnstalleerde instantie van een extensiepakket. Met een extensie worden de functies die door een extensiepakket worden gedefinieerd, beschikbaar gemaakt voor een eigenschap. Deze functies worden gebruikt bij het maken van gegevenselementen en regelcomponenten.

Zie de [&#x200B; gids van het uitbreidingseindpunt &#x200B;](./endpoints/extensions.md) leren hoe te om uitbreidingen in API te beheren.

## Bibliotheken

Een bibliotheek is een inzameling van middelen (uitbreidingen, regels, en gegevenselementen) die het gewenste gedrag van een bezit vertegenwoordigen. Bibliotheken worden gecompileerd in builds, en die bouwstijlen worden toegewezen aan verschillende milieu&#39;s aangezien zij neer de het publiceren stroom van het testen aan productie bewegen.

Zie de [&#x200B; gids van het bibliotheekeindpunt &#x200B;](./endpoints/libraries.md) leren hoe te om bibliotheken in API te beheren.

## Builds

Een markeringsbibliotheek wordt gecompileerd in een bouwstijl zodat het aan een milieu voor het testen en plaatsing wordt toegewezen. De inhoud van een bouwstijl varieert afhankelijk van de middelen inbegrepen in de bibliotheek, de configuratie van het milieu waaraan de bouwstijl wordt toegewezen, en het platform van het bezit dat de bouwstijl tot behoort.

Zie [&#x200B; bouwt eindpuntgids &#x200B;](./endpoints/builds.md) om te leren hoe te om bouwt in API te beheren.

## Omgevingen

Een milieu wijst op de specifieke gastheer waar een bouwstijl kan worden opgesteld, en of de bouwstijl als reeks dossiers zou moeten worden opgesteld of in een archiefformaat gecomprimeerd. In de Reactor-API staan omgevingen los van hosts zelf, die worden beheerd door het `/hosts` -eindpunt.

Zie [&#x200B; bouwt eindpuntgids &#x200B;](./endpoints/builds.md) om te leren hoe te om bouwt in API te beheren.

## Gastheren

Een gastheer vertegenwoordigt een ontvangen bestemming waar een bibliotheek kan worden geleverd en uiteindelijk worden opgesteld bouwt. Gastheren kunnen Akamai- of SFTP-servers zijn.

Zie de [&#x200B; gids van het gastheereindpunt &#x200B;](./endpoints/hosts.md) leren hoe te om gastheren in API te beheren.

## App-configuraties

Toepassingsconfiguraties staan toe dat referenties worden opgeslagen en opgehaald voor later gebruik. Zie de [&#x200B; gids van het de eindpunt van toepassingsconfiguraties &#x200B;](./endpoints/app-configurations.md) leren hoe te om app configuraties in API te beheren.

## Controlegebeurtenissen

Een auditgebeurtenis is een record van een specifieke wijziging in een andere tagbron die wordt gegenereerd op het moment dat de wijziging wordt aangebracht. Dit zijn systeemgebeurtenissen waarop kan worden geabonneerd door het gebruik van een callback functie.

Zie de [&#x200B; gids van het de controlegebeurtenissen eindpunt van gebeurtenissen &#x200B;](./endpoints/audit-events.md) leren hoe te om controlegebeurtenissen in API te beheren.

## Callbacks

Een callback is een bericht dat Experience Platform naar een gastheer URL verzendt wanneer een nieuwe controlegebeurtenis wordt geproduceerd. Zie de [&#x200B; gids van het callbacks eindpunt &#x200B;](./endpoints/callbacks.md) leren hoe te om callbacks in API te beheren.

## Notities

Notities zijn tekstuele annotaties die u aan bepaalde tagbronnen kunt toevoegen, zoals gegevenselementen, extensies, bibliotheken, eigenschappen, regels en regelcomponenten. Zie de [&#x200B; gids van het Notitieeindpunt &#x200B;](./endpoints/notes.md) leren hoe te nota&#39;s in API beheren.

## Profiel

Een profiel bevat alle informatie over de aangemelde gebruiker, inclusief alle Adobe Orgs waartoe ze behoren, de productprofielen waartoe ze behoren binnen elke organisatie en de rechten die ze hebben van elk productprofiel.

Zie de [&#x200B; gids van het profieleindpunt &#x200B;](./endpoints/profile.md) leren hoe te om deze informatie in API te bekijken.

## Zoeken

Het `/search` eindpunt verstrekt een manier om middelen te vinden die een gewenste die criteria aanpassen, als vraag wordt uitgedrukt. Alle vragen zijn scoped aan uw huidige bedrijf en toegankelijke eigenschappen. Zie de [&#x200B; gids van het onderzoekseindpunt &#x200B;](./endpoints/search.md) leren hoe deze functionaliteit gebruikt.

## Geheimen

Een geheim bevat geloofsbrieven die gebeurtenis toestaan door:sturen om aan een ander systeem voor veilige gegevensuitwisseling voor authentiek te verklaren. Zie de [&#x200B; geheimengids &#x200B;](./guides/secrets.md) voor een overzicht op hoe de geheimen in gebeurtenis door:sturen functioneren, en de [&#x200B; geheimen eindpuntgids &#x200B;](./endpoints/secrets.md) leren hoe te om hen in Reactor API te beheren.

## Volgende stappen

Begin makend vraag gebruikend de Registratie API van het Schema, lees [&#x200B; begonnen gids &#x200B;](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
