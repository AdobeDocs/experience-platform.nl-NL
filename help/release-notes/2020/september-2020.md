---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2020
description: In de release van september 2020 staat een opmerking voor Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 9 september 2020**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensbeheer](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Gegevensbeheer {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. De klasse speelt binnen [!DNL Experience Platform] op diverse niveaus een sleutelrol, zoals catalogisering, gegevenskoppeling, labels voor gegevensgebruik, beleid voor gegevenstoegang en toegangsbeheer voor marketingacties.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen in de gebruikersinterface voor de labels van gegevenssets | Verschillende nieuwe besturingselementen voor sorteren en filteren zijn toegevoegd aan de interface van de gegevenssetlabels om het werken met grote schema&#39;s eenvoudiger te maken: <ul><li>U kunt velden sorteren op alfabetische volgorde op basis van het volledige schema.</li><li>Gedeeltelijke zoekopdrachten uitvoeren op padnamen van velden.</li><li>Velden filteren zonder labels, met een geselecteerd label of met een labelcategorie.</li></ul> |

Zie het [ overzicht van het Beleid van Gegevens ](../../data-governance/home.md) voor meer informatie over de dienst.

## Doelen {#destinations}

In [ Real-time Customer Data Platform ](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| UX-verbeteringen | Gebruikers kunnen inline tabelhandelingen gebruiken om gemakkelijker toegang te krijgen tot primaire handelingen, zoals het toevoegen van gegevens, het bewerken van planningen en het toevoegen van segmenten. Zie het [ document van de bestemmingswerkruimte ](../../destinations/ui/destinations-workspace.md) voor meer informatie. |

Meer leren, bezoek het [ overzicht van bestemmingen ](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

Met [!DNL Observability Insights] kunt u de activiteiten op Adobe Experience Platform volgen aan de hand van statistische gegevens en gebeurtenismeldingen.

**Nieuwe Eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Adobe I/O-gebeurtenismeldingen | [!DNL Observability Insights] gebruikt Adobe I/O Events om gebeurtenismeldingen te maken voor verschillende services van Experience Platforms. De lading van het bericht wordt verzonden naar een gevormde webhaak die u kunt dan gebruiken om verdere stroomafwaartse processen te automatiseren. |

Zie het [[!DNL Observability Insights]  overzicht ](../../observability/home.md) voor meer informatie over de dienst.

## [!DNL Privacy Service] {#privacy}

Verschillende wettelijke en organisatorische regelingen geven gebruikers het recht om hun persoonsgegevens op verzoek in uw gegevensopslag te openen of te verwijderen. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor LGPD (Brazilië) | Privacy-banen kunnen nu worden gecreëerd onder de Braziliaanse [!DNL Lei Geral de Proteção de Dados] (LGPD)-verordening. Deze taken worden bijgehouden met de code voor regelgeving `lgpd_bra` . |

Zie het [ overzicht van de Privacy Service ](../../privacy-service/home.md) voor meer informatie over de dienst.

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-Time Customer Profile] ziet u een holistische weergave van elke individuele klant die gegevens van meerdere kanalen combineert, waaronder online, offline, CRM en gegevens van derden. Met [!DNL Profile] kunt u uw verschillende klantgegevens consolideren in een uniforme weergave die een actionabel, tijdstempelaccount voor elke klantinteractie biedt.

| Functie | Beschrijving |
| ------- | ----------- |
| Profile Viewer | De profielviewer is in de gebruikersinterface van het platform bijgewerkt tot een dashboard met volledige aanpassing. De gebruiker kan nu de volgende taken uitvoeren: <ul><li>Werk de geselecteerde standaard- en aangepaste kenmerken bij in de basisinformatiewidget.</li><li>Aangepaste widgets maken, bewerken en verwijderen</li><li>Widgets vergroten of verkleinen en opnieuw rangschikken</li></ul> |

Voor meer informatie over [!DNL Real-Time Customer Profile], met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, te lezen gelieve het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md).

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform], zodat ze gemakkelijk toegankelijk zijn voor elke Adobe.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Exporttaken | Er is een vlag toegevoegd waarmee segmenten kunnen worden geëvalueerd als onderdeel van een exporttaak. Hierdoor kunnen gebruikers zowel segmentatie als export in één taak uitvoeren. |
| Beleid samenvoegen | Het veelvoudige samenvoegbeleid kan in één enkele baan van de partijsegmentatie worden omvat. |

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [ overzicht van de Segmentatie ](../../segmentation/home.md)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Automatisch toewijzen | [!DNL Platform] biedt intelligente aanbevelingen voor automatische toewijzing tijdens de workflow voor gegevensinvoer, op basis van een door de gebruiker geselecteerd doelschema of gegevensset. U kunt flexibele regels voor automatische toewijzingen handmatig aanpassen aan uw gebruiksgevallen. |
| UX-verbeteringen | Gebruikers kunnen inline tabelhandelingen gebruiken om gemakkelijker toegang te krijgen tot primaire handelingen, zoals het toevoegen van gegevens, het bewerken van planningen en het toevoegen van segmenten. Zie [ controledatablows ](../../sources/tutorials/ui/monitor.md) document voor meer informatie. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
