---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform van 8 april 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 3f3704cc1e11a4d11278a34800c8bfdc24a80753

---


# Opmerkingen bij de release Adobe Experience Platform

## Releasedatum: 8 april 2020

## Intelligente services

Intelligente services stellen marketinganalisten en praktijkmensen in staat om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen van de klantervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap. Daarnaast kunnen marketingprofessionals voorspellingen activeren in Adobe Experience Cloud, Adobe Experience Platform en toepassingen van derden.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|---|---|
| Customer AI | Klantenservice-AI biedt marketers de mogelijkheid om voorspellingen van klanten op individueel niveau te genereren met uitleg. Met behulp van invloedrijke factoren kan de AI van de Klant u vertellen wat een klant waarschijnlijk zal doen en waarom. Bovendien kunnen marketers profiteren van de voorspellingen en inzichten van de klant van AI om de ervaringen van klanten aan te passen door de meest geschikte aanbiedingen en berichten te bedienen. |
| Attributie-AI | Attribution AI is een multi-channel, algoritmische attributiedienst die de invloed en de incrementele impact van klanteninteractie tegen gespecificeerde resultaten berekent. Met Attribution AI kunnen marketers marketing- en advertentiekosten meten en optimaliseren door de impact van elke afzonderlijke interactie van de klant in elke fase van de reizen van de klant te begrijpen. |

**Bekende problemen**

* Momenteel geen bekende problemen.

Voor meer informatie over de Intelligente Diensten en wat het moet aanbieden, zie het Overzicht [van de](../../intelligent-services/home.md)Intelligente Diensten.

## Privacy Service

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

## Bronnen

Met het Adobe Experience Platform kunt u gegevens uit externe bronnen ophalen en tegelijk die gegevens structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Het Platform van de ervaring verstrekt RESTful API en een interactieve UI die u bronverbindingen voor diverse gegevensleveranciers met gemak laat opzetten. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

### Nieuwe functies

| Functie | Beschrijving |
| ------- | ----------- |
| API- en UI-ondersteuning voor databases | Nieuwe bronaansluitingen voor Apache Spark (op HDInsights), Azure Synapse Analytics, Azure Table Storage, Hive (op HDInsights) en Phoenix. |
| API- en UI-ondersteuning voor op betalingen gebaseerde toepassingen | Nieuwe bronconnectors voor PayPal. |
| API- en UI-ondersteuning voor op protocollen gebaseerde toepassingen | Nieuwe bronconnectors voor Generic OData. |

### Bekende problemen

* Geen

Zie het [bronoverzicht](../../source-connectors/home.md)voor meer informatie over bronnen.

<!-- ## Access control

Experience Platform leverages [Adobe Admin Console](https://adminconsole.adobe.com) product profiles to link users with permissions and sandboxes. Permissions control access to a variety of Platform capabilities, including data modeling, profile management, and sandbox administration.

### Key features

|Feature | Description|
|--- | ---|
|Permissions | In the Admin Console, the _Permissions_ tab within a Platform product profile allows you customize which Platform capabilities are available for the users attached to that profile. Available permission categories include: Data Modeling, Data Management, Profile Management, Identities, Data Monitoring, Sandbox Administration, Destinations, Sources.|
|Access to sandboxes | The _Permissions_ tab within a Platform product profile can grant users access to specific sandboxes. See the section on [sandboxes](#sandboxes) below for more information.|

For more information, please see the [access control overview](../../access-control/home.md).

## Sandboxes

Experience Platform is built to enrich digital experience applications on a global scale. Companies often run multiple digital experience applications in parallel and need to cater for the development, testing, and deployment of these applications while ensuring operational compliance. In order to address this need, Experience Platform provides sandboxes which partition a single Platform instance into separate virtual environments to help develop and evolve digital experience applications.

### Key features

|Feature | Description|
|--- | ---|
|Production sandbox | Experience Platform provides a single production sandbox, which cannot be deleted or reset.|
|Non-production sandboxes | Multiple non-production sandboxes can be created for a single Platform instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox.|
|Sandbox switcher | In the Experience Platform user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu.|
|`x-sandbox-name` header | All calls to Experience Platform APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in.|

For more information, please see the [sandboxes overview](../../sandboxes/home.md). -->