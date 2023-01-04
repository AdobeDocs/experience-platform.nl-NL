---
title: Opmerkingen bij de release van Adobe Experience Platform, oktober 2020
description: In de release van oktober 2020 staat een opmerking voor Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 14 oktober 2020**

- [Gegevensprep](#data-prep)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)
- [Tijd tot waarde](#time-to-value)

## Gegevensprep {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| `is_set` -functie | De `is_set` kunt u de aanwezigheid van een kenmerk in de brongegevens controleren. `is_set` kan worden gebruikt in combinatie met `is_empty` om zowel de aanwezigheid van het kenmerk als de aanwezigheid van de waarde binnen het kenmerk te controleren. |
| `get_values` -functie | De `get_values` Met deze functie kunt u de waarden van de invoerkaart voor een bepaalde toets ophalen. |

Lees voor meer informatie de [Overzicht van Data Prep](../../data-prep/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-Time Customer Profile], kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| ------- | ----------- |
| API-uitbreidingen voor voorvertoning van profiel | De API voor de voorvertoning van profielen (`/previewsamplestatus`) bevat nu de mogelijkheid om een uitsplitsing weer te geven van de totale profielfragmenten in uw IMS-organisatie en om de distributie van profielfragmenten in alle naamruimten weer te geven. |
| Updates van de Unieschemaweergave | In het Experience Platform UI, kunnen de gebruikers informatie over alle schema&#39;s en datasets gemakkelijker vinden die tot het unieschema bijdragen, evenals oppervlakte zeer belangrijke attributen zoals identiteit en relatievelden. Deze updates verbeteren de capaciteit om problemen op te lossen en te bevestigen dat de profielen correct worden gevormd, worden de identiteiten correct vastgemaakt, en de gegevens zijn met succes opgenomen. |

Voor meer informatie over [!DNL Real-Time Customer Profile], met inbegrip van zelfstudies en aanbevolen procedures voor het werken met [!DNL Profile] gegevens, lees de [Overzicht van het realtime klantprofiel](../../profile/home.md).

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform], zodat ze gemakkelijk toegankelijk zijn voor elke Adobe-toepassing.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verwijdering segmentatielimiet streaming | De limiet van zeven dagen voor de terugzoekperiode is verwijderd. |

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| SSH-verificatieondersteuning voor SFTP | U kunt uw SFTP-account verbinden met [!DNL Platform] het gebruiken van RSA/DSA Open SSH sleutels. Zie de [SFTP-overzicht](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie . |
| UX-verbeteringen | U kunt uw gegevensset inschakelen voor [!DNL Profile] tijdens de gegevensinvoer. Zie de [gegevensstroom voor cloudopslag](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) zelfstudie voor meer informatie. |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).

## Tijd tot waarde {#time-to-value}

Adobe Experience Platform biedt marketingteams volledig de mogelijkheid om een 360-gradenweergave van hun klanten te maken zonder dat hiervoor uitgebreide expertise op het gebied van gegevenstechniek nodig is. Het doel is teams en waarde door gegevenssnelheid te versnellen.

&quot;Tijd tot waarde&quot; snijdt over persona&#39;s. De Ingenieurs van gegevens kunnen taken op een efficiënte en versnelde manier met de transparantie van de gegevensactiviteit voltooien, zodat een robuust, scalable klantenprofiel in real time sneller beschikbaar is. Marketers kunnen dan het volledige, robuuste klantprofiel gebruiken voor segmentatie en activering.

### Functiemarkeringen

#### Schema

Verbetert bruikbaarheid en werkstroom, en verstrekt out-of-box inzichten, normalisering, en transparantie van zeer belangrijke gebieden binnen schemacomposities. Hiermee wordt een gegevenskoppeling beschikbaar gemaakt voor de combinatie van afzonderlijke gegevensmodellen die worden voorgesteld als het &quot;union schema&quot;, waarmee u inzicht krijgt in de structuur en de ingrediënten van Real-Time klantprofiel.

- Workflowupgrade voor schema
   - De kortere weg van het gebruik voor het gemeenschappelijkste type van schema&#39;s XDM, met geautomatiseerde montages in de schemageditor en aanbevelingen van de schemagebiedgroep die op uw doelstellingen worden gebaseerd
   - Efficiëntere workflow dankzij meerdere mogelijkheden voor het selecteren en voorvertonen van veldgroepen
   - Verstrek transparantie op zeer belangrijke attributen van schemacompositie, met inbegrip van identiteit, verhouding, en vereiste en verouderde gebieden
- Unieschemagegevenslijn en belangrijkste kenmerken transparantie

#### Gegevensinname en -verzameling

De auto-afbeelding, de kaartvoorproef, en de bruikbaarheidsverbetering brengen gegevens van om het even welk platform of bron voor gebruik in profiel, stroomafwaartse segmentatie, en activering in. Het systeem heeft de efficiency en de intelligentie om dit proces gemakkelijker te maken te gebruiken, zelfs voor mensen buiten IT.

- Eenvoudiger toegang tot gegevensbronnen met inline-actiepatroon voor cataloguspaginakaart en gegevenstabel
- Berekend veld/expressie voor gegevensinvoer
- Aanbevelingen voor gegevenstoewijzing versnellen het innameproces
- Voorvertoning en validaties van toewijzing

#### Profielconfiguratie

De markt-vriendschappelijke profielkijker met aanpassing helpt u de samenstelling van een profiel voor gebruik in segmentatie, planning, en activeringsgevallen begrijpen. De geconsolideerde workflow hydrateert het profiel op een gecontroleerde en efficiënte manier door een stapsgewijze workflow voor het samenvoegbeleid te bieden.

- Bekijk elk individueel profiel in een verbeterde profielviewer die een dashboard met volledige aanpassing toont, toelatend gegroepeerde dwars-kanaalgegevens die op de bedrijfsdoelstellingen van de teler worden gebaseerd.
- Bewerk standaard- en aangepaste kenmerken in de widget Basisinformatie, afhankelijk van de bedrijfsbehoeften.
- Pas widgets met attributen van het klantenprofiel in real time aan, gebruikend de selecteur van het unieschema. Het samenvoegingsschema wordt afgeleid van de onderliggende gegevensmodellen die binnen de invoer van profielgegevens worden gebruikt.


#### Bewaking

Zorgt voor transparantie van gegevensstroom en geeft inzicht in de gezondheid van gegevensverkeer in het systeem van bronschakelaars, die meer zelfbediening en snellere actionability voor het oplossen van problemensituaties verstrekken.

- Alle doorloopacties controleren en een gedetailleerde weergave van elke uitvoering bekijken, inclusief voltooiingsstatus, uitvoerduur, lijst met verwerkte bestanden, fouten en diagnostische actiemogelijkheden
