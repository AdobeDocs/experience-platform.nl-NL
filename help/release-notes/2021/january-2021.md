---
title: 'Aanvullende informatie van januari 2021 voor Adobe Experience Platform '
description: Aanvullende informatie van januari 2021 voor Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 26%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 27 januari 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Gewone expressiefuncties | [!DNL Data Prep] Mapper ondersteunt nu het zoeken naar overeenkomsten en het extraheren van een deel van het invoerveld op basis van reguliere expressies. |

Voor meer informatie, gelieve te zien het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] is een Microsoft-oplossing voor objectopslag voor de cloud. |

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Geavanceerde id-overeenkomsten | Verbeteringen aan de mogelijkheden voor de overeenkomende doelgroep in [!DNL Facebook Custom Audiences] en [!DNL Google Customer Match] door ondersteuning toe te voegen voor extra overeenkomende identiteiten, zoals externe id&#39;s, telefoonnummers en id&#39;s van mobiele apparaten. Raadpleeg de volgende documentatie voor meer informatie: <ul><li>[ bestemming Facebook ](../../destinations/catalog/social/facebook.md)</li><li>[ de Klant van Google Gelijke bestemming ](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[ activeer publieksgegevens aan het stromen segment de uitvoerbestemmingen ](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Meer leren, bezoek het [ overzicht van bestemmingen ](../../destinations/home.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met [!DNL Profile] kunt u klantgegevens consolideren in een uniforme weergave die een actionabel, tijdstempelaccount voor elke interactie van de klant biedt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Gegevensset verwijderen uit profielarchief | Wanneer u een dataset van het meer van Gegevens van Experience Platform schrapt, zal het automatisch van de opslag van het Profiel eveneens worden geschrapt. U hoeft niet langer het API-eindpunt van de taken van het profielsysteem te gebruiken om een verwijderingsverzoek te doen om de dataset expliciet uit de profielopslag te verwijderen. Voor meer informatie, zie de [ API eindpuntgids van de banen van het profielsysteem ](../../profile/api/profile-system-jobs.md). |
| Geschatte aantal naamruimten van id voor een bepaald segment | De API voor voorvertoning rapporteert nu voor geschatte profielaantallen:<ul><li>Het totale aantal geschatte profielen in een segment voor een bepaalde naamruimte.</li><li>Het totale aantal geschatte profielen in het schema van de Unie van het Profiel voor een bepaalde namespace.</li></ul>Meer leren, verwijs naar de [ API eindpuntgids van de profielvoorproef ](../../profile/api/preview-sample-status.md). |

Voor meer informatie over het Profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, gelieve te beginnen door het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md) te lezen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen voor Adobe Audience Manager-bronaansluiting | U kunt nu afzonderlijke eerste-partijsegmenten van Audience Manager filteren en selecteren om in Experience Platform in te voeren, en de eerste-partijkenmerken filteren. Zie het leerprogramma op [ creërend een bron van Audience Manager schakelaar ](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) voor meer informatie. |
| [!DNL Google BigQuery] Verbeteringen aan bronaansluiting | U kunt nu bestanden die groter zijn dan 10 GB in één flowuitvoering opnemen via de [!DNL BigQuery] -bronconnector. Zie het [[!DNL BigQuery]  overzicht van de bronschakelaar ](../../sources/connectors/databases/bigquery.md) voor meer informatie. |
| Ondersteuning voor complexe gegevenstypen voor cloudopslag | U kunt nu complexe gegevenstypen, zoals arrays in JSON-bestanden, opnemen bij gebruik van een bronaansluiting voor cloudopslag. Zie de leerprogramma&#39;s bij het creëren van een dataflow van de wolkenopslag [ in UI ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) of [ gebruikend  [!DNL Flow Service]  API ](../../sources/tutorials/api/collect/cloud-storage.md) voor meer informatie. |
| Ondersteuning voor service principal key-based authentication for [!DNL Microsoft Dynamics] source | U kunt nu verifiëren aan uw [!DNL Dynamics] rekening gebruikend een de dienstbelangrijkste sleutel als alternatief aan op wachtwoord-gebaseerde authentificatie. Zie het [[!DNL Dynamics]  overzicht van de bronschakelaar ](../../sources/connectors/crm/ms-dynamics.md) voor meer informatie. |
| UI-ondersteuning voor aangepaste scheidingstekens in bronnen voor cloudopslag | U kunt een scheidingsteken van de douanekolom zoals een komma (`,`), lusje (`\t`), of een pijp (`|`) nu plaatsen, om afgebakende dossiers UI te verzamelen. Zie het leerprogramma op [ creërend een dataflow met een de bronschakelaar van de wolkenopslag ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) voor meer informatie |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
