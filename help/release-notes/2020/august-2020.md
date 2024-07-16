---
title: Opmerkingen bij de release van Adobe Experience Platform, augustus 2020
description: Opmerkingen bij de release van augustus 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 12 augustus 2020**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te ontketenen. [!DNL Data Science Workspace] is geïntegreerd in Adobe Experience Platform en helpt u bij het maken van voorspellingen met behulp van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| VM-verbeteringen in [!DNL JupyterLab] | Verbeterde stabiliteit van langlopende [!DNL JupyterLab notebook] virtuele machines. |

Voor meer informatie over [!DNL JupyterLab], gelieve te zien de [[!DNL JupyterLab]  gebruikersgids ](../../data-science-workspace/jupyterlab/overview.md).

## Doelen {#destinations}

In [ Real-time Customer Data Platform ](../../rtcdp/overview.md), zijn de bestemmingen pre-gebouwde integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Doel | Beschrijving |
|--- | ---|
| [!DNL Google Customer Match] | Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om klanten te bereiken en opnieuw contact op te nemen met andere Google, zoals: [!DNL Search], [!DNL Shopping] , Gmail en YouTube. <br><br> Bezoek de [!DNL Google Customer Match] [ pagina ](../../destinations/catalog/advertising/google-customer-match.md) in de bestemmingscatalogus voor meer informatie over de bestemming en hoe te opstelling het in Real-Time CDP. |

**Nieuwe eigenschappen**

| Functie | Beschrijving |
|------- | -----------|
| Aangepaste bestandsnaameditor | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud waarmee u de naam van de geëxporteerde bestanden kunt bewerken. Voor meer informatie, verwijs naar [ vorm stap ](../../destinations/ui/activate-batch-profile-destinations.md) in het activeringswerkschema. |
| Aanbevolen kenmerken | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud die aanbevolen kenmerken bevat om aan de geëxporteerde bestanden toe te voegen. Voor meer informatie, verwijs naar [ Uitgezochte attributenstap ](../../destinations/ui/activate-batch-profile-destinations.md) in het activeringswerkschema. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Real-time Customer Data Platform ([!DNL Real-Time CDP]) is gebaseerd op Experience Platform en helpt bedrijven bekende en onbekende gegevens bijeen te brengen om klantprofielen te activeren door middel van intelligente beslissingen tijdens de reis van de klant. [!DNL Real-Time CDP] combineert meerdere bedrijfsgegevensbronnen om klantprofielen in real-time te maken. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| IAB TCF 2.0-ondersteuning | [!DNL Real-Time CDP] is nu een geregistreerde leverancier voor versie 2.0 van [!DNL Transparency & Consent Framework] (TCF), zoals geschetst door [!DNL Interactive Advertising Bureau] (IAB). U kunt uw gegevensverrichtingen en profielschema&#39;s vormen om de gegevens van de klantentoestemming goed te keuren die door CMP worden geproduceerd, en de toestemmingsvoorkeur van uw klanten af te dwingen wanneer het activeren van segmenten aan stroomafwaartse bestemmingen. |

Voor meer informatie over [!DNL Real-Time CDP], zie het [[!DNL Real-Time CDP]  overzicht ](../../rtcdp/overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Bewaking van de stroom | Gebruikers kunnen alle flowuitvoering controleren en een gedetailleerde weergave van elke uitvoering bekijken, zoals voltooiingsstatus, duur van de uitvoering, lijst met verwerkte bestanden, fouten en metriek. Zie [ controledatablows ](../../sources/tutorials/ui/monitor.md) document voor meer informatie. |
| Meldingen voor stroomuitvoering | Gebruikers kunnen zich abonneren op gebeurtenissen en websites registreren om realtime meldingen te ontvangen over de status, metriek en fouten met betrekking tot flowuitvoering. |
| Verbeteringen in gebruikerscatalogus | Updates voor het catalogusscherm van bronnen zodat u gemakkelijker toegang hebt tot primaire acties van geselecteerde objecten. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
