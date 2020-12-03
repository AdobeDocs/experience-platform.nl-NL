---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 15 januari 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '880'
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
| Beperkingen van veldtype voor velden met gelijke hiërarchie | Nadat een XDM-veld is gedefinieerd als een bepaald type, moeten andere velden met dezelfde naam en hiërarchie hetzelfde veldtype gebruiken, ongeacht de klassen of mixen waarin ze worden gebruikt. Als een mixin voor de XDM- [!DNL Profile] klasse bijvoorbeeld een `profile.age` veld van het type &quot;integer&quot; bevat, [!DNL ExperienceEvent] kan een vergelijkbare mix voor XDM geen `profile.age` veld van het type &quot;string&quot; hebben. Als u een ander veldtype wilt gebruiken, moet het veld een andere hiërarchie hebben dan het eerder gedefinieerde veld (bijvoorbeeld `profile.person.age`). Deze functie is bedoeld om conflicten te voorkomen wanneer schema&#39;s in een unie worden samengebracht. Hoewel de beperking geen retroactief effect heeft op bestaande schema&#39;s, wordt sterk geadviseerd dat u uw schema&#39;s voor field-type conflicten herziet en hen zonodig uitgeeft. |
| Hoofdlettergevoelige veldvalidatie | Aangepaste velden op hetzelfde niveau moeten verschillende namen hebben, ongeacht het hoofdlettergebruik. Als u bijvoorbeeld een aangepast veld met de naam &quot;E-mail&quot; toevoegt, kunt u geen ander aangepast veld op hetzelfde niveau met de naam &quot;e-mail&quot; toevoegen. |

**Bekende problemen**

* Geen

Meer informatie over het werken met XDM die API en [!DNL Schema Registry] gebruikersinterface gebruikt, te lezen gelieve de documentatie [!DNL Schema Editor] van het [](../../xdm/home.md)Systeem XDM.

## [!DNL Privacy Service] {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service]kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| [!DNL Privacy Service] herbranding | De voormalige naam &quot;GDPR Service&quot; is omgedoopt [!DNL Privacy Service] omdat de dienst is gegroeid om andere regels naast GDPR te ondersteunen. |
| Nieuwe API-eindpunten | Het basispad voor de [!DNL Privacy Service] API is bijgewerkt van `/data/privacy/gdpr` naar `/data/core/privacy/jobs`. |
| Nieuwe vereiste `regulation` eigenschap | Bij het maken van nieuwe taken in de [!DNL Privacy Service] API moet een `regulation` eigenschap worden opgegeven in de payload van de aanvraag om aan te geven welke regelgeving moet worden gebruikt om de taak onder te volgen. Accepteerde waarden zijn `gdpr` en `ccpa`. |
| Ondersteuning voor [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] Accepteert nu toegang/schrappingsverzoeken van Adobe [!DNL Primetime Authentication], die `primetimeAuthentication` als zijn productwaarde gebruiken. |
| Verbeteringen in de gebruikersinterface van Privacy Service | Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen. Nieuw **Type verordening **dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen. |

**Bekende problemen**

* Geen

Voor meer informatie over [!DNL Privacy Service], gelieve te beginnen door het overzicht [van de](../../privacy-service/home.md)Privacy Service te lezen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

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
| Gegevensinname | Bronnen weergeven | Alleen-lezen toegang tot beschikbare bronnen op het tabblad **[!UICONTROL Catalogus]** en geverifieerde bronnen op het tabblad **[!UICONTROL Bladeren]** . |

**Bekende problemen**

* Geen

Voor meer informatie over bronnen, zie het [bronoverzicht](../../sources/home.md)

## Doelen {#destinations}

In [real time CDP](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor toegangsbeheermachtigingen | De functionaliteit van Doelen in Echt - tijd CDP werkt met de toegangsbeheertoestemmingen van Adobe Experience Platform. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. |

**Toegangsbeheermachtigingen**

| Categorie | Machtiging | Beschrijving |
|--- | --- | ---|
| Doelen | Doelen beheren | Toegang tot het lezen, creëren, uitgeven, en onbruikbaar maken bestemmingen. |
| Doelen | Doelen weergeven | Alleen-lezen toegang tot beschikbare doelen op het tabblad **[!UICONTROL Catalogus]** en geverifieerde doelen op het tabblad **Bladeren** . |
| Doelen | Doelen activeren | Mogelijkheid om gegevens naar doelen te activeren. Voor deze machtiging moet &quot;Doelen beheren&quot; of &quot;Doelen weergeven&quot; worden toegevoegd aan het productprofiel. |

**Bekende problemen**

* Geen

Zie het overzicht [](../../destinations/home.md) Doelen voor meer informatie.