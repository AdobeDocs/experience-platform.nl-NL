---
title: Adobe Experience Platform Release Notes september 2019
description: De release van september 2019 bevat notities voor Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 10 september 2019**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, zoals batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de Adobe Experience Platform-interface.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ----------- | ---------- |
| Nieuw domein voor streaming invoer | Het `dcs.data.adobe.net` -domein is verplaatst naar het nieuwe gemeenschappelijke domein voor gegevensverzameling `dcs.adobedc.net` . Gebruikers dienen hun implementaties bij te werken volgens de herziene documentatie over het inslikken van Adobe Experience Platform. Alle documentatie met betrekking tot het stroomsgewijs opnemen van Adobe Experience Platform is bijgewerkt en gebruikt nu het nieuwe domein. |

Voor meer informatie, bezoek de [ documentatie van de Ingestie van Gegevens ](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] is een volledig beheerde service binnen [!DNL Experience Platform] waarmee wetenschappers gegevens op naadloze wijze inzichten kunnen genereren op basis van gegevens en inhoud in oplossingen voor Adoben en systemen van derden door modellen voor het leren van machines te maken en te exploiteren. [!DNL Data Science Workspace] is nauw geïntegreerd met [!DNL Platform] en maakt de levenscyclus van de end-to-end gegevenswetenschap mogelijk, inclusief de exploratie en voorbereiding van XDM-gegevens, gevolgd door de ontwikkeling en de exploitatie van Modellen om [!DNL Real-Time Customer Profile] automatisch te verrijken met Inzichten voor het leren van machines.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| -----------| ---------- |
| Planning van de Diensten via UI | Geïntegreerd met [!DNL Platform] Orchestration Service om modeltraining en -scoring te automatiseren met door de gebruiker gedefinieerde schema&#39;s met behulp van de gebruikersinterface. |
| [!DNL Service Gallery] | Blader door, controleer en open de services voor machinaal leren, met de mogelijkheid om geautomatiseerde training en scoring taken te plannen, allemaal in de nieuwe versie [!DNL Service Gallery] . |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Verbeteringen in de gebruikersinterface. |

**Bekende kwesties**

* Er is momenteel geen toegankelijke manier in [!DNL Service Gallery] om een bestaande service te verwijderen. Ondertussen, gelieve te verwijzen naar de [ het Leren API van de Machine van Sensei verwijzing ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) om een bestaande Dienst door API vraag te schrappen.
* [!DNL Service Gallery] heeft geen pagineringssteun om de opleiding en het scoring looppas van de Dienst te filtreren.
* Wanneer u de geplande training of scoring configureert, wordt de frequentie op uur ingesteld, zodat het programma niet wordt toegepast. [!DNL Service Gallery]

Voor meer informatie, bezoek het [ Overzicht van Workspace van de Wetenschap van Gegevens ](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] biedt de mogelijkheid om standaard-SQL te gebruiken voor het uitvoeren van query&#39;s op gegevens in Adobe Experience Platform ter ondersteuning van verschillende gebruiksgevallen voor analyses en gegevensbeheer. Het is een serverloos hulpmiddel dat u toestaat om zich bij datasets van [!DNL Data Lake] aan te sluiten en de vraagresultaten te vangen als nieuwe dataset voor gebruik in het melden, [!DNL Data Science Workspace], of voor opname in [!DNL Real-Time Customer Profile].

Met [!DNL Query Service] kunt u gegevensanalysecosystemen samenstellen, zodat u een beeld krijgt van klanten in hun verschillende interactiekanalen. Deze kanalen kunnen verkooppuntsystemen, web-, mobiele of CRM-systemen omvatten.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen in [!DNL Query Editor] | Er is een opslagfunctie toegevoegd waarmee u een query kunt opslaan en er later aan kunt werken. Het tabblad &quot;Bladeren&quot; is toegevoegd aan de gebruikersinterface van [!DNL Query Service] in Adobe Experience Platform waarin query&#39;s worden weergegeven die zijn opgeslagen door gebruikers in uw organisatie. Het deelvenster &quot;Query-details&quot; is geïmplementeerd waarin nuttige metagegevens worden weergegeven over de query die wordt weergegeven. |
| Nieuwe toewijzingsfuncties | Adobe-bepaalde functies in [!DNL Query Service] aan vraag voor kanaalattributie met vervalparameters. |
| Verbeteringen in SQL-syntaxis | Ondersteuning voor ilike-syntaxis. |
| Gegevenssets genereren met een gedefinieerd XDM-schema | Een nieuwe clausule in Create Lijst als Uitgezochte vragen (CTAS) toegevoegd die u toestaat om een doelschema te specificeren. |

Voor meer informatie, verwijs naar de [ documentatie van de Dienst van de Vraag ](../../query-service/home.md).
