---
title: Aanvullende informatie van september 2019 voor Adobe Experience Platform
description: Aanvullende informatie voor de versie van september 2019 voor Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 6%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: woensdag 10 september 2019**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. Adobe Experience Platform [!DNL Data Ingestion] biedt meerdere alternatieven voor het opnemen van gegevens, zoals batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de Adobe Experience Platform-interface.

**Nieuwe functies**

| Functie | Beschrijving |
| ----------- | ---------- |
| Nieuw domein voor streaming invoer | Het `dcs.data.adobe.net` -domein is verplaatst naar het nieuwe gemeenschappelijke domein voor gegevensverzameling `dcs.adobedc.net` . Gebruikers dienen hun implementaties bij te werken volgens de herziene documentatie over het inslikken van Adobe Experience Platform. Alle documentatie met betrekking tot het stroomsgewijs opnemen van Adobe Experience Platform is bijgewerkt en gebruikt nu het nieuwe domein. |

Voor meer informatie, bezoek de [&#x200B; documentatie van de Ingestie van Gegevens &#x200B;](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] is een volledig beheerde service binnen [!DNL Experience Platform] waarmee wetenschappers gegevens naadloos inzichten kunnen genereren op basis van gegevens en inhoud in Adobe-oplossingen en systemen van derden door Machine Learning Models te maken en te exploiteren. [!DNL Data Science Workspace] is nauw geïntegreerd met [!DNL Experience Platform] en maakt de levenscyclus van de end-to-end gegevenswetenschap mogelijk, inclusief de exploratie en voorbereiding van XDM-gegevens, gevolgd door de ontwikkeling en de exploitatie van Modellen om [!DNL Real-Time Customer Profile] automatisch te verrijken met Inzichten voor het leren van machines.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Planning van de Diensten via UI | Geïntegreerd met [!DNL Experience Platform] Orchestration Service om modeltraining en -scoring te automatiseren met door de gebruiker gedefinieerde schema&#39;s met behulp van de gebruikersinterface. |
| [!DNL Service Gallery] | Blader door, controleer en open de services voor machinaal leren, met de mogelijkheid om geautomatiseerde training en scoring taken te plannen, allemaal in de nieuwe versie [!DNL Service Gallery] . |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Verbeteringen in de gebruikersinterface. |

**Bekende kwesties**

* Er is momenteel geen toegankelijke manier in [!DNL Service Gallery] om een bestaande service te verwijderen. Ondertussen, gelieve te verwijzen naar de [&#x200B; het Leren API van de Machine van Sensei verwijzing &#x200B;](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) om een bestaande Dienst door API vraag te schrappen.
* [!DNL Service Gallery] heeft geen pagineringssteun om de opleiding en het scoring looppas van de Dienst te filtreren.
* Wanneer u de geplande training of scoring configureert, wordt de frequentie op uur ingesteld, zodat het programma niet wordt toegepast. [!DNL Service Gallery]

Voor meer informatie, bezoek het [&#x200B; Overzicht van Workspace van de Wetenschap van Gegevens &#x200B;](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] biedt de mogelijkheid om standaard-SQL te gebruiken voor het uitvoeren van query&#39;s op gegevens in Adobe Experience Platform ter ondersteuning van verschillende gebruiksgevallen voor analyses en gegevensbeheer. Het is een serverloos hulpmiddel dat u toestaat om zich bij datasets van [!DNL Data Lake] aan te sluiten en de vraagresultaten te vangen als nieuwe dataset voor gebruik in het melden, [!DNL Data Science Workspace], of voor opname in [!DNL Real-Time Customer Profile].

Met [!DNL Query Service] kunt u gegevensanalysecosystemen samenstellen, zodat u een beeld krijgt van klanten in hun verschillende interactiekanalen. Deze kanalen kunnen verkooppuntsystemen, web-, mobiele of CRM-systemen omvatten.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen in [!DNL Query Editor] | Er is een opslagfunctie toegevoegd waarmee u een query kunt opslaan en er later aan kunt werken. Het tabblad &quot;Bladeren&quot; is toegevoegd aan de gebruikersinterface van [!DNL Query Service] in Adobe Experience Platform waarin query&#39;s worden weergegeven die zijn opgeslagen door gebruikers in uw organisatie. Het deelvenster &quot;Query-details&quot; is geïmplementeerd waarin nuttige metagegevens worden weergegeven over de query die wordt weergegeven. |
| Nieuwe toewijzingsfuncties | Adobe-gedefinieerde functies in [!DNL Query Service] om te zoeken naar kanaaltoewijzing met vervalparameters. |
| Verbeteringen in SQL-syntaxis | Ondersteuning voor ilike-syntaxis. |
| Gegevenssets genereren met een gedefinieerd XDM-schema | Een nieuwe clausule in Create Lijst als Uitgezochte vragen (CTAS) toegevoegd die u toestaat om een doelschema te specificeren. |

Voor meer informatie, verwijs naar de [&#x200B; documentatie van de Dienst van de Vraag &#x200B;](../../query-service/home.md).
