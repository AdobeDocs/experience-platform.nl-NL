---
keywords: Experience Platform;thuis;populaire onderwerpen;PSQL;psql;de dienst van de Vraag;de vraagdienst;meta-gegevens;bevelen;meta-gegevensbevelen;
solution: Experience Platform
title: Metadata PostgreSQL-opdrachten in Query Service
description: Een lijst met PostgreSQL-opdrachten die momenteel worden ondersteund voor het opvragen van metagegevens in Adobe Experience Platform Query Service.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Metagegevens [!DNL PostgreSQL] opdrachten in Query Service

Voor meta-gegevens op uw dataset, worden de volgende [!DNL PostgreSQL] bevelen momenteel gesteund voor het vragen:

>[!NOTE]
>
>De onderstaande opdrachten zijn hoofdlettergevoelig.

| Opdracht | Beschrijving |
|------- | ------------|
| `\conninfo` | Uitvoergegevens over de huidige databaseverbinding. |
| `\d` | Hiermee geeft u een lijst weer met alle zichtbare tabellen, weergaven, gematerialiseerde weergaven, reeksen en externe tabellen. |
| `\dE` | Hiermee geeft u een lijst met externe tabellen weer. |
| `\df or \df+` | Hiermee geeft u een lijst met functies weer. |
| `\di` | Hiermee geeft u een lijst met indexen weer. |
| `\dm` | Hiermee geeft u een lijst met gematerialiseerde weergaven weer. |
| `\dn` | Hiermee geeft u een lijst met schema&#39;s (naamruimten) weer. |
| `\ds` | Hiermee geeft u een lijst met reeksen weer. |
| `\dS` | Toont een lijst van PostSQL-bepaalde lijsten. |
| `\dt` | Hiermee geeft u een lijst met tabellen weer. |
| `\dT` | Hiermee geeft u een lijst met gegevenstypen weer. |
| `\dv` | Hiermee geeft u een lijst met weergaven weer. |
| `\encoding` | Hier wordt de huidige codering van de tekenset van de client weergegeven. |
| `\errverbose` | Herhaalt het meest recente foutbericht van de server op maximale breedtegraad. |
| `\l or \list` | Toont een lijst van gegevensbestanden in de server. |
| `\set` | Hiermee worden de namen en waarden van alle huidige psql-variabelen weergegeven. |
| `\showtables` | Toont de volgende informatie: <br> naam: De naam waardoor de lijst zal worden bedoeld.<br> datasetId: Identiteitskaart van de dataset die wordt opgeslagen.<br> dataset: De naam van de dataset die wordt opgeslagen.<br> beschrijving: Een beschrijving van de dataset.<br> opgelost: Een booleaanse waarde die verklaart al dan niet de dataset in de huidige zitting wordt opgelost. |
| `\timing` | Hiermee schakelt u de weergave in of uit. De weergave is in milliseconden. Intervallen langer dan één seconde worden weergegeven in minuten:seconden-indeling, waarbij uren- en dagvelden worden toegevoegd wanneer dat nodig is. |

Alle opdrachten die met `\d` beginnen, kunnen worden gecombineerd. U kunt `\dtsn` bijvoorbeeld uitgeven om een lijst van alle lijsten, opeenvolgingen, en schema&#39;s te tonen. In `\d` zelf worden alle zichtbare tabellen, weergaven, gematerialiseerde weergaven en reeksen weergegeven.

Voor extra informatie over de hierboven vermelde bevelen, gelieve te verwijzen naar de documentatie bij [ postgresql.org ](https://www.postgresql.org/docs/10/app-psql.html). Niet alle opties in de [!DNL PostgreSQL] -documentatie worden echter ondersteund door [!DNL Experience Platform] .
