---
title: Aanvullende informatie van april 2020 voor Adobe Experience Platform
description: Aanvullende informatie van april 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: opmerkingen bij de release;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 26%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 8 april 2020**

Nieuwe functies in Adobe Experience Platform:

* [[!DNL Intelligent Services]](#intelligent)

Updates voor bestaande functies:

* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Datagovernance](#governance)
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

Voor meer informatie over [!DNL Intelligent Services] en wat het moet aanbieden, zie het [&#x200B; Intelligente overzicht van de Diensten &#x200B;](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)-systeem {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform] . [!DNL Experience Data Model] (XDM), aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Automatische alternatieve weergave-info | [!DNL Schema Registry] past automatisch de aangepaste titel- en beschrijvingswaarden toe die in de `alternateDisplayInfo` -descriptor zijn geconfigureerd. |
| Beperkingen voor scalaire velden | [!DNL Schema Registry] staat niet meer dan 6000 scalaire gebieden in één enkel schema toe. |
| Overzicht van prestaties | De [!DNL Schema Registry] is hervormd om te presteren en aan de eisen van [!DNL Experience Platform] beter te voldoen. |

**Bugfixes**

* Bijgewerkt XDM in XED geconverteerd om een schonere XED formaat voor genestelde gebieden van URI in standaardXDM te steunen.

**Bekende kwesties**

* Bekend

## Datagovernance {#governance}

Adobe Experience Platform-datagovernance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving te waarborgen van regelgeving, beperkingen en beleidsregels die op gegevensgebruik van toepassing zijn. Dit speelt binnen [!DNL Experience Platform] een sleutelrol op verschillende niveaus zoals catalogisering, gegevensoorsprong, labeling van gegevensgebruik, beleid voor gegevenstoegang en beheer van toegang tot gegevens voor marketingacties.

Aan de slag met gegevensbeheer vereist een grondig inzicht in de verordeningen, de contractuele verplichtingen, en het collectieve beleid die op uw klantengegevens van toepassing zijn. Daarna kunnen gegevens worden geclassificeerd door de juiste labels voor gegevensgebruik toe te passen en kan het gebruik ervan worden geregeld door de definitie van beleid voor gegevensgebruik.

Het gegevensbeheerframework vereenvoudigt en stroomlijnt het proces voor het categoriseren van gegevens en het maken van beleidsregels voor gegevensgebruik via de gebruikersinterface en de API van [!DNL Experience Platform] .[!DNL Policy Service]

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Beleid voor gegevensgebruik beheren in de gebruikersinterface | Het beleid van het gegevensgebruik kan nu binnen de **1&rbrace; werkruimte van Beleid &lbrace;in** UI worden geleid. [!DNL Experience Platform] Zie de [&#x200B; gids van de beleidsgebruiker &#x200B;](../../data-governance/policies/user-guide.md) voor meer informatie. |

**Bekende kwesties**

* Geen.

Voor meer informatie, gelieve te zien het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](../../data-governance/home.md).


## Bestemmingen {#destinations}

In [&#x200B; Real-Time Customer Data Platform &#x200B;](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Real-Time CDP ondersteunt nu gegevensactivering voor meer dan vijftig [!DNL Experience Cloud Launch] extensies, waardoor analyses, personalisatie en andere gebruiksgevallen mogelijk zijn. Zie hieronder voor meer informatie:

| Documentatie | Beschrijving |
|--- | ---|
| [&#x200B; de types en de categorieën van de Bestemming &#x200B;](../../destinations/destination-types.md) | Dit artikel verklaart het verschil tussen verbindingen en uitbreidingen in de interface van Real-Time CDP en adviseert wanneer om elk van deze bestemmingen te gebruiken. |
| [&#x200B; de uitbreidingen van de Lancering van het Platform van de Ervaring &#x200B;](../../destinations/catalog/launch-extensions/overview.md) | Op deze pagina wordt uitgelegd wat [!DNL Launch] extensies zijn, worden gebruiksscenario&#39;s voor het gebruik van extensies vermeld en worden koppelingen naar documentatie voor elke [!DNL Launch] -extensie in Real-Time CDP weergegeven. |

Voor meer informatie, gelieve te zien het [&#x200B; overzicht van Doelen &#x200B;](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot privé- of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | De verzoeken van de privacy kunnen nu worden gecreeerd en worden gevolgd onder de Wet van de Bescherming van Persoonlijke Gegevens (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de array `regulation` de waarde &#39;pdpa_tha&#39;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Request Builder in de gebruikersinterface van [!DNL Privacy Service]. Raadpleeg het [handboek](../../privacy-service/ui/user-guide.md) voor meer informatie. |
| Afschaffing van het oude eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is afgeschaft. |

Bekende problemen

* Geen

Voor meer informatie over [!DNL Privacy Service], gelieve te beginnen door het [&#x200B; overzicht van Privacy Service &#x200B;](../../privacy-service/home.md) te lezen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| API- en UI-ondersteuning voor databases | Nieuwe bronaansluitingen voor [!DNL Apache Spark] (op HDInsights), [!DNL Azure Synapse Analytics] , [!DNL Azure Table Storage] en [!DNL Hive] . |
| API- en UI-ondersteuning voor op protocollen gebaseerde toepassingen | Nieuwe bronconnectors voor [!DNL Generic OData]. |

**Bekende kwesties**

* Geen

Meer over bronnen leren, zie het [&#x200B; overzicht van bronnen &#x200B;](../../sources/home.md).
