---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 9 september 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: adf8e8457c8ffef263223a38d3f9c345cf7c6ab2
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 9 september 2020**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Governance]](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeteringen in de gebruikersinterface voor de labels van gegevenssets | Verschillende nieuwe besturingselementen voor sorteren en filteren zijn toegevoegd aan de interface van de gegevenssetlabels om het werken met grote schema&#39;s eenvoudiger te maken: <ul><li>U kunt velden sorteren op alfabetische volgorde op basis van het volledige schema-pad.</li><li>Gedeeltelijke zoekopdrachten uitvoeren op padnamen van velden.</li><li>Velden filteren zonder labels, met een geselecteerd label of met een labelcategorie.</li></ul> |

Zie het overzicht [van](../../data-governance/home.md) Gegevensbeheer voor meer informatie over de dienst.

## Doelen {#destinations}

In het Platform [van Gegevens van de Klant in](../../rtcdp/overview.md)real time, zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| UX-verbeteringen | Gebruikers kunnen inline tabelhandelingen gebruiken om gemakkelijker toegang te krijgen tot primaire handelingen, zoals het toevoegen van gegevens, het bewerken van planningen en het toevoegen van segmenten. Zie het document van de [bestemmingswerkruimte](../../destinations/ui/destinations-workspace.md) voor meer informatie. |

Ga voor meer informatie naar het overzicht met [bestemmingen](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] kunt u de activiteiten op Adobe Experience Platform volgen door statistische gegevens en gebeurtenismeldingen te gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Adobe I/O-gebeurtenismeldingen | [!DNL Observability Insights] hefboomwerkingen Adobe I/O Events om gebeurtenisberichten voor verscheidene diensten van het Experience Platform tot stand te brengen. De lading van het bericht wordt verzonden naar een gevormde webhaak die u kunt dan gebruiken om verdere stroomafwaartse processen te automatiseren. Zie het overzicht [van](../../observability/notifications/overview.md) meldingen voor meer informatie. |

Zie het [[!DNL Observability Insights] overzicht](../../observability/home.md) voor meer informatie over de dienst.

## [!DNL Privacy Service] {#privacy}

Verschillende wettelijke en organisatorische regelingen geven gebruikers het recht om hun persoonsgegevens op verzoek in uw gegevensopslag te openen of te verwijderen. Adobe Experience Platform [!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u deze gegevensaanvragen van uw klanten kunt beheren. Met [!DNL Privacy Service]kunt u verzoeken indienen om toegang te krijgen tot persoonlijke of persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor LGPD (Brazilië) | Privacy jobs kunnen nu worden gecreëerd in het kader van de Braziliaanse [!DNL Lei Geral de Proteção de Dados] (LGPD) verordening. Deze banen worden bijgehouden onder de code van de verordening `lgpd_bra`. |

Zie het overzicht [van de](../../privacy-service/home.md) Privacy Service voor meer informatie over de dienst.

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-time Customer Profile], kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| ------- | ----------- |
| Profielviewer | De profielviewer is in de gebruikersinterface van het Platform bijgewerkt tot een dashboard met volledige aanpassing. De gebruiker heeft nu de optie om de volgende taken uit te voeren: <ul><li>Werk de geselecteerde standaard- en aangepaste kenmerken bij in de basisinformatiewidget.</li><li>Aangepaste widgets maken, bewerken en verwijderen</li><li>Widgets vergroten of verkleinen en opnieuw rangschikken</li></ul> |

Lees voor meer informatie over [!DNL Real-time Customer Profile], waaronder zelfstudies en aanbevolen procedures voor het werken met [!DNL Profile] gegevens, het overzicht [](../../profile/home.md)van het realtime-klantprofiel.

## Segmenteringsservice {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt bouwen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal gevormd en gehandhaafd [!DNL Platform], die hen gemakkelijk toegankelijk door om het even welke toepassing van de Adobe maken.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Exporttaken | Er is een vlag toegevoegd waarmee segmenten kunnen worden geëvalueerd als onderdeel van een exporttaak. Hierdoor kunnen gebruikers zowel segmentatie als export in één taak uitvoeren. |
| Beleid samenvoegen | Het veelvoudige samenvoegbeleid kan in één enkele baan van de partijsegmentatie worden omvat. |

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het overzicht van de [Segmentatie](../../segmentation/home.md)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Automatisch toewijzen | [!DNL Platform] verstrekt intelligente aanbevelingen voor auto afbeelding tijdens het werkschema van de gegevensopname, dat op een user-selected doelschema of dataset wordt gebaseerd. U kunt flexibele regels voor automatische toewijzingen handmatig aanpassen aan uw gebruiksgevallen. |
| UX-verbeteringen | Gebruikers kunnen inline tabelhandelingen gebruiken om gemakkelijker toegang te krijgen tot primaire handelingen, zoals het toevoegen van gegevens, het bewerken van planningen en het toevoegen van segmenten. Zie het document met [controlegegevens](../../sources/tutorials/ui/monitor.md) voor meer informatie. |

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.
