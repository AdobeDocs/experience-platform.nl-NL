---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform van 8 april 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 8cc3b63fc91877ca1337f65e8f5c0e949b7ef01f

---


# Opmerkingen bij de release Adobe Experience Platform

## Releasedatum: 8 april 2020

Nieuwe functies in het Adobe Experience Platform:
* [Intelligente services](#intelligent)

Updates voor bestaande functies:
* [Experience Data Model (XDM)](#xdm)
* [Gegevensbeheer](#governance)
* [Doelen](#destinations)
* [Privacy Service](#privacy)
* [Bronnen](#sources)

## Intelligente services {#intelligent}

Intelligente services stellen marketinganalisten en praktijkmensen in staat om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen van de klantervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap. Daarnaast kunnen marketingmedewerkers voorspellingen activeren in Adobe Experience Cloud, Adobe Experience Platform en toepassingen van derden.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|---|---|
| Customer AI | Klantenservice-AI biedt marketers de mogelijkheid om voorspellingen van klanten op individueel niveau te genereren met uitleg. Met behulp van invloedrijke factoren kan de AI van de Klant u vertellen wat een klant waarschijnlijk zal doen en waarom. Bovendien kunnen marketers profiteren van de voorspellingen en inzichten van de klant van AI om de ervaringen van klanten aan te passen door de meest geschikte aanbiedingen en berichten te bedienen. |
| Attributie-AI | Attribution AI is een multi-channel, algoritmische attributiedienst die de invloed en de incrementele impact van klanteninteractie tegen gespecificeerde resultaten berekent. Met Attribution AI kunnen marketers marketing- en advertentiekosten meten en optimaliseren door de impact van elke afzonderlijke interactie van de klant in elke fase van de reizen van de klant te begrijpen. |

**Bekende problemen**

* Momenteel geen bekende problemen.

Voor meer informatie over de Intelligente Diensten en wat het moet aanbieden, zie het Overzicht [van de](../../intelligent-services/home.md)Intelligente Diensten.

## XDM-systeem (Experience Data Model) {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter het ervaringsplatform. Experience Data Model (XDM), aangestuurd door Adobe, is een poging om gegevens over klantervaring te standaardiseren en schema&#39;s voor het beheer van klantervaring te definiëren.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Deze biedt algemene structuren en definities waarmee toepassingen kunnen communiceren met services op het Adobe Experience Platform. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Automatische alternatieve weergave-info | De Register van het Schema past automatisch de aangepaste titel en beschrijvingswaarden toe die in de `alternateDisplayInfo` beschrijver worden gevormd. |
| Beperkingen voor scalaire velden | De Registratie van het Schema staat meer dan 6000 scalaire gebieden in één enkel schema niet toe. |
| Overzicht van prestaties | Het register van het Schema is herzien om beter te presteren en aan de eisen van het Platform van de Ervaring te voldoen. |

**Bugfixes**

* Bijgewerkt XDM in XED geconverteerd om een schonere XED formaat voor genestelde gebieden van URI in standaardXDM te steunen.

**Bekende problemen**

* Bekend

## Gegevensbeheer {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en om ervoor te zorgen dat wordt voldaan aan de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik. Het speelt een sleutelrol binnen het ervaringsplatform op diverse niveaus, met inbegrip van catalogisering, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

Aan de slag met gegevensbeheer vereist een grondig inzicht in de verordeningen, de contractuele verplichtingen, en het collectieve beleid die op uw klantengegevens van toepassing zijn. Daarna kunnen gegevens worden geclassificeerd door de juiste labels voor gegevensgebruik toe te passen en kan het gebruik ervan worden geregeld door de definitie van beleid voor gegevensgebruik.

Het DULE-framework vereenvoudigt en stroomlijnt het proces voor het indelen van gegevens en het maken van beleidsregels voor gegevensgebruik via de gebruikersinterface van het Experience Platform en de DULE Policy Service API.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Beleid voor gegevensgebruik beheren in de gebruikersinterface | Het beleid voor gegevensgebruik kan nu worden beheerd binnen de werkruimte _Beleid_ in de gebruikersinterface van het Experience Platform. Zie de gids [van de](../../data-governance/policies/user-guide.md) beleidsgebruiker voor meer informatie. |

**Bekende problemen**

* Geen.

Zie het overzicht [van](../../data-governance/home.md)gegevensbeheer voor meer informatie.


## Doelen {#destinations}

In [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md)zijn doelen vooraf gebouwde integratie met doelplatforms die gegevens naadloos aan die partners activeren.

**Nieuwe bestemmingen**

Adobe CDP in realtime ondersteunt nu gegevensactivering voor meer dan vijftig Experience Cloud Launch-extensies, waardoor analyses, personalisatie en andere gebruiksgevallen mogelijk zijn. Zie hieronder voor meer informatie:

| Documentatie | Beschrijving |
|--- | ---|
| [Doeltypen en -categorieën](/help/rtcdp/destinations/destination-types.md) | Dit artikel verklaart het verschil tussen verbindingen en uitbreidingen in de interface van Adobe in real time CDP en adviseert wanneer om elk van deze bestemmingen te gebruiken. |
| [Experience Platform Launch-extensies](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | Op deze pagina wordt uitgelegd wat extensies Starten zijn, worden gebruiksscenario&#39;s voor het gebruik van extensies vermeld en worden koppelingen naar documentatie voor elke extensie Starten in Adobe Real-time CDP weergegeven. |

Zie het overzicht [](/help/rtcdp/destinations/destinations-overview.md)Doelen voor meer informatie.

## Privacy Service {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform Privacy Service biedt een RESTful API en een gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met de Privacy Service kunt u verzoeken om toegang tot persoonlijke of persoonlijke klantgegevens van Adobe Experience Cloud-toepassingen en deze verwijderen. Zo kunt u de automatische naleving van wettelijke en organisatorische privacyregels vereenvoudigen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | De verzoeken van de privacy kunnen nu worden gecreeerd en worden gevolgd onder de Wet van de Bescherming van Persoonlijke Gegevens (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de `regulation` array de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Request Builder in de gebruikersinterface van de privacyservice. Raadpleeg de [gebruikershandleiding](../../privacy-service/ui/user-guide.md) voor meer informatie. |
| Oude afleiding van eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is vervangen. |

Bekende problemen

* Geen

Voor meer informatie over de Dienst van de Privacy, gelieve te beginnen door het overzicht [van de Dienst van de](../../privacy-service/home.md)Privacy te lezen.

## Bronnen {#sources}

Met het Adobe Experience Platform kunt u gegevens uit externe bronnen ophalen en tegelijk die gegevens structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Het Platform van de ervaring verstrekt RESTful API en een interactieve UI die u bronverbindingen voor diverse gegevensleveranciers met gemak laat opzetten. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| API- en UI-ondersteuning voor databases | Nieuwe bronaansluitingen voor Apache Spark (op HDInsights), Azure Synapse Analytics, Azure Table Storage, Hive (op HDInsights) en Phoenix. |
| API- en UI-ondersteuning voor op betalingen gebaseerde toepassingen | Nieuwe bronconnectors voor PayPal. |
| API- en UI-ondersteuning voor op protocollen gebaseerde toepassingen | Nieuwe bronconnectors voor Generic OData. |

**Bekende problemen**

* Geen

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.
