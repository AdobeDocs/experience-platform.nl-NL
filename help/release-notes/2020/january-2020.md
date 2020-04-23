---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform op 15 januari 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 5199a344a66381ef9d7eea1ea8314e5de7152e3b

---


# Opmerkingen bij de release Adobe Experience Platform

## Releasedatum: 15 januari 2020

Updates voor bestaande functies in het Adobe Experience Platform:

* [XDM-systeem (Experience Data Model)](#xdm)
* [Privacy Service](#privacy)
* [Bronnen](#sources)
* [Doelen](#destinations)

## XDM-systeem (Experience Data Model) {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter het ervaringsplatform. Experience Data Model (XDM), aangestuurd door Adobe, is een poging om gegevens over klantervaring te standaardiseren en schema&#39;s voor het beheer van klantervaring te definiëren.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Deze biedt algemene structuren en definities waarmee toepassingen kunnen communiceren met services op het Adobe Experience Platform. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Beperkingen van veldtype voor velden met gelijke hiërarchie | Nadat een XDM-veld is gedefinieerd als een bepaald type, moeten andere velden met dezelfde naam en hiërarchie hetzelfde veldtype gebruiken, ongeacht de klassen of mixen waarin ze worden gebruikt. Als een mixin voor de klasse XDM Profile bijvoorbeeld een veld van het type &quot;integer&quot; bevat, kan een vergelijkbare mix voor XDM ExperienceEvent geen `profile.age` `profile.age` veld van het type &quot;string&quot; hebben. Als u een ander veldtype wilt gebruiken, moet het veld een andere hiërarchie hebben dan het eerder gedefinieerde veld (bijvoorbeeld `profile.person.age`). Deze functie is bedoeld om conflicten te voorkomen wanneer schema&#39;s in een unie worden samengebracht. Hoewel de beperking geen retroactief effect heeft op bestaande schema&#39;s, wordt sterk geadviseerd dat u uw schema&#39;s voor field-type conflicten herziet en hen zonodig uitgeeft. |
| Hoofdlettergevoelige veldvalidatie | Aangepaste velden op hetzelfde niveau moeten verschillende namen hebben, ongeacht het hoofdlettergebruik. Als u bijvoorbeeld een aangepast veld met de naam &quot;E-mail&quot; toevoegt en hieraan een aangepaste waarde toevoegt, kunt u geen ander aangepast veld op hetzelfde niveau met de naam &quot;e-mail&quot; toevoegen. |

**Bekende problemen**

* Geen

Meer informatie over het werken met XDM gebruikend de Registratie API van het Schema en gebruikersinterface van de Redacteur van het Schema, gelieve de documentatie [van het](../../xdm/home.md)Systeem XDM te lezen.

## Privacy Service {#privacy}

De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek. Adobe Experience Platform Privacy Service biedt een RESTful API en een gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met de Privacy Service kunt u verzoeken om toegang tot persoonlijke of persoonlijke klantgegevens van Adobe Experience Cloud-toepassingen en deze verwijderen. Zo kunt u de automatische naleving van wettelijke en organisatorische privacyregels vereenvoudigen.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Privacy Service opnieuw brandmerken | De voormalige naam &quot;GDPR Service&quot; is omgedoopt tot Privacy Service, aangezien de dienst is gegroeid om andere regels naast GDPR te ondersteunen. |
| Nieuwe API-eindpunten | Het basispad voor de Privacy Service API is bijgewerkt van `/data/privacy/gdpr` naar `/data/core/privacy/jobs`. |
| Nieuwe vereiste `regulation` eigenschap | Bij het creëren van nieuwe banen in de Dienst API van de Privacy, moet een `regulation` bezit in de verzoeklading worden geleverd om te wijzen op welke verordening om de baan onder te volgen. Accepteerde waarden zijn `gdpr` en `ccpa`. |
| Ondersteuning voor Adobe Primetime-verificatie | De privacyservice accepteert nu aanvragen voor toegang tot/verwijdering van Adobe Primetime-verificatie, die `primetimeAuthentication` als productwaarde worden gebruikt. |
| Verbeteringen in de gebruikersinterface van de privacyservice | Afzonderlijke pagina&#39;s voor het volgen van taken voor GDPR en CCPA verordeningen. Het nieuwe _Regeltype_ dropdown om tussen het volgen gegevens voor GDPR en CCPA te schakelen. |

**Bekende problemen**

* Geen

Voor meer informatie over de Dienst van de Privacy, gelieve te beginnen door het overzicht [van de Dienst van de](../../privacy-service/home.md)Privacy te lezen.

## Bronnen {#sources}

Met het Adobe Experience Platform kunt u gegevens uit externe bronnen ophalen en tegelijk die gegevens structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Het Platform van de ervaring verstrekt RESTful API en een interactieve UI die u bronverbindingen voor diverse gegevensleveranciers met gemak laat opzetten. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor kenmerkgegevens van klanten | UI- en API-ondersteuning voor het maken van streaming-connectors om klantkenmerkgegevens in te voeren. |
| Extra ondersteuning voor bestandsindelingen voor cloudopslagsystemen | Bestandsinvoer uit cloudopslagsystemen ondersteunt nu XDM-compatibele Parquet- en JSON-bestandsindelingen. |
| Ondersteuning voor toegangsbeheermachtigingen | Het toegangsbeheerframework in het Adobe Experience Platform biedt de machtigingen die nodig zijn om toegang te verlenen tot bronnen bij het invoeren van gegevens. Afhankelijk van hun toestemmingsniveau, kan een gebruiker bronnen bekijken, bronnen beheren, of toegang volledig worden ontzegd. |

**Toegangsbeheermachtigingen**

| Categorie | Machtiging | Beschrijving |
|--- | --- | ---|
| Gegevensinname | Bronnen beheren | Toegang tot het lezen, maken, bewerken en uitschakelen van bronnen. |
| Gegevensinname | Bronnen weergeven | Alleen-lezen toegang tot beschikbare bronnen op het tabblad *Catalogus* en geverifieerde bronnen op het tabblad *Bladeren* . |

**Bekende problemen**

* Geen

Voor meer informatie over bronnen, zie het [bronoverzicht](../../sources/home.md)

## Doelen {#destinations}

In [Adobe real-time CDP](../../rtcdp/overview.md), zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Ondersteuning voor toegangsbeheermachtigingen | De functionaliteit Doelen in CDP In real time werkt met de toegangsbeheertoestemmingen van het Platform van de Ervaring van Adobe. Afhankelijk van het machtigingsniveau van uw gebruiker, kunt u bestemmingen bekijken, beheren en activeren. |

**Toegangsbeheermachtigingen**

| Categorie | Machtiging | Beschrijving |
|--- | --- | ---|
| Doelen | Doelen beheren | Toegang tot het lezen, creëren, uitgeven, en onbruikbaar maken bestemmingen. |
| Doelen | Doelen weergeven | Alleen-lezen toegang tot beschikbare doelen op het tabblad _Catalogus_ en geverifieerde doelen op het tabblad _Bladeren_ . |
| Doelen | Doelen activeren | Mogelijkheid om gegevens naar doelen te activeren. Voor deze machtiging moet &quot;Doelen beheren&quot; of &quot;Doelen weergeven&quot; worden toegevoegd aan het productprofiel. |

**Bekende problemen**

* Geen

Zie het overzicht [](../../rtcdp/destinations/destinations-overview.md) Doelen voor meer informatie.