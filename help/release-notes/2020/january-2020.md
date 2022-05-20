---
title: Opmerkingen bij de release van Adobe Experience Platform Januari 2020
description: Opmerkingen bij de release januari 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 15 januari 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Beperkingen van veldtype voor velden met gelijke hiërarchie | Nadat een XDM-veld is gedefinieerd als een bepaald type, moeten andere velden met dezelfde naam en hiërarchie hetzelfde veldtype gebruiken, ongeacht de klassen of groepen schemavelden waarin ze worden gebruikt. Als een veldgroep bijvoorbeeld voor de XDM [!DNL Profile] klasse bevat een `profile.age` veld van het type &quot;integer&quot;, een vergelijkbare veldgroep voor XDM [!DNL ExperienceEvent] kan geen `profile.age` veld van het type &quot;string&quot;. Als u een ander veldtype wilt gebruiken, moet het veld een andere hiërarchie hebben dan het eerder gedefinieerde veld (bijvoorbeeld `profile.person.age`). Deze functie is bedoeld om conflicten te voorkomen wanneer schema&#39;s in een unie worden samengebracht. Hoewel de beperking geen retroactief effect heeft op bestaande schema&#39;s, wordt sterk geadviseerd dat u uw schema&#39;s voor field-type conflicten herziet en hen zonodig uitgeeft. |
| Hoofdlettergevoelige veldvalidatie | Aangepaste velden op hetzelfde niveau moeten verschillende namen hebben, ongeacht het hoofdlettergebruik. Als u bijvoorbeeld een aangepast veld met de naam &quot;E-mail&quot; toevoegt, kunt u geen ander aangepast veld op hetzelfde niveau met de naam &quot;e-mail&quot; toevoegen. |

**Bekende problemen**

* Geen

Meer informatie over het werken met XDM [!DNL Schema Registry] API en [!DNL Schema Editor] gebruikersinterface, lees de [XDM System-documentatie](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful API en een gebruikersinterface om u te helpen deze gegevensverzoeken van uw klanten beheren. Met [!DNL Privacy Service]kunt u verzoeken om toegang tot persoonlijke of persoonlijke klantgegevens van Adobe Experience Cloud-toepassingen en deze verwijderen, zodat u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| [!DNL Privacy Service] herbranding | De voormalige naam &quot;GDPR Service&quot; is hernoemd naar [!DNL Privacy Service] aangezien de dienst is gegroeid om andere voorschriften naast de GDPR te ondersteunen. |
| Nieuwe API-eindpunten | Basispad voor de [!DNL Privacy Service] API is bijgewerkt vanaf `/data/privacy/gdpr` tot `/data/core/privacy/jobs`. |
| Nieuw vereist `regulation` eigenschap | Wanneer u nieuwe taken maakt in het dialoogvenster [!DNL Privacy Service] API, a `regulation` de goederen moeten in de lading van het verzoek worden geleverd om aan te geven welke regeling moet worden toegepast om de functie onder te houden. Accepteerde waarden zijn `gdpr` en `ccpa`. |
| Ondersteuning voor [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] Accepteert nu toegang/schrappingsverzoeken van Adobe [!DNL Primetime Authentication], gebruiken `primetimeAuthentication` als productwaarde. |
| Verbeteringen in de gebruikersinterface van Privacy Service | Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen. Nieuw **Type verordening **dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen. |

**Bekende problemen**

* Geen

Meer informatie over [!DNL Privacy Service], te beginnen met het lezen van de [Overzicht van Privacy Service](../../privacy-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor kenmerkgegevens van klanten | UI- en API-ondersteuning voor het maken van streaming-connectors om klantkenmerkgegevens in te voeren. |
| Extra ondersteuning voor bestandsindelingen voor cloudopslagsystemen | Bestandsinvoer uit cloudopslagsystemen ondersteunt nu XDM-compatibele Parquet- en JSON-bestandsindelingen. |
| Ondersteuning voor toegangsbeheermachtigingen | Het toegangsbeheerkader in Adobe Experience Platform verstrekt de toestemmingen nodig om toegang tot bronnen in gegevensopname te verlenen. Afhankelijk van hun toestemmingsniveau, kan een gebruiker bronnen bekijken, bronnen beheren, of toegang volledig worden ontzegd. |

**Toegangsbeheermachtigingen**

| Categorie | Machtiging | Beschrijving |
|--- | --- | ---|
| Gegevensinname | Bronnen beheren | Toegang tot het lezen, maken, bewerken en uitschakelen van bronnen. |
| Gegevensinname | Bronnen weergeven | Alleen-lezen toegang tot beschikbare bronnen in het dialoogvenster **[!UICONTROL Catalog]** tabblad en geverifieerde bronnen in het dialoogvenster **[!UICONTROL Browse]** tab. |

**Bekende problemen**

* Geen

Voor meer informatie over bronnen raadpleegt u de [overzicht van bronnen](../../sources/home.md)

## Doelen {#destinations}

In [Real-time CDP](../../rtcdp/overview.md), zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor toegangsbeheermachtigingen | De functionaliteit van Doelen in Echt - tijd CDP werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. |

**Toegangsbeheermachtigingen**

| Categorie | Machtiging | Beschrijving |
|--- | --- | ---|
| Doelen | Doelen beheren | Toegang tot het lezen, creëren, uitgeven, en onbruikbaar maken bestemmingen. |
| Doelen | Doelen weergeven | Alleen-lezen toegang tot beschikbare doelen in de **[!UICONTROL Catalog]** tab en geverifieerde doelen in het dialoogvenster **Bladeren** tab. |
| Doelen | Doelen activeren | Mogelijkheid om gegevens naar doelen te activeren. Voor deze machtiging moet &quot;Doelen beheren&quot; of &quot;Doelen weergeven&quot; worden toegevoegd aan het productprofiel. |

**Bekende problemen**

* Geen

Zie de [Overzicht van doelen](../../destinations/home.md) voor meer informatie .
