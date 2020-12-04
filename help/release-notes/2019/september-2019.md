---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 10 september 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 10 september 2019**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, waaronder batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de Adobe Experience Platform-interface.

**Nieuwe functies**

| Functie | Beschrijving |
| ----------- | ---------- |
| Nieuw domein voor streaming invoer | Het `dcs.data.adobe.net` domein is verplaatst naar het nieuwe gemeenschappelijke domein voor gegevensverzameling `dcs.adobedc.net`. Gebruikers dienen hun implementaties bij te werken volgens de herziene documentatie over het inslikken van Adobe Experience Platform. Alle documentatie met betrekking tot het stroomsgewijs opnemen van Adobe Experience Platform is bijgewerkt en gebruikt nu het nieuwe domein. |

Voor meer informatie, bezoek de documentatie [van de](../../ingestion/home.md)Ingestie van Gegevens.

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] is een volledig beheerde dienst binnen [!DNL Experience Platform] die gegevenswetenschappers toelaat om inzichten van gegevens en inhoud over oplossingen van Adobe en derdesystemen foutloos te produceren door de Modellen van het Leren van de Machine te bouwen en in werking te stellen. [!DNL Data Science Workspace] is nauw geïntegreerd met de levenscyclus van de end-to-end gegevenswetenschap, inclusief de exploratie en voorbereiding van XDM-gegevens, gevolgd door de ontwikkeling en de exploitatie van Modellen om automatisch te verrijken [!DNL Platform] [!DNL Real-time Customer Profile] met Inzichten voor het leren van machines.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Planning van de Diensten via UI | Geïntegreerd met de Dienst van de Orchestratie om Model opleiding en het scoren met user-defined programma&#39;s te automatiseren gebruikend UI. [!DNL Platform] |
| [!DNL Service Gallery] | Blader door, controleer en open de services voor machinaal leren met de mogelijkheid om geautomatiseerde training en scoring taken te plannen, allemaal binnen de nieuwe opzet [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Verbeteringen in de gebruikersinterface. |

**Bekende problemen**

* Er is momenteel geen toegankelijke manier in de [!DNL Service Gallery] om een bestaande Dienst te schrappen. In de tussentijd raadpleegt u de API-naslaggids [voor het leren van](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei-machines om een bestaande service te verwijderen via API-aanroepen.
* De [!DNL Service Gallery] heeft geen pagineringssteun om de opleiding en het scoring looppas van de Dienst te filtreren.
* Wanneer het vormen van geplande opleiding of het scoren looppas door de [!DNL Service Gallery], plaatsend de frequentie om het programma te verhinderen worden toegepast.

Voor meer informatie, bezoek het Overzicht [van de Werkruimte van de Wetenschap van](../../data-science-workspace/home.md)Gegevens.

## [!DNL Query Service] {#query}

[!DNL Query Service] biedt de mogelijkheid om standaard SQL te gebruiken voor het zoeken naar gegevens in Adobe Experience Platform ter ondersteuning van een groot aantal gebruiksgevallen voor analyses en gegevensbeheer. Het is een serverloos hulpmiddel dat u toestaat om zich bij datasets van de vraag aan te sluiten [!DNL Data Lake] en de vraagresultaten als nieuwe dataset voor gebruik in het melden, [!DNL Data Science Workspace]of voor opname in te vangen [!DNL Real-time Customer Profile].

U kunt gegevens gebruiken [!DNL Query Service] om ecosystemen van de gegevensanalyse te bouwen, die tot een beeld van klanten over hun diverse interactiekanalen leiden. Deze kanalen kunnen verkooppuntsystemen, web-, mobiele of CRM-systemen omvatten.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen aan [!DNL Query Editor] | Er is een opslagfunctie toegevoegd waarmee u een query kunt opslaan en er later aan kunt werken. Het tabblad &quot;Bladeren&quot; is toegevoegd aan de [!DNL Query Service] gebruikersinterface van Adobe Experience Platform waarin query&#39;s worden weergegeven die zijn opgeslagen door gebruikers in uw organisatie. Het deelvenster &quot;Query-details&quot; is geïmplementeerd waarin nuttige metagegevens worden weergegeven over de query die wordt weergegeven. |
| Nieuwe toewijzingsfuncties | Adobe-bepaalde functies in [!DNL Query Service] aan vraag voor kanaalattributie met vervalparameters. |
| Verbeteringen in SQL-syntaxis | Ondersteuning voor ilike-syntaxis. |
| Gegevenssets genereren met een gedefinieerd XDM-schema | Een nieuwe clausule in Create Lijst als Uitgezochte vragen (CTAS) toegevoegd die u toestaat om een doelschema te specificeren. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).