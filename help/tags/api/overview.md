---
title: Reactor-API
description: Met de Reactor-API kunnen ontwikkelaars programmatisch alle bronnen voor tags in Adobe Experience Platform beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: 153eab11-db08-499e-80d1-c56f254372ce
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# [!DNL Reactor] API-handleiding

De Reactor-API bevat verschillende eindpunten waarmee u programmatisch alle bronnen voor tags in Adobe Experience Platform kunt beheren.

Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over het verifiëren aan API.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de [Referentie voor Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/).

## Bedrijven

Een bedrijf vertegenwoordigt de organisatie van een markeringsgebruiker, typisch een zaken. Deze bedrijven komen overeen met 1:1 met IMS Organisatie-id&#39;s. API-gebruikers hebben alleen zichtbaarheid in de bedrijven waartoe zij toegang hebben.

Zie de [eindgids voor bedrijven](./endpoints/companies.md) voor meer informatie over het weergeven van beschikbare bedrijven in de API.

## Properties

Een eigenschap is een container die de meeste andere bronnen bevat die beschikbaar zijn in de Reactor-API. De enige middelen die niet in het bezit zijn van een bezit zijn controlegebeurtenissen, bedrijven, uitbreidingspakketten, en profielen. Een bezit behoort tot precies één bedrijf, en een bedrijf kan vele eigenschappen hebben.

Zie de [leidraad voor eigenschappen eindpunt](./endpoints/properties.md) voor meer informatie over het beheren van eigenschappen in de API.

## Gegevenselementen

Een gegevenselement werkt als een variabele die naar een belangrijk stuk gegevens binnen uw toepassing verwijst. De elementen van gegevens worden gebruikt binnen regels en uitbreidingsconfiguraties. Wanneer de regel wordt geactiveerd bij uitvoering in een browser of toepassing, wordt de waarde van het gegevenselement opgelost en gebruikt binnen de regel.

Zie de [eindgids voor gegevenselementen](./endpoints/data-elements.md) voor meer informatie over het beheren van gegevenselementen in de API.

## Regels

De regels controleren het gedrag van de middelen in een opgestelde bibliotheek. Een regel is een groep van één of meerdere regelcomponenten, en bestaat om de regelcomponenten samen op een logische manier te binden.

Zie de [leidraad voor regeleindpunten](./endpoints/rules.md) voor meer informatie over het beheren van regels in de API.

## Regelcomponenten

De componenten van de regel zijn de individuele punten die omhoog een regel maken. Regelcomponenten hebben drie basistypen:

* **Gebeurtenissen**: Wat een regel activeert
* **Voorwaarden**: Wat de regel controleert om een actie te bepalen
* **Handelingen**: Wat de regel uitvoert afhankelijk van of aan de voorwaarde wordt voldaan

Zie de [leidraad voor regeleindpunten](./endpoints/rules.md) voor meer informatie over het beheren van regels in de API.

## Extensiepakketten

Een extensiepakket bestaat uit een groep afzonderlijke mogelijkheden die aan een taggebruiker beschikbaar kunnen worden gesteld. Het meest meestal komen deze mogelijkheden in de vorm van regelcomponenten en gegevenselementen, maar kunnen ook belangrijkste modules en gedeelde modules omvatten. De mogelijkheden van een extensiepakket worden geïnstalleerd als een extensie wanneer deze in een bibliotheek wordt opgenomen.

Zie de [eindhulplijn extensiepakketten](./endpoints/extension-packages.md) voor meer informatie over het beheren van extensiepakketten in de API.

## Extensies

Een extensie vertegenwoordigt de geïnstalleerde instantie van een extensiepakket. Met een extensie worden de functies die door een extensiepakket worden gedefinieerd, beschikbaar gemaakt voor een eigenschap. Deze functies worden gebruikt bij het maken van gegevenselementen en regelcomponenten.

Zie de [eindgebruikershandleiding voor extensies](./endpoints/extensions.md) voor meer informatie over het beheren van extensies in de API.

## Bibliotheken

Een bibliotheek is een inzameling van middelen (uitbreidingen, regels, en gegevenselementen) die het gewenste gedrag van een bezit vertegenwoordigen. Bibliotheken worden gecompileerd in builds, en die bouwstijlen worden toegewezen aan verschillende milieu&#39;s aangezien zij neer de het publiceren stroom van het testen aan productie bewegen.

Zie de [hulplijn voor bibliotheekeindpunt](./endpoints/libraries.md) voor meer informatie over het beheren van bibliotheken in de API.

## Builds

Een markeringsbibliotheek wordt gecompileerd in een bouwstijl zodat het aan een milieu voor het testen en plaatsing wordt toegewezen. De inhoud van een bouwstijl varieert afhankelijk van de middelen inbegrepen in de bibliotheek, de configuratie van het milieu waaraan de bouwstijl wordt toegewezen, en het platform van het bezit dat de bouwstijl tot behoort.

Zie de [bouwt eindpuntgids](./endpoints/builds.md) voor meer informatie over het beheren van builds in de API.

## Omgevingen

Een milieu wijst op de specifieke gastheer waar een bouwstijl kan worden opgesteld, en of de bouwstijl als reeks dossiers zou moeten worden opgesteld of in een archiefformaat gecomprimeerd. In de Reactor-API staan omgevingen los van hosts zelf, die worden beheerd door de `/hosts` eindpunt.

Zie de [bouwt eindpuntgids](./endpoints/builds.md) voor meer informatie over het beheren van builds in de API.

## Gastheren

Een gastheer vertegenwoordigt een ontvangen bestemming waar een bibliotheek kan worden geleverd en uiteindelijk worden opgesteld bouwt. Gastheren kunnen Akamai- of SFTP-servers zijn.

Zie de [eindgebruikershandleiding voor hosts](./endpoints/hosts.md) om te leren hoe u hosts in de API kunt beheren.

## App-configuraties

Met toepassingsconfiguraties kunnen referenties worden opgeslagen en opgehaald voor later gebruik. Zie de [eindhulplijn voor app-configuraties](./endpoints/app-configurations.md) voor meer informatie over het beheren van toepassingsconfiguraties in de API.

## Gebeurtenissen van Audit

Een auditgebeurtenis is een record van een specifieke wijziging in een andere tagbron die wordt gegenereerd op het moment dat de wijziging wordt aangebracht. Dit zijn systeemgebeurtenissen waarop kan worden geabonneerd door het gebruik van een callback functie.

Zie de [eindhandleiding voor auditgebeurtenissen](./endpoints/audit-events.md) voor meer informatie over het beheren van auditgebeurtenissen in de API.

## Callbacks

Een callback is een bericht dat het Platform naar een gastheer URL verzendt wanneer een nieuwe controlegebeurtenis wordt geproduceerd. Zie de [callbacks eindgebruikergids](./endpoints/callbacks.md) om te leren hoe te om callbacks in API te beheren.

## Notities

Notities zijn tekstuele annotaties die u aan bepaalde tagbronnen kunt toevoegen, zoals gegevenselementen, extensies, bibliotheken, eigenschappen, regels en regelcomponenten. Zie de [leidraad voor notitiepunten](./endpoints/notes.md) voor meer informatie over het beheren van notities in de API.

## Profiel

Een profiel bevat alle informatie over de aangemelde gebruiker, met inbegrip van alle Adobe Orgs waartot zij behoren, de productprofielen zij tot binnen elk Org behoren, en de rechten die zij van elk productprofiel hebben.

Zie de [overzichtstekeneindhulplijn](./endpoints/profile.md) voor informatie over het weergeven van deze informatie in de API.

## Zoeken

De `/search` eindpunt verstrekt een manier om middelen te vinden die een gewenste criteria aanpassen, die als vraag wordt uitgedrukt. Alle vragen zijn scoped aan uw huidige bedrijf en toegankelijke eigenschappen. Zie de [zoekeindpuntgids](./endpoints/search.md) voor meer informatie over het gebruik van deze functionaliteit.

## Geheimen

Een geheim bevat geloofsbrieven die gebeurtenis toestaan door:sturen om aan een ander systeem voor veilige gegevensuitwisseling voor authentiek te verklaren. Zie de [geheimengids](./guides/secrets.md) voor een overzicht over hoe de geheimen in gebeurtenis het door:sturen functioneren, en [punthulplijn voor geheimen](./endpoints/secrets.md) om te leren hoe u ze beheert in de Reactor-API.

## Volgende stappen

Beginnen het maken van vraag gebruikend de Registratie API van het Schema, lees [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.
