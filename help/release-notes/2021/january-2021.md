---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 27 januari 2021
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 18712835b2408b24cd2735b19c94bf1b1fe50df1
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 januari 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

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

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensset verwijderen uit profielarchief | Wanneer u een dataset van het Meer van Gegevens van het Experience Platform schrapt, zal het automatisch van de opslag van het Profiel eveneens worden geschrapt. U hoeft niet langer het API-eindpunt van de taken van het profielsysteem te gebruiken om een verwijderingsverzoek te doen om de dataset expliciet uit de profielopslag te verwijderen. Voor meer informatie, zie [API eindgids van de banen van het profielsysteem van banenAPI](../../profile/api/profile-system-jobs.md). |
| Geschatte aantal naamruimten van id voor een bepaald segment | De API voor voorvertoning rapporteert nu voor geschatte profielaantallen:<ul><li>Het totale aantal geschatte profielen in een segment voor een bepaalde naamruimte.</li><li>Het totale aantal geschatte profielen in het schema van de Unie van het Profiel voor een bepaalde namespace.</li></ul>Voor meer informatie raadpleegt u de [API-eindpunthulplijn voor voorvertoning van profiel](../../profile/api/preview-sample-status.md). |

Voor meer informatie over het profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, gelieve te beginnen door [Overzicht van het Profiel van de Klant in real time](../../profile/home.md) te lezen.

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
