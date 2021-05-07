---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform oktober 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 14 oktober 2020**

- [Gegevensprep](#data-prep)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)
- [Tijd tot waarde](#time-to-value)

## Data Prep {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| `is_set` -functie | Met de functie `is_set` kunt u de aanwezigheid van een kenmerk in de brongegevens controleren. `is_set` kan worden gebruikt in combinatie met  `is_empty` om zowel de aanwezigheid van het kenmerk als de aanwezigheid van de waarde binnen het kenmerk te controleren. |
| `get_values` -functie | Met de functie `get_values` kunt u de waarden uit de invoerkaart voor een bepaalde toets ophalen. |

Lees voor meer informatie het [Data Prep-overzicht](../../data-prep/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-time Customer Profile] ziet u een holistische weergave van elke individuele klant die gegevens van meerdere kanalen combineert, waaronder online, offline, CRM en gegevens van derden. [!DNL Profile] staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| ------- | ----------- |
| API-uitbreidingen voor voorvertoning van profiel | De API voor de voorvertoning van profielen (`/previewsamplestatus`) bevat nu de mogelijkheid om een uitsplitsing te bekijken van de totale profielfragmenten in uw IMS-organisatie en om de distributie van profielfragmenten in verschillende naamruimten te bekijken. |
| Updates van de Unieschemaweergave | In het Experience Platform UI, kunnen de gebruikers informatie over alle schema&#39;s en datasets gemakkelijker vinden die tot het unieschema bijdragen, evenals oppervlakte zeer belangrijke attributen zoals identiteit en relatievelden. Deze updates verbeteren de capaciteit om problemen op te lossen en te bevestigen dat de profielen correct worden gevormd, worden de identiteiten correct vastgemaakt, en de gegevens zijn met succes opgenomen. |

Lees voor meer informatie over [!DNL Real-time Customer Profile], waaronder zelfstudies en aanbevolen procedures voor het werken met [!DNL Profile]-gegevens, het [Real-time Customer Profile overview](../../profile/home.md).

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt bouwen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile]-gegevens. Deze segmenten worden centraal gevormd en gehandhaafd op [!DNL Platform], die hen gemakkelijk toegankelijk maken door om het even welke toepassing van de Adobe.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verwijdering segmentatielimiet streaming | De limiet van zeven dagen voor de terugzoekperiode is verwijderd. |

Zie [Segmentatieoverzicht](../../segmentation/home.md) voor meer informatie over [!DNL Segmentation Service]

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met services van [!DNL Platform]. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| SSH-verificatieondersteuning voor SFTP | U kunt uw rekening SFTP met [!DNL Platform] verbinden gebruikend de Open sleutels van SSH van RSA/DSA. Zie [SFTP overzicht](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie. |
| UX-verbeteringen | U kunt uw dataset voor [!DNL Profile] tijdens het proces van gegevensopname toelaten. Zie de [workflow voor cloudopslaggegevens](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) zelfstudie voor meer informatie. |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).

## Tijd naar waarde {#time-to-value}

Adobe Experience Platform biedt marketingteams volledig de mogelijkheid om een 360-gradenweergave van hun klanten te maken zonder dat hiervoor uitgebreide expertise op het gebied van gegevenstechniek nodig is. Het doel is teams en waarde door gegevenssnelheid te versnellen.

&quot;Tijd tot waarde&quot; snijdt over persona&#39;s. De Ingenieurs van gegevens kunnen taken op een efficiënte en versnelde manier met de transparantie van de gegevensactiviteit voltooien, zodat een robuust, scalable klantenprofiel in real time sneller beschikbaar is. Marketers kunnen dan het volledige, robuuste klantprofiel gebruiken voor segmentatie en activering.

### Functiemarkeringen

#### Schema

Verbetert bruikbaarheid en werkstroom, en verstrekt out-of-box inzichten, normalisering, en transparantie van zeer belangrijke gebieden binnen schemacomposities. Hiermee wordt een gegevenskoppeling beschikbaar gemaakt voor de combinatie van afzonderlijke gegevensmodellen die worden voorgesteld als het &quot;union schema&quot;, waarmee u inzicht krijgt in de structuur en de ingrediënten van het Real-time klantprofiel.

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
