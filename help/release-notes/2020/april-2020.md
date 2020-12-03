---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 8 april 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 8 april 2020**

Nieuwe functies in Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Updates voor bestaande functies:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [[!DNL Data Governance]](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] marketinganalisten en praktijkbeoefenaars in staat stellen de kracht van kunstmatige intelligentie en het leren van machines te benutten in gevallen waarin de klant gebruikmaakt van ervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap. Daarnaast kunnen marketingspecialisten voorspellingen activeren in Adobe Experience Cloud, Adobe Experience Platform en toepassingen van derden.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] biedt marketers de mogelijkheid om klantprognoses op individueel niveau te genereren met uitleg. Met behulp van invloedrijke factoren, [!DNL Customer AI] kan u vertellen wat een klant waarschijnlijk zal doen en waarom. Bovendien, kunnen de marketers van [!DNL Customer AI] voorspellingen en inzichten profiteren om klantenervaringen te personaliseren door de meest aangewezen aanbiedingen en overseinen te dienen. |
| [!DNL Attribution AI] | [!DNL Attribution AI] is een multi-channel, algoritmische attributiedienst die de invloed en de stijgende invloed van klanteninteractie tegen gespecificeerde resultaten berekent. Met [!DNL Attribution AI], kunnen de marketers marketing en reclame uitgaven meten en optimaliseren door het effect van elke individuele klanteninteractie over elke fase van de reizen van de klanten te begrijpen. |

**Bekende problemen**

* Momenteel geen bekende problemen.

Voor meer informatie over [!DNL Intelligent Services] en wat het moet aanbieden, zie het [Intelligente Overzicht](../../intelligent-services/home.md)van de Diensten.

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Automatische alternatieve weergave-info | De aangepaste waarden voor titel en beschrijving die in de [!DNL Schema Registry] `alternateDisplayInfo` descriptor zijn geconfigureerd, worden automatisch door de gebruiker toegepast. |
| Beperkingen voor scalaire velden | Het [!DNL Schema Registry] is niet toegestaan meer dan 6000 scalaire gebieden in één enkel schema. |
| Overzicht van prestaties | Het [!DNL Schema Registry] is herzien om te presteren en aan de eisen van [!DNL Experience Platform] betere. |

**Bugfixes**

* Bijgewerkt XDM in XED geconverteerd om een schonere XED formaat voor genestelde gebieden van URI in standaardXDM te steunen.

**Bekende problemen**

* Bekend

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren die op gegevensgebruik van toepassing zijn. Het speelt een sleutelrol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

Aan de slag met gegevensbeheer vereist een grondig inzicht in de verordeningen, de contractuele verplichtingen, en het collectieve beleid die op uw klantengegevens van toepassing zijn. Daarna kunnen gegevens worden geclassificeerd door de juiste labels voor gegevensgebruik toe te passen en kan het gebruik ervan worden geregeld door de definitie van beleid voor gegevensgebruik.

Het [!DNL Data Governance] framework vereenvoudigt en stroomlijnt het proces voor het indelen van gegevens en het maken van beleidsregels voor gegevensgebruik via de [!DNL Experience Platform] gebruikersinterface en de [!DNL Policy Service] API.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Beleid voor gegevensgebruik beheren in de gebruikersinterface | Het beleid voor gegevensgebruik kan nu worden beheerd in de werkruimte **Beleid** in de [!DNL Experience Platform] gebruikersinterface. Zie de gids [van de](../../data-governance/policies/user-guide.md) beleidsgebruiker voor meer informatie. |

**Bekende problemen**

* Geen.

Zie het overzicht [van](../../data-governance/home.md)gegevensbeheer voor meer informatie.


## Doelen {#destinations}

In het Platform [van Gegevens van de Klant in](../../rtcdp/overview.md)real time, zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

CDP in real time steunt nu gegevensactivering aan meer dan vijftig [!DNL Experience Cloud Launch] uitbreidingen, toelatend analyses, verpersoonlijking, en andere gebruiksgevallen. Zie hieronder voor meer informatie:

| Documentatie | Beschrijving |
|--- | ---|
| [Doeltypen en -categorieën](../../destinations/destination-types.md) | Dit artikel verklaart het verschil tussen verbindingen en uitbreidingen in de interface In real time CDP en adviseert wanneer om elk van deze bestemmingen te gebruiken. |
| [Experience Platform Launch-extensies](../../destinations/catalog/launch-extensions/overview.md) | Deze pagina verklaart wat [!DNL Launch] uitbreidingen zijn, maakt een lijst van gebruiksgevallen voor het gebruiken van hen, en verbindingen aan documentatie voor elke [!DNL Launch] uitbreiding in CDP in real time. |

Zie het overzicht [](../../destinations/home.md)Doelen voor meer informatie.

## [!DNL Privacy Service] {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service]kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| PDPA-ondersteuning | De verzoeken van de privacy kunnen nu worden gecreeerd en worden gevolgd onder de Wet van de Bescherming van Persoonlijke Gegevens (PDPA) in Thailand. Wanneer u privacyverzoeken indient in de API, accepteert de `regulation` array de waarde &quot;pdpa_tha&quot;. |
| Naamruimtetypen in de gebruikersinterface | U kunt nu verschillende naamruimtetypen opgeven in de [!DNL Privacy Service] gebruikersinterface van Request Builder. Raadpleeg de [gebruikershandleiding](../../privacy-service/ui/user-guide.md) voor meer informatie. |
| Oude afleiding van eindpunt | Het oude API-eindpunt (`data/privacy/gdpr`) is vervangen. |

Bekende problemen

* Geen

Voor meer informatie over [!DNL Privacy Service], gelieve te beginnen door het overzicht [van de](../../privacy-service/home.md)Privacy Service te lezen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| API- en UI-ondersteuning voor databases | Nieuwe bronconnectors voor [!DNL Apache Spark] (op HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (op HDInsights) en [!DNL Phoenix]. |
| API- en UI-ondersteuning voor op betalingen gebaseerde toepassingen | Nieuwe bronschakelaars voor [!DNL PayPal]. |
| API- en UI-ondersteuning voor op protocollen gebaseerde toepassingen | Nieuwe bronschakelaars voor [!DNL Generic OData]. |

**Bekende problemen**

* Geen

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.
