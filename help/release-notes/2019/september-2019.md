---
title: Adobe Experience Platform Release Notes september 2019
description: De release van september 2019 bevat notities voor Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '536'
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
| Nieuw domein voor streaming invoer | De `dcs.data.adobe.net` domein is verplaatst naar het nieuwe gemeenschappelijke domein voor gegevensverzameling `dcs.adobedc.net`. Gebruikers dienen hun implementaties bij te werken volgens de herziene documentatie over het inslikken van Adobe Experience Platform. Alle documentatie met betrekking tot het stroomsgewijs opnemen van Adobe Experience Platform is bijgewerkt en gebruikt nu het nieuwe domein. |

Ga voor meer informatie naar de [Documentatie over gegevensinname](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] is een volledig beheerde dienst binnen [!DNL Experience Platform] dat gegevenswetenschappers in staat stelt naadloos inzichten van gegevens en inhoud over Adobe oplossingen en derdesystemen te produceren door de Modellen van het Leren van de Machine te bouwen en te exploiteren. [!DNL Data Science Workspace] is nauw geïntegreerd met [!DNL Platform] en maakt de levenscyclus van de end-to-end gegevenswetenschap mogelijk, inclusief de exploratie en voorbereiding van XDM-gegevens, gevolgd door de ontwikkeling en de operationele implementatie van Modellen om automatisch te verrijken [!DNL Real-time Customer Profile] met Inzichten van het leren van de machine.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Planning van de Diensten via UI | Geïntegreerd met [!DNL Platform] Orchestration Service om modeltraining en -scoring te automatiseren met door de gebruiker gedefinieerde schema&#39;s met behulp van de UI. |
| [!DNL Service Gallery] | Blader door, monitor en toegang tot services voor computerleren met de mogelijkheid om geautomatiseerde training en scoring taken te plannen, allemaal binnen de herontworpen [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0. | [!DNL JupyterLab] Verbeteringen in de gebruikersinterface. |

**Bekende problemen**

* Er is momenteel geen toegankelijke manier in de [!DNL Service Gallery] om een bestaande dienst te schrappen. In de tussentijd kunt u de [Referentie voor API voor leren Sensei Machine](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) om een bestaande Dienst door API vraag te schrappen.
* De [!DNL Service Gallery] heeft geen pagineringssteun om de opleiding van de Dienst en het scoren looppas te filtreren.
* Wanneer het vormen van geplande opleiding of het scoren looppas door [!DNL Service Gallery]door de frequentie in te stellen op uren, wordt het schema niet toegepast.

Ga voor meer informatie naar de [Overzicht van de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] biedt de mogelijkheid om standaard SQL te gebruiken voor het zoeken naar gegevens in Adobe Experience Platform ter ondersteuning van een groot aantal gebruiksgevallen voor analyses en gegevensbeheer. Het is een serverloos hulpmiddel dat u toestaat om zich bij datasets van aan te sluiten [!DNL Data Lake] en vangen de vraagresultaten als nieuwe dataset voor gebruik in het melden, [!DNL Data Science Workspace]of voor inname in [!DNL Real-time Customer Profile].

U kunt [!DNL Query Service] het bouwen van ecosystemen voor gegevensanalyse, waarbij een beeld wordt geschetst van klanten over hun verschillende interactiekanalen. Deze kanalen kunnen verkooppuntsystemen, web-, mobiele of CRM-systemen omvatten.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen aan [!DNL Query Editor] | Er is een opslagfunctie toegevoegd waarmee u een query kunt opslaan en er later aan kunt werken. Het tabblad &quot;Bladeren&quot; is toegevoegd aan het dialoogvenster [!DNL Query Service] gebruikersinterface op Adobe Experience Platform die query&#39;s weergeeft die zijn opgeslagen door gebruikers in uw organisatie. Het deelvenster &quot;Query-details&quot; is geïmplementeerd waarin nuttige metagegevens worden weergegeven over de query die wordt weergegeven. |
| Nieuwe toewijzingsfuncties | Adobe-gedefinieerde functies in [!DNL Query Service] om naar kanaalattributie met vervalparameters te zoeken. |
| Verbeteringen in SQL-syntaxis | Ondersteuning voor ilike-syntaxis. |
| Gegevenssets genereren met een gedefinieerd XDM-schema | Een nieuwe clausule in Create Lijst als Uitgezochte vragen (CTAS) toegevoegd die u toestaat om een doelschema te specificeren. |

Raadpleeg voor meer informatie de [Documentatie bij Query Service](../../query-service/home.md).
