---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform, 10 augustus 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 8b540a108336ae4475f072b71a34e37cac064826
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 12 augustus 2020**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [!DNL Destinations](#destinations)
- [[!DNL-bronnen]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten van uw gegevens te onthullen. Met de geïntegreerde Adobe Experience Platform-software kunt u [!DNL Data Science Workspace] voorspellingen maken op basis van uw inhoud en gegevenselementen voor verschillende Adobe-oplossingen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| VM-verbeteringen in [!DNL JupyterLab] | Verbeterde stabiliteit van langdurige [!DNL JupyterLab notebook] virtuele machines. |

Raadpleeg de [!DNL JupyterLab]gebruikershandleiding [[!DNL JupyterLab] voor meer informatie over](../../data-science-workspace/jupyterlab/overview.md).

## Doelen {#destinations}

In [Adobe Real-time het Platform](../../rtcdp/overview.md)van de Gegevens van de Klant, zijn de bestemmingen prebuilt integraties met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe bestemmingen**

Er zijn nieuwe doelen beschikbaar waar u uw Adobe Experience Platform-gegevens kunt activeren. Zie hieronder voor meer informatie:

| Bestemming | Beschrijving |
|--- | ---|
| [!DNL Google Customer Match] | Met Google Customer Match kunt u uw online- en offline gegevens gebruiken om uw klanten te bereiken en opnieuw contact op te nemen met andere klanten over de eigendommen en bediende eigenschappen van Google, zoals: [!DNL Search], [!DNL Shopping], Gmail en YouTube. <br><br> Bezoek de [!DNL Google Customer Match] pagina [](/help/rtcdp/destinations/google-customer-match-destination.md) in de bestemmingscatalogus voor meer informatie over de bestemming en hoe te opstelling het in Adobe in real time CDP. |

**Nieuwe functies**

| Functie | Beschrijving |
|------- | -----------|
| Aangepaste bestandsnaameditor | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud waarmee u de naam van de geëxporteerde bestanden kunt bewerken. Voor meer informatie, verwijs naar de [ Configure stap](/help/rtcdp/destinations/activate-destinations.md#configure) in het activeringswerkschema. |
| Aanbevolen kenmerken | Update naar de workflow voor gegevensactivering voor marketingdoelen en opslagdoelen in de cloud die aanbevolen kenmerken bevat om aan de geëxporteerde bestanden toe te voegen. Raadpleeg de stap [Kenmerken](/help/rtcdp/destinations/activate-destinations.md#select-attributes) selecteren in de activeringsworkflow voor meer informatie. |

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
