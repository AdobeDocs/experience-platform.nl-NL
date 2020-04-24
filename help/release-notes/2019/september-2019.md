---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform van 10 september 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498

---


# Opmerkingen bij de release Adobe Experience Platform

**Releasedatum: 10 september 2019**

Updates voor bestaande functies in het Adobe Experience Platform:

* [Gegevensinname](#ingestion)
* [Werkruimte voor gegevenswetenschap](#dsw)
* [Query-service](#query)

## Gegevensinname {#ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het opnemen van elk type en elke vertraging van gegevens. Adobe Experience Platform Data Ingestie biedt meerdere alternatieven voor het opnemen van gegevens, zoals batch-API&#39;s, streaming API&#39;s, native Adobe-connectors, partners voor gegevensintegratie of de gebruikersinterface van het Adobe Experience Platform.

**Nieuwe functies**

| Functie | Beschrijving |
| ----------- | ---------- |
| Nieuw domein voor streaming invoer | Het `dcs.data.adobe.net` domein is verplaatst naar het nieuwe gemeenschappelijke domein voor gegevensverzameling `dcs.adobedc.net`. Gebruikers moeten hun implementaties bijwerken volgens de herziene streamingdocumentatie van het Adobe Experience Platform. Alle documentatie met betrekking tot streamingopname voor het Adobe Experience Platform is bijgewerkt en gebruikt nu het nieuwe domein. |

Voor meer informatie, bezoek de documentatie [van de](../../ingestion/home.md)Ingestie van Gegevens.

## Werkruimte voor gegevenswetenschap {#dsw}

De Werkruimte van de Wetenschap van het Platform van de Gegevens van het Platform van de Ervaring van Adobe is een volledig beheerde dienst binnen het Platform van de Ervaring die gegevenswetenschappers toelaat om inzichten van gegevens en inhoud over de oplossingen van Adobe en derdesystemen naadloos te produceren door de Modellen van het Leren van de Machine te bouwen en in werking te stellen. De Werkruimte van de Wetenschap van Gegevens is strak geïntegreerd met Platform en machtigt de levenscyclus van de gegevenswetenschap van begin tot eind, met inbegrip van exploratie en voorbereiding van XDM gegevens, die door de ontwikkeling en de verrichting van Modellen wordt gevolgd om het Profiel van de Klant in real time met de Inzichten van het Leren van de Machine automatisch te verrijken.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Planning van de Diensten via UI | Geïntegreerd met de Dienst van de Orchestratie van het Platform om Model opleiding en het scoren met user-defined programma&#39;s te automatiseren gebruikend UI. |
| Servicegalerie | Blader naar, monitor en toegang tot services voor machinaal leren met de mogelijkheid om geautomatiseerde training en scoring taken te plannen, allemaal in de herontworpen servicegalerie. |
| JupyterLab 5.0.0 | Verbeteringen in de gebruikersinterface van JupyterLab. |

**Bekende problemen**

* Er is momenteel geen toegankelijke manier in de Galerij van de Dienst om een bestaande Dienst te schrappen. In de tussentijd raadpleegt u de API-naslaggids [voor het leren van](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei-machines om een bestaande service te verwijderen via API-aanroepen.
* De galerie van de Dienst heeft pagineringssteun niet om de opleiding en het scoren van de Dienst looppas van de Dienst te filtreren.
* Wanneer het vormen van geplande opleiding of het scoren looppas door de Galerij van de Dienst, die de frequentie plaatst om het programma te verhinderen worden toegepast.

Voor meer informatie, bezoek het Overzicht [van de Werkruimte van de Wetenschap van](../../data-science-workspace/home.md)Gegevens.

## Query-service {#query}

De Dienst van de vraag verstrekt de capaciteit om standaardSQL aan vraaggegevens in het Platform van de Ervaring van Adobe te gebruiken om een verscheidenheid van analyse en gegevensbeheer gebruiksgevallen te steunen. Het is een serverloos hulpmiddel dat u toestaat om zich bij datasets van het meer van Gegevens aan te sluiten en de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time te vangen.

U kunt de Dienst van de Vraag gebruiken om de ecosystemen van de gegevensanalyse te bouwen, die tot een beeld van klanten over hun diverse interactiekanalen leiden. Deze kanalen kunnen verkooppuntsystemen, web-, mobiele of CRM-systemen omvatten.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen aan de Redacteur van de Vraag | Er is een opslagfunctie toegevoegd waarmee u een query kunt opslaan en er later aan kunt werken. Het tabblad &quot;Bladeren&quot; is toegevoegd aan de gebruikersinterface van de Query-service op het Adobe Experience Platform, waarin query&#39;s worden weergegeven die zijn opgeslagen door gebruikers in uw organisatie. Het deelvenster &quot;Query-details&quot; is geïmplementeerd waarin nuttige metagegevens worden weergegeven over de query die wordt weergegeven. |
| Nieuwe toewijzingsfuncties | Door Adobe gedefinieerde functies in Query Service om te zoeken naar kanaaltoewijzing met vervalparameters. |
| Verbeteringen in SQL-syntaxis | Ondersteuning voor ilike-syntaxis. |
| Gegevenssets genereren met een gedefinieerd XDM-schema | Een nieuwe clausule in Create Lijst als Uitgezochte vragen (CTAS) toegevoegd die u toestaat om een doelschema te specificeren. |

Raadpleeg de documentatie [van de](../../query-service/home.md)Query Service voor meer informatie.