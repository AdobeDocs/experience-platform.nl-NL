---
title: Opmerkingen bij de release van Adobe Experience Platform Januari 2021
description: Opmerkingen bij de release van januari 2021 voor Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '717'
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

Zie voor meer informatie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] is Microsoft-oplossing voor objectopslag voor de cloud. |

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Geavanceerde id-overeenkomsten | Verbeteringen aan de mogelijkheden van de publieksovereenkomst op het gebied van [!DNL Facebook Custom Audiences] en [!DNL Google Customer Match]door ondersteuning toe te voegen voor extra overeenkomende identiteiten, zoals externe id&#39;s, telefoonnummers en mobiele apparaat-id&#39;s. Raadpleeg de volgende documentatie voor meer informatie: <ul><li>[Facebook-bestemming](../../destinations/catalog/social/facebook.md)</li><li>[Google Customer Match-bestemming](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Ga voor meer informatie naar de [Overzicht van doelen](../../destinations/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensset verwijderen uit profielarchief | Wanneer u een dataset van het Meer van Gegevens van het Experience Platform schrapt, zal het automatisch van de opslag van het Profiel eveneens worden geschrapt. U hoeft niet langer het API-eindpunt van de taken van het profielsysteem te gebruiken om een verwijderingsverzoek te doen om de dataset expliciet uit de profielopslag te verwijderen. Zie voor meer informatie de [API-eindgids voor profielsysteemtaken](../../profile/api/profile-system-jobs.md). |
| Geschatte aantal naamruimten van id voor een bepaald segment | De API voor voorvertoning rapporteert nu voor geschatte profielaantallen:<ul><li>Het totale aantal geschatte profielen in een segment voor een bepaalde naamruimte.</li><li>Het totale aantal geschatte profielen in het schema van de Unie van het Profiel voor een bepaalde namespace.</li></ul>Raadpleeg voor meer informatie de [API-eindhulplijn voor profielvoorvertoning](../../profile/api/preview-sample-status.md). |

Voor meer informatie over het profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] om te beginnen met het lezen van de [Overzicht van het realtime klantprofiel](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen voor Adobe Audience Manager-bronaansluiting | U kunt nu individuele eerste-partijsegmenten van Audience Manager aan binnengaan in Platform filteren en selecteren, evenals uit de eigenschappen van de eerste partij filteren. Zie de zelfstudie aan [een Audience Manager-bronaansluiting maken](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) voor meer informatie . |
| [!DNL Google BigQuery] verbetering bronaansluiting | U kunt nu bestanden die groter zijn dan 10 GB in één flowuitvoering opnemen met de opdracht [!DNL BigQuery] bronaansluiting. Zie de [[!DNL BigQuery] overzicht van de bronaansluiting](../../sources/connectors/databases/bigquery.md) voor meer informatie . |
| Ondersteuning voor complexe gegevenstypen voor cloudopslag | U kunt nu complexe gegevenstypen, zoals arrays in JSON-bestanden, opnemen bij gebruik van een bronaansluiting voor cloudopslag. Bekijk de zelfstudies over het maken van een gegevensstroom voor cloudopslag [in de gebruikersinterface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) of [met de [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie . |
| Steun voor de dienst belangrijkste op sleutel-gebaseerde authentificatie voor [!DNL Microsoft Dynamics] bron | U kunt nu verifiëren voor uw [!DNL Dynamics] account die een service principal-sleutel gebruikt als alternatief voor op een wachtwoord gebaseerde verificatie. Zie de [[!DNL Dynamics] overzicht van de bronaansluiting](../../sources/connectors/crm/ms-dynamics.md) voor meer informatie . |
| UI-ondersteuning voor aangepaste scheidingstekens in bronnen voor cloudopslag | U kunt nu een aangepast kolomscheidingsteken instellen, zoals een komma (`,`), tab (`\t`) of een pijp (`|`), om gescheiden bestanden te verzamelen in de interface. Zie de zelfstudie aan [een gegevensstroom maken met de bronaansluiting voor cloudopslag](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) voor meer informatie |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
