---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform, 10 augustus 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: d29f7c7243ec798abe60fff895b36277996cb4a0
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 12 augustus 2020**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Data Platform]](#rtcdp)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te onthullen. Met de geïntegreerde Adobe Experience Platform-software kunt u [!DNL Data Science Workspace] voorspellingen maken op basis van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| VM-verbeteringen in [!DNL JupyterLab] | Verbeterde stabiliteit van langdurige [!DNL JupyterLab notebook] virtuele machines. |

Raadpleeg de [!DNL JupyterLab]gebruikershandleiding [[!DNL JupyterLab] voor meer informatie over](../../data-science-workspace/jupyterlab/overview.md).

## Doelen {#destinations}

In het Platform [van Gegevens van de Klant in](../../rtcdp/overview.md)real time, zijn de bestemmingen prebuilt integratie met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| [!DNL Google Customer Match] | Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere klanten over de eigendommen en bediende eigenschappen van Google, zoals: [!DNL Search], [!DNL Shopping], Gmail en YouTube. <br><br> Bezoek de [!DNL Google Customer Match] pagina [](../../destinations/catalog/advertising/google-customer-match.md) in de bestemmingscatalogus voor meer informatie over de bestemming en hoe te opstelling het in real time CDP. |

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Aangepaste bestandsnaameditor | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud waarmee u de naam van de geëxporteerde bestanden kunt bewerken. Voor meer informatie, verwijs naar de [ Configure stap](../../destinations/ui/activate-destinations.md#configure) in het activeringswerkschema. |
| Aanbevolen kenmerken | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud die aanbevolen kenmerken bevat om aan de geëxporteerde bestanden toe te voegen. Raadpleeg de stap [Kenmerken](../../destinations/ui/activate-destinations.md#select-attributes) selecteren in de activeringsworkflow voor meer informatie. |

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Het Real-Time Customer Data Platform ([!DNL Real-time CDP]) is gebaseerd op Experience Platform en helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen te activeren met intelligente beslissingen gedurende de hele reis van de klant. [!DNL Real-time CDP] combineert veelvoudige bronnen van ondernemingsgegevens om klantenprofielen in real time tot stand te brengen. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| IAB TCF 2.0-ondersteuning | [!DNL Real-time CDP] is nu een geregistreerde leverancier voor versie 2.0 van [!DNL Transparency & Consent Framework] (TCF), zoals geschetst door [!DNL Interactive Advertising Bureau] (IAB). U kunt uw gegevensverrichtingen en profielschema&#39;s vormen om de gegevens van de klantentoestemming goed te keuren die door CMP worden geproduceerd, en de toestemmingsvoorkeur van uw klanten af te dwingen wanneer het activeren van segmenten aan stroomafwaartse bestemmingen. Zie het overzicht op [IAB TCF 2.0 steun in Echt - tijd CDP](../../rtcdp/privacy/iab/overview.md) voor meer informatie. |

Zie het [!DNL Real-time CDP]overzicht [[!DNL Real-time CDP] voor meer informatie over](../../rtcdp/overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Bewaking van de stroom | Gebruikers kunnen alle flowuitvoering controleren en een gedetailleerde weergave van elke uitvoering bekijken, zoals voltooiingsstatus, uitvoerduur, lijst met verwerkte bestanden, fouten en metriek. Zie het document met [controlegegevens](../../sources/tutorials/ui/monitor.md) voor meer informatie. |
| Meldingen voor stroomuitvoering | Gebruikers kunnen zich abonneren op gebeurtenissen en websites registreren om realtime meldingen te ontvangen over de status, metriek en fouten met betrekking tot flowuitvoering. |
| Verbeteringen in gebruikerscatalogus | Updates voor het catalogusscherm van bronnen zodat u gemakkelijker toegang hebt tot primaire acties van geselecteerde objecten. |

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.