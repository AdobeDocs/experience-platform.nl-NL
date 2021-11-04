---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 8 april 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: opmerkingen bij de release;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 8 april 2020**

Nieuwe functies in Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Updates voor bestaande functies:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Data Governance](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] marketinganalisten en praktijkbeoefenaars in staat stellen de kracht van kunstmatige intelligentie en het leren van machines te benutten in gevallen waarin de klant gebruikmaakt van ervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap. Daarnaast kunnen marketingspecialisten voorspellingen activeren in Adobe Experience Cloud, Adobe Experience Platform en toepassingen van derden.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] biedt marketers de mogelijkheid om klantprognoses op individueel niveau te genereren met uitleg. Met behulp van invloedrijke factoren [!DNL Customer AI] kan u vertellen wat een klant waarschijnlijk zal doen en waarom. Bovendien kunnen marketeers profiteren van [!DNL Customer AI] voorspellingen en inzichten om klantenervaringen te personaliseren door de meest aangewezen aanbiedingen en overseinen te dienen. |
| [!DNL Attribution AI] | [!DNL Attribution AI] is een multi-channel, algoritmische attributiedienst die de invloed en de stijgende invloed van klanteninteractie tegen gespecificeerde resultaten berekent. Met [!DNL Attribution AI]Marketers kunnen marketing- en reclameuitgaven meten en optimaliseren door inzicht te krijgen in de impact van elke individuele interactie van de klant in elke fase van de reis van de klant. |

**Bekende problemen**

* Momenteel geen bekende problemen.

Voor meer informatie over [!DNL Intelligent Services] en wat zij te bieden heeft, zie [Overzicht van intelligente services](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Automatische alternatieve weergave-info | De [!DNL Schema Registry] past automatisch de aangepaste titel en beschrijvingswaarden toe die in worden gevormd `alternateDisplayInfo` descriptor. |
| Beperkingen voor scalaire velden | De [!DNL Schema Registry] staat niet meer dan 6000 scalaire gebieden in één enkel schema toe. |
| Overzicht van prestaties | De [!DNL Schema Registry] is herzien om te presteren en aan de eisen van [!DNL Experience Platform] beter. |

**Bugfixes**

* Bijgewerkt XDM in XED geconverteerd om een schonere XED formaat voor genestelde gebieden van URI in standaardXDM te steunen.

**Bekende problemen**

* Bekend

## Gegevensbeheer {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen [!DNL Experience Platform] op verschillende niveaus, waaronder catalogisering, gegevenskoppeling, etikettering van het gegevensgebruik, beleid inzake gegevenstoegang en toegangscontrole voor marketingacties.

Aan de slag met gegevensbeheer vereist een grondig inzicht in de verordeningen, de contractuele verplichtingen, en het collectieve beleid die op uw klantengegevens van toepassing zijn. Daarna kunnen gegevens worden geclassificeerd door de juiste labels voor gegevensgebruik toe te passen en kan het gebruik ervan worden geregeld door de definitie van beleid voor gegevensgebruik.

Het gegevensbeheerkader vereenvoudigt en stroomlijnt het proces om gegevens te categoriseren en gegevensgebruiksbeleid tot stand te brengen door [!DNL Experience Platform] gebruikersinterface en [!DNL Policy Service] API.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Beleid voor gegevensgebruik beheren in de gebruikersinterface | Het beleid voor gegevensgebruik kan nu worden beheerd binnen het **Beleid** werkruimte in de [!DNL Experience Platform] UI. Zie de [beleidsgebruikershandleiding](../../data-governance/policies/user-guide.md) voor meer informatie . |

**Bekende problemen**

* Geen.

Zie voor meer informatie de [Overzicht van gegevensbeheer](../../data-governance/home.md).


## Doelen {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

CDP in real time ondersteunt nu gegevensactivering tot meer dan vijftig [!DNL Experience Cloud Launch] extensies, analyses, personalisatie en andere gebruiksgevallen inschakelen. Zie hieronder voor meer informatie:

| Documentatie | Beschrijving |
|--- | ---|
| [Doeltypen en -categorieën](../../destinations/destination-types.md) | Dit artikel verklaart het verschil tussen verbindingen en uitbreidingen in de interface In real time CDP en adviseert wanneer om elk van deze bestemmingen te gebruiken. |
| [Experience Platform Launch-extensies](../../destinations/catalog/launch-extensions/overview.md) | Op deze pagina wordt uitgelegd wat [!DNL Launch] extensies zijn, geven een overzicht van de gebruikte hoofdletters en kleine letters en koppelingen naar documentatie voor elke extensie [!DNL Launch] extensie in Real-Time CDP. |

Zie voor meer informatie de [Overzicht van doelen](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful API en een gebruikersinterface om u te helpen deze gegevensverzoeken van uw klanten beheren. Met [!DNL Privacy Service]kunt u verzoeken om toegang tot persoonlijke of persoonlijke klantgegevens van Adobe Experience Cloud-toepassingen en deze verwijderen, zodat u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | De verzoeken van de privacy kunnen nu worden gecreeerd en worden gevolgd onder de Wet van de Bescherming van Persoonlijke Gegevens (PDPA) in Thailand. Wanneer u een privacyverzoek indient in de API, wordt de `regulation` array accepteert de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de Request Builder in het dialoogvenster [!DNL Privacy Service] UI. Zie de [gebruikershandleiding](../../privacy-service/ui/user-guide.md) voor meer informatie . |
| Oude afleiding van eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is vervangen. |

Bekende problemen

* Geen

Meer informatie over [!DNL Privacy Service], te beginnen met het lezen van de [Overzicht van Privacy Service](../../privacy-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| API- en UI-ondersteuning voor databases | Nieuwe bronschakelaars voor [!DNL Apache Spark] (op HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (op HDInsights), en [!DNL Phoenix]. |
| API- en UI-ondersteuning voor op betalingen gebaseerde toepassingen | Nieuwe bronschakelaars voor [!DNL PayPal]. |
| API- en UI-ondersteuning voor op protocollen gebaseerde toepassingen | Nieuwe bronschakelaars voor [!DNL Generic OData]. |

**Bekende problemen**

* Geen

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
