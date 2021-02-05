---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 27 januari 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 2e3a6acbfaa7f733a9843068c00f31f0b7f535b6
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 januari 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Sources]](#sources)
- [[!DNL Experience Platform Launch Server Side]](#launch)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Gewone expressiefuncties | [!DNL Data Prep] Mapper ondersteunt nu het zoeken naar overeenkomsten en het extraheren van een deel van het invoerveld op basis van reguliere expressies. |

Zie [[!DNL Data Prep] overzicht](../../data-prep/home.md) voor meer informatie.

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] is de objectopslagoplossing van Microsoft voor de cloud. |

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Geavanceerde id-overeenkomsten | De verhogingen aan de mogelijkheden van de publieksverhouding in [!DNL Facebook Custom Audiences] en [!DNL Google Customer Match], door steun voor extra identiteitsaanpassing, zoals externe IDs, telefoonaantallen, en mobiele apparaat IDs toe te voegen. Raadpleeg de volgende documentatie voor meer informatie: <ul><li>[Facebook-bestemming](../../destinations/catalog/social/facebook.md)</li><li>[Google Customer Match-bestemming](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Profielen en segmenten naar een doel activeren](../../destinations/ui/activate-destinations.md)</li></ul> |

Voor meer informatie gaat u naar [bestemmingen overview](../../destinations/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen voor Adobe Audience Manager-bronaansluiting | U kunt nu individuele eerste-partijsegmenten van Audience Manager aan binnengaan in Platform filteren en selecteren, evenals uit de eigenschappen van de eerste partij filteren. Zie de zelfstudie op [het creëren van een Audience Manager bronschakelaar](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) voor meer informatie. |
| [!DNL Google BigQuery] verbetering bronaansluiting | U kunt nu bestanden die groter zijn dan 10 GB in één flowuitvoering opnemen met de bronconnector [!DNL BigQuery]. Zie [[!DNL BigQuery] overzicht van de bronconnector](../../sources/connectors/databases/bigquery.md) voor meer informatie. |
| Ondersteuning voor complexe gegevenstypen voor cloudopslag | U kunt nu complexe gegevenstypen, zoals arrays in JSON-bestanden, opnemen bij gebruik van een bronaansluiting voor cloudopslag. Zie de zelfstudies over het maken van een gegevensstroom voor cloudopslag [in de interface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) of [met de API [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie. |
| Ondersteuning voor service principal key-based authentication for [!DNL Microsoft Dynamics] source | U kunt nu verifiëren aan uw [!DNL Dynamics] rekening gebruikend een de dienstbelangrijkste sleutel als alternatief aan op wachtwoord-gebaseerde authentificatie. Zie [[!DNL Dynamics] overzicht van de bronconnector](../../sources/connectors/crm/ms-dynamics.md) voor meer informatie. |
| UI-ondersteuning voor aangepaste scheidingstekens in bronnen voor cloudopslag | U kunt een scheidingsteken van de douanekolom zoals een komma (`,`), lusje (`\t`), of een pijp (`|`) nu plaatsen, om afgebakende dossiers in UI te verzamelen. Zie de zelfstudie over [het maken van een gegevensstroom met een bronaansluiting voor cloudopslag](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) voor meer informatie |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).

## [!DNL Experience Platform Launch Server Side] {#launch}

Met Adobe Experience Platform Launch Server Side wordt de webpagina en het gewicht van de app verminderd doordat Adobe Experience Platform Edge Network wordt gebruikt om taken uit te voeren die normaal op de client worden uitgevoerd. De Zijregels van de Server van de Lancering van het Platform kunnen gegevens transformeren en verzenden naar nieuwe bestemmingen zonder cliënt-zijimplementaties te veranderen.

De Zijde van de Server van de Lancering van het Platform, in combinatie met het Web van Adobe Experience Platform en Mobiele SDKs, maakt het mogelijk om:

- Maak één enkele vraag van de pagina die een nuttige lading van gegevens bevat en dan dit gegeven server-kant federeert om cliënt-zijnetwerkverkeer te verminderen en een snellere ervaring voor klanten te leveren.
- Verlaag de tijd die het duurt voordat webpagina&#39;s worden geladen, zodat uw site voldoet aan de best practices van de branche op het gebied van prestaties.
- Verhoog de transparantie en controleer op welke gegevenstypen waar en voor alle eigenschappen aan de clientzijde worden verzonden.
- Maak een serverregel om eerder bijgehouden gegevens naar een nieuwe bestemming te verzenden.

Raadpleeg de documentatie [Platform starten](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html?lang=en) voor meer informatie.