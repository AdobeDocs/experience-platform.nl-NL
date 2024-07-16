---
title: Opmerkingen bij de release van Adobe Experience Platform, april 2020
description: Aanvullende informatie van april 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: opmerkingen bij de release;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 8 april 2020**

Nieuwe functies in Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Updates voor bestaande functies:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Gegevensbeheer](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] biedt marketinganalisten en -professionals de mogelijkheid om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in praktijkgevallen van klanten. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap. Daarnaast kunnen marketingspecialisten voorspellingen activeren in Adobe Experience Cloud, Adobe Experience Platform en toepassingen van derden.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] biedt marketers de mogelijkheid om klantprognoses op individueel niveau met uitleg te genereren. Met behulp van invloedrijke factoren kan [!DNL Customer AI] u vertellen wat een klant waarschijnlijk zal doen en waarom. Daarnaast kunnen marketers profiteren van [!DNL Customer AI] voorspellingen en inzichten om de ervaringen van klanten aan te passen door de meest geschikte aanbiedingen en berichten te leveren. |
| [!DNL Attribution AI] | [!DNL Attribution AI] is een multi-channel, algoritmische attributieservice die de invloed en de stijgende invloed van klanteninteractie tegen gespecificeerde resultaten berekent. Met [!DNL Attribution AI] kunnen marketers marketing- en advertentiekosten meten en optimaliseren door inzicht te krijgen in de impact van elke afzonderlijke interactie van de klant in elke fase van de reizen van de klant. |

**Bekende kwesties**

* Momenteel geen bekende problemen.

Voor meer informatie over [!DNL Intelligent Services] en wat het moet aanbieden, zie het [ Intelligente overzicht van de Diensten ](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)-systeem {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform] . [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Automatische alternatieve weergave-info | [!DNL Schema Registry] past automatisch de aangepaste titel- en beschrijvingswaarden toe die in de `alternateDisplayInfo` -descriptor zijn geconfigureerd. |
| Beperkingen voor scalaire velden | [!DNL Schema Registry] staat niet meer dan 6000 scalaire gebieden in één enkel schema toe. |
| Overzicht van prestaties | De [!DNL Schema Registry] is hervormd om te presteren en aan de eisen van [!DNL Experience Platform] beter te voldoen. |

**Bugfixes**

* Bijgewerkt XDM in XED geconverteerd om een schonere XED formaat voor genestelde gebieden van URI in standaardXDM te steunen.

**Bekende kwesties**

* Bekend

## Gegevensbeheer {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. De klasse speelt binnen [!DNL Experience Platform] op diverse niveaus een sleutelrol, zoals catalogisering, gegevenskoppeling, labels voor gegevensgebruik, beleid voor gegevenstoegang en toegangsbeheer voor marketingacties.

Aan de slag met gegevensbeheer vereist een grondig inzicht in de verordeningen, de contractuele verplichtingen, en het collectieve beleid die op uw klantengegevens van toepassing zijn. Daarna kunnen gegevens worden geclassificeerd door de juiste labels voor gegevensgebruik toe te passen en kan het gebruik ervan worden geregeld door de definitie van beleid voor gegevensgebruik.

Het gegevensbeheerframework vereenvoudigt en stroomlijnt het proces voor het categoriseren van gegevens en het maken van beleidsregels voor gegevensgebruik via de gebruikersinterface en de API van [!DNL Experience Platform] .[!DNL Policy Service]

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| -----------| ---------- |
| Beleid voor gegevensgebruik beheren in de gebruikersinterface | Het beleid van het gegevensgebruik kan nu binnen de **1} werkruimte van Beleid {in [!DNL Experience Platform] UI worden geleid.** Zie de [ gids van de beleidsgebruiker ](../../data-governance/policies/user-guide.md) voor meer informatie. |

**Bekende kwesties**

* Geen.

Voor meer informatie, gelieve te zien het [ overzicht van het Beleid van Gegevens ](../../data-governance/home.md).


## Doelen {#destinations}

In [ Real-time Customer Data Platform ](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Real-Time CDP ondersteunt nu gegevensactivering voor meer dan vijftig [!DNL Experience Cloud Launch] extensies, waardoor analyses, personalisatie en andere gebruiksgevallen mogelijk zijn. Zie hieronder voor meer informatie:

| Documentatie | Beschrijving |
|--- | ---|
| [ de types en de categorieën van de Bestemming ](../../destinations/destination-types.md) | Dit artikel verklaart het verschil tussen verbindingen en uitbreidingen in de interface van Real-Time CDP en adviseert wanneer om elk van deze bestemmingen te gebruiken. |
| [ uitbreidingen van het Experience Platform Launch ](../../destinations/catalog/launch-extensions/overview.md) | Op deze pagina wordt uitgelegd wat [!DNL Launch] extensies zijn, worden gebruiksscenario&#39;s voor het gebruik van extensies vermeld en worden koppelingen naar documentatie voor elke [!DNL Launch] -extensie in Real-Time CDP weergegeven. |

Voor meer informatie, gelieve te zien het [ overzicht van Doelen ](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | De verzoeken van de privacy kunnen nu worden gecreeerd en worden gevolgd onder de Wet van de Bescherming van Persoonlijke Gegevens (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de array `regulation` de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Request Builder in de gebruikersinterface van [!DNL Privacy Service] . Zie de [ gebruikersgids ](../../privacy-service/ui/user-guide.md) voor meer informatie. |
| Oude afleiding van eindpunt | Het oude API eindpunt (`data/privacy/gdpr`) is afgekeurd. |

Bekende problemen

* Geen

Voor meer informatie over [!DNL Privacy Service], gelieve te beginnen door het [ overzicht van de Privacy Service ](../../privacy-service/home.md) te lezen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| API- en UI-ondersteuning voor databases | Nieuwe bronaansluitingen voor [!DNL Apache Spark] (op HDInsights), [!DNL Azure Synapse Analytics] , [!DNL Azure Table Storage] , [!DNL Hive] (op HDInsights) en [!DNL Phoenix] . |
| API- en UI-ondersteuning voor op betalingen gebaseerde toepassingen | Nieuwe bronconnectors voor [!DNL PayPal]. |
| API- en UI-ondersteuning voor op protocollen gebaseerde toepassingen | Nieuwe bronconnectors voor [!DNL Generic OData]. |

**Bekende kwesties**

* Geen

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
