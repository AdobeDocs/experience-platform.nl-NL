---
title: Opmerkingen bij de release van Adobe Experience Platform Januari 2021
description: Aanvullende informatie van januari 2021 voor Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 27 januari 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Gewone expressiefuncties | [!DNL Data Prep] Mapper ondersteunt nu het zoeken naar overeenkomsten en het extraheren van een deel van het invoerveld op basis van reguliere expressies. |

Voor meer informatie, gelieve te zien het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen**

| Doel | Beschrijving |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] is een Microsoft-oplossing voor objectopslag voor de cloud. |

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Geavanceerde id-overeenkomsten | Verbeteringen aan de mogelijkheden voor de overeenkomende doelgroep in [!DNL Facebook Custom Audiences] en [!DNL Google Customer Match] door ondersteuning toe te voegen voor extra overeenkomende identiteiten, zoals externe id&#39;s, telefoonnummers en id&#39;s van mobiele apparaten. Raadpleeg de volgende documentatie voor meer informatie: <ul><li>[ bestemming van Facebook ](../../destinations/catalog/social/facebook.md)</li><li>[ de Klant van Google Gelijke bestemming ](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[ activeer publieksgegevens aan het stromen segment de uitvoerbestemmingen ](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Meer leren, bezoek het [ overzicht van bestemmingen ](../../destinations/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Met [!DNL Profile] kunt u klantgegevens consolideren in een uniforme weergave die een actionabel, tijdstempelaccount voor elke interactie van de klant biedt.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensset verwijderen uit profielarchief | Wanneer u een dataset van het Meer van Gegevens van het Experience Platform schrapt, zal het automatisch van de opslag van het Profiel eveneens worden geschrapt. U hoeft niet langer het API-eindpunt van de taken van het profielsysteem te gebruiken om een verwijderingsverzoek te doen om de dataset expliciet uit de profielopslag te verwijderen. Voor meer informatie, zie de [ API eindpuntgids van de banen van het profielsysteem ](../../profile/api/profile-system-jobs.md). |
| Geschatte aantal naamruimten van id voor een bepaald segment | De API voor voorvertoning rapporteert nu voor geschatte profielaantallen:<ul><li>Het totale aantal geschatte profielen in een segment voor een bepaalde naamruimte.</li><li>Het totale aantal geschatte profielen in het schema van de Unie van het Profiel voor een bepaalde namespace.</li></ul>Meer leren, verwijs naar de [ API eindpuntgids van de profielvoorproef ](../../profile/api/preview-sample-status.md). |

Voor meer informatie over het Profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, gelieve te beginnen door het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md) te lezen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen voor Adobe Audience Manager-bronaansluiting | U kunt nu individuele eerste-partijsegmenten van Audience Manager aan binnengaan in Platform filteren en selecteren, evenals uit de eigenschappen van de eerste partij filteren. Zie het leerprogramma op [ creërend een Audience Manager bronschakelaar ](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) voor meer informatie. |
| [!DNL Google BigQuery] Verbeteringen aan bronaansluiting | U kunt nu bestanden die groter zijn dan 10 GB in één flowuitvoering opnemen via de [!DNL BigQuery] -bronconnector. Zie het [[!DNL BigQuery]  overzicht van de bronschakelaar ](../../sources/connectors/databases/bigquery.md) voor meer informatie. |
| Ondersteuning voor complexe gegevenstypen voor cloudopslag | U kunt nu complexe gegevenstypen, zoals arrays in JSON-bestanden, opnemen bij gebruik van een bronaansluiting voor cloudopslag. Zie de leerprogramma&#39;s bij het creëren van een dataflow van de wolkenopslag [ in UI ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) of [ gebruikend  [!DNL Flow Service]  API ](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie. |
| Ondersteuning voor service principal key-based authentication for [!DNL Microsoft Dynamics] source | U kunt nu verifiëren aan uw [!DNL Dynamics] rekening gebruikend een de dienstbelangrijkste sleutel als alternatief aan op wachtwoord-gebaseerde authentificatie. Zie het [[!DNL Dynamics]  overzicht van de bronschakelaar ](../../sources/connectors/crm/ms-dynamics.md) voor meer informatie. |
| UI-ondersteuning voor aangepaste scheidingstekens in bronnen voor cloudopslag | U kunt een scheidingsteken van de douanekolom zoals een komma (`,`), lusje (`\t`), of een pijp (`|`) nu plaatsen, om afgebakende dossiers UI te verzamelen. Zie het leerprogramma op [ creërend een dataflow met een de bronschakelaar van de wolkenopslag ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) voor meer informatie |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
