---
title: Aanvullende informatie van oktober 2020 voor Adobe Experience Platform
description: Aanvullende informatie van oktober 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 16%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 14 oktober 2020**

- [Gegevensvoorbereiding](#data-prep)
- [Realtime-klantenprofiel](#profile)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)
- [Tijd tot waarde](#time-to-value)

## Gegevensvoorbereiding {#data-prep}

Met gegevensvoorbereiding kunnen gegevenstechnici gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience-datamodel).

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| `is_set` functie | Met de functie `is_set` kunt u de aanwezigheid van een kenmerk in de brongegevens controleren. `is_set` kan in combinatie met `is_empty` worden gebruikt om zowel de aanwezigheid van het kenmerk als de aanwezigheid van de waarde binnen het kenmerk te controleren. |
| `get_values` functie | Met de functie `get_values` kunt u de waarden van de invoerkaart voor een bepaalde toets ophalen. |

Voor meer informatie, te lezen gelieve het [&#x200B; Prep overzicht van Gegevens &#x200B;](../../data-prep/home.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met [!DNL Real-Time Customer Profile] ziet u een holistische weergave van elke individuele klant die gegevens van meerdere kanalen combineert, waaronder online, offline, CRM en gegevens van derden. Met [!DNL Profile] kunt u uw verschillende klantgegevens consolideren in een uniforme weergave die een actionabel, tijdstempelaccount voor elke klantinteractie biedt.

| Functie | Beschrijving |
| ------- | ----------- |
| API-uitbreidingen voor voorvertoning van profiel | De voorproef API van het Profiel (`/previewsamplestatus`) omvat nu de capaciteit om een verdeling van totale profielfragmenten over uw organisatie te bekijken, evenals de distributie van profielfragmenten over identiteitsnamespaces. |
| Updates van de Unieschemaweergave | In Experience Platform UI, kunnen de gebruikers gemakkelijker informatie betreffende alle schema&#39;s en datasets vinden die tot het unieschema bijdragen, evenals oppervlakte zeer belangrijke attributen zoals identiteit en relatievelden. Deze updates verbeteren de capaciteit om problemen op te lossen en te bevestigen dat de profielen correct worden gevormd, worden de identiteiten correct vastgemaakt, en de gegevens zijn met succes opgenomen. |

Voor meer informatie over [!DNL Real-Time Customer Profile], met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, te lezen gelieve het [&#x200B; overzicht van het Profiel van de Klant in real time &#x200B;](../../profile/home.md).

## Segmentatieservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Experience Platform], zodat ze gemakkelijk toegankelijk zijn voor alle Adobe-toepassingen.

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verwijdering segmentatielimiet streaming | De limiet van zeven dagen voor de terugzoekperiode is verwijderd. |

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [&#x200B; overzicht van de Segmentatie &#x200B;](../../segmentation/home.md)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| SSH-verificatieondersteuning voor SFTP | U kunt uw SFTP-account verbinden met [!DNL Experience Platform] met behulp van RSA/DSA Open SSH-toetsen. Zie het [&#x200B; overzicht van SFTP &#x200B;](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie. |
| UX-verbeteringen | U kunt uw dataset voor [!DNL Profile] tijdens het proces van de gegevensopname toelaten. Zie het [&#x200B; werkschema van de de gegevensstroom van de wolkenopslag &#x200B;](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) leerprogramma voor meer informatie. |

Meer over bronnen leren, zie het [&#x200B; overzicht van bronnen &#x200B;](../../sources/home.md).

## Tijd tot waarde {#time-to-value}

Adobe Experience Platform biedt marketingteams de volledige mogelijkheid om een 360-gradenweergave van hun klanten te maken zonder dat hiervoor uitgebreide expertise op het gebied van gegevenstechniek nodig is. Het doel is teams en waarde door gegevenssnelheid te versnellen.

&quot;Tijd tot waarde&quot; snijdt over persona&#39;s. De Ingenieurs van gegevens kunnen taken op een efficiënte en versnelde manier met de transparantie van de gegevensactiviteit voltooien, zodat een robuust, scalable klantenprofiel in real time sneller beschikbaar is. Marketers kunnen dan het volledige, robuuste klantprofiel gebruiken voor segmentatie en activering.

### Functiemarkeringen

#### Schema

Verbetert bruikbaarheid en werkstroom, en verstrekt out-of-box inzichten, normalisering, en transparantie van zeer belangrijke gebieden binnen schemacomposities. Hiermee wordt een gegevenskoppeling beschikbaar gemaakt voor de combinatie van afzonderlijke gegevensmodellen die worden voorgesteld als het &quot;union schema&quot;, waarbij insight de structuur en de ingrediënten krijgt toegewezen aan Real-Time klantprofiel.

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

Zorgt voor transparantie van de gegevensstroom en geeft insight informatie over de gezondheid van gegevensverkeer in het systeem van bronschakelaars, die meer zelfbediening en snellere actionability voor het oplossen van problemensituaties verstrekken.

- Alle doorloopacties controleren en een gedetailleerde weergave van elke uitvoering bekijken, inclusief voltooiingsstatus, uitvoerduur, lijst met verwerkte bestanden, fouten en diagnostische actiemogelijkheden
