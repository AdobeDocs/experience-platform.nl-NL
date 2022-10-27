---
title: Opmerkingen bij de release van Adobe Experience Platform, augustus 2020
description: Opmerkingen bij de release van augustus 2020 voor Adobe Experience Platform.
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
exl-id: 9347147f-e830-4487-aa12-f56723abb3c8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 4%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 12 augustus 2020**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te onthullen. geïntegreerd in Adobe Experience Platform, [!DNL Data Science Workspace] helpt u om voorspellingen te maken gebruikend uw inhoud en gegevensactiva over Adobe oplossingen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| VM-verbeteringen in [!DNL JupyterLab] | Verbeterde stabiliteit van de lange termijn [!DNL JupyterLab notebook] virtuele machines. |

Voor meer informatie over [!DNL JupyterLab], zie de [[!DNL JupyterLab] gebruikershandleiding](../../data-science-workspace/jupyterlab/overview.md).

## Doelen {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| [!DNL Google Customer Match] | Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere, in Google gevestigde en bediende eigendommen, zoals: [!DNL Search], [!DNL Shopping], Gmail en YouTube. <br><br> Ga naar [!DNL Google Customer Match] [page](../../destinations/catalog/advertising/google-customer-match.md) in de lijst met bestemmingen voor meer informatie over het doel en hoe u het kunt instellen in Real-Time CDP. |

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Aangepaste bestandsnaameditor | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud waarmee u de naam van de geëxporteerde bestanden kunt bewerken. Raadpleeg voor meer informatie de [ Stap configureren](../../destinations/ui/activate-batch-profile-destinations.md) in de activeringsworkflow. |
| Aanbevolen kenmerken | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud die aanbevolen kenmerken bevat om aan de geëxporteerde bestanden toe te voegen. Raadpleeg voor meer informatie de [stap Kenmerken selecteren](../../destinations/ui/activate-batch-profile-destinations.md) in de activeringsworkflow. |

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Gebouwd op Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen met intelligente besluitvorming door de klantenreis te activeren. [!DNL Real-Time CDP] combineert veelvoudige bronnen van ondernemingsgegevens om klantenprofielen in real time tot stand te brengen. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| IAB TCF 2.0-ondersteuning | [!DNL Real-Time CDP] is nu een geregistreerde leverancier voor versie 2.0 van [!DNL Transparency & Consent Framework] (TCF), zoals beschreven door de [!DNL Interactive Advertising Bureau] (IAB). U kunt uw gegevensverrichtingen en profielschema&#39;s vormen om de gegevens van de klantentoestemming goed te keuren die door CMP worden geproduceerd, en de toestemmingsvoorkeur van uw klanten af te dwingen wanneer het activeren van segmenten aan stroomafwaartse bestemmingen. |

Voor meer informatie over [!DNL Real-Time CDP], zie de [[!DNL Real-Time CDP] overzicht](../../rtcdp/overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Bewaking van de stroom | Gebruikers kunnen alle flowuitvoering controleren en een gedetailleerde weergave van elke uitvoering bekijken, zoals voltooiingsstatus, uitvoerduur, lijst met verwerkte bestanden, fouten en metriek. Zie de [gegevensstromen controleren](../../sources/tutorials/ui/monitor.md) voor meer informatie. |
| Meldingen voor stroomuitvoering | Gebruikers kunnen zich abonneren op gebeurtenissen en websites registreren om realtime meldingen te ontvangen over de status, metriek en fouten met betrekking tot flowuitvoering. |
| Verbeteringen in gebruikerscatalogus | Updates voor het catalogusscherm van bronnen zodat u gemakkelijker toegang hebt tot primaire acties van geselecteerde objecten. |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
