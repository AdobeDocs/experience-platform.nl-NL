---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform 9 september 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 64b6b59923d549cdcbf35d2e375529aec8cf81b8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 9 september 2020**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL-gegevensbeheer]](#governance)
* [[!DNL-doelen]](#destinations)
* [[!DNL-bronnen]](#sources)

## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface voor de labels van gegevenssets | Verschillende nieuwe besturingselementen voor sorteren en filteren zijn toegevoegd aan de interface van de gegevenssetlabels om het werken met grote schema&#39;s eenvoudiger te maken: <ul><li>U kunt velden sorteren op alfabetische volgorde op basis van het volledige schema-pad.</li><li>Gedeeltelijke zoekopdrachten uitvoeren op padnamen van velden.</li><li>Velden filteren zonder labels, met een geselecteerd label of met een labelcategorie.</li></ul> |

Zie het overzicht [van](../../data-governance/home.md) Gegevensbeheer voor meer informatie over de dienst.

## Doelen {#destinations}

In [Adobe Real-time het Platform](../../rtcdp/overview.md)van de Gegevens van de Klant, zijn de bestemmingen prebuilt integraties met bestemmingsplatforms die gegevens aan die partners op een naadloze manier activeren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| UX-verbeteringen | Gebruikers kunnen inline tabelhandelingen gebruiken om gemakkelijker toegang te krijgen tot primaire handelingen, zoals het toevoegen van gegevens, het bewerken van planningen en het toevoegen van segmenten. Zie het document van de [bestemmingswerkruimte](../../rtcdp/destinations/destinations-workspace.md) voor meer informatie. |

Ga voor meer informatie naar het overzicht met [bestemmingen](../../rtcdp/destinations/destinations-overview.md)

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Automatisch toewijzen | [!DNL Platform] verstrekt intelligente aanbevelingen voor auto afbeelding tijdens het werkschema van de gegevensopname, dat op een user-selected doelschema of dataset wordt gebaseerd. U kunt flexibele regels voor automatische toewijzingen handmatig aanpassen aan uw gebruiksgevallen. |
| UX-verbeteringen | Gebruikers kunnen inline tabelhandelingen gebruiken om gemakkelijker toegang te krijgen tot primaire handelingen, zoals het toevoegen van gegevens, het bewerken van planningen en het toevoegen van segmenten. Zie het document met [controlegegevens](../../sources/tutorials/ui/monitor.md) voor meer informatie. |

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.