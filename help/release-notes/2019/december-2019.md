---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform van 11 december 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Opmerkingen bij de release Adobe Experience Platform

## Releasedatum: 11 december 2019

## Segmenteringsservice

De Dienst van de Segmentatie van het Platform van de Ervaring van Adobe verstrekt een gebruikersinterface en RESTful API die u toestaat om segmenten te bouwen en publiek van uw gegevens van het Profiel van de Klant in real time te produceren. Deze segmenten worden centraal geconfigureerd en onderhouden op Platform, waardoor ze gemakkelijk toegankelijk zijn voor elke Adobe-toepassing.

De Dienst van de segmentatie bepaalt een bepaalde ondergroep van profielen door de criteria te beschrijven die een verhandelbare groep mensen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

### Nieuwe functies

| Functie | Beschrijving |
|--- | ---|
| Het samengevoegde lusje van het publiek in de Bouwer van het Segment | De tabbladen _Segmenten_ en _Soorten publiek_ in Segment Builder zijn gecombineerd tot één tabblad _Soorten publiek_ . Dit lusje staat u toe om naar bestaand publiek te doorbladeren en te zoeken, dat u dan en in het canvas van de regelbouwer kunt slepen om een nieuwe segmentdefinitie tot stand te brengen. Verwijzen naar een publiek kan één van de volgende reeksen regellogica aan de nieuwe segmentdefinitie toevoegen: Het lidmaatschap van het publiek als regel, de volledige reeks regellogica die het referenced publiek bepaalde. |
| Nieuwe locatie voor de kiezer voor het samenvoegbeleid | De plaats van de selecteur van het fusiebeleid in de Bouwer van het Segment is veranderd. Als u een samenvoegbeleid voor een segmentdefinitie wilt selecteren, klikt u op het tandwielpictogram op het tabblad _Velden_ en gebruikt u het vervolgkeuzemenu Beleid __ samenvoegen om het samenvoegbeleid te selecteren dat u wilt gebruiken. |

### Bekende problemen

* Geen

Voor meer informatie, gelieve te zien het overzicht [van de Dienst van de](../../segmentation/home.md)Segmentatie.

## Beslissingsservice

Met de Adobe Experience Platform Decisioning Service kunt u via programmacode en op intelligente wijze de &quot;Next Best Experience&quot; selecteren uit een set beschikbare opties voor een bepaalde persoon, deze leveren aan een willekeurig kanaal of een willekeurige toepassing en rapportage en analyse uitvoeren.

### Nieuwe functies

| Functie | Beschrijving |
| -----------| ---------- |
| Rangschikkingsfuncties | De volgorde van de aanbiedingen voor profielen wordt nu bepaald door een rangschikkingsfunctie in plaats van een vaste set aanbiedingen voor alle profielen. |

### Bekende problemen

* Geen.

Zie het overzicht [van de Dienst van het](../../decisioning-service/home.md) Beslissen voor een volledige inleiding aan de dienst.

## Bronnen

Met het Adobe Experience Platform kunt u gegevens uit externe bronnen ophalen en tegelijk die gegevens structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe Solutions, cloudopslag, software van derden en uw CRM-systeem.

Het Platform van de ervaring verstrekt RESTful API en een interactieve UI die u bronverbindingen voor diverse gegevensleveranciers met gemak laat opzetten. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

### Nieuwe functies

| Functie | Beschrijving |
| ---------- | ------------ |
| Streaming verbinding | Met streaming opname kunt u gegevens van client- en server-side apparaten naar het Platform verzenden in real-time. Release omvat een nieuwe streamingverbinding, gebruikersinterface. |
| Connectorondersteuning voor Google Cloud Store | Ondersteuning voor het verzamelen van gegevens in de Google Cloud Store. |

### Bekende problemen

* Geen.

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.

## XDM-systeem (Experience Data Model)

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter het ervaringsplatform. Experience Data Model (XDM), aangestuurd door Adobe, is een poging om gegevens over klantervaring te standaardiseren en schema&#39;s voor het beheer van klantervaring te definiëren.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Deze biedt algemene structuren en definities waarmee toepassingen kunnen communiceren met services op het Adobe Experience Platform. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

### Nieuwe functies

| Functie | Beschrijving |
|--- | ---|
| Verbeterde schemavalidatie | Nieuwe controles om ervoor te zorgen dat de verwijzingen in extra gebieden zoals verwacht oplossen. Extra controles toegevoegd aan velden die zijn gedefinieerd als een array van objecten om te controleren of de objecten volledig zijn gedefinieerd. Verbeterde foutmeldingen voor het opsporen en verhelpen van problemen. |

### Bugfixes

* Onderhoud en verbeteringen met betrekking tot toegangsbeheer en sandboxen.
* Steun voor `eTag` het `/descriptors` eindpunt in de Registratie API van het Schema.

### Bekende problemen

* Geen

Meer informatie over het werken met XDM gebruikend de Registratie API van het Schema en gebruikersinterface van de Redacteur van het Schema, gelieve de documentatie [van het](../../xdm/home.md)Systeem XDM te lezen.