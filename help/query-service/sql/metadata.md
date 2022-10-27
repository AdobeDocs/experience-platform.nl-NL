---
keywords: Experience Platform;thuis;populaire onderwerpen;PSQL;psql;de dienst van de Vraag;de vraagdienst;meta-gegevens;bevelen;meta-gegevensbevelen;
solution: Experience Platform
title: Metadata PostgreSQL-opdrachten in Query Service
topic-legacy: metadata
description: Een lijst met PostgreSQL-opdrachten die momenteel worden ondersteund voor het opvragen van metagegevens in Adobe Experience Platform Query Service.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Metagegevens [!DNL PostgreSQL] opdrachten in Query-service

Voor meta-gegevens op uw dataset, het volgende [!DNL PostgreSQL] opdrachten worden momenteel ondersteund voor het opvragen van:

>[!NOTE]
>
>De onderstaande opdrachten zijn hoofdlettergevoelig.

| Opdracht | Beschrijving |
|------- | ------------|
| `\conninfo` | Uitvoergegevens over de huidige databaseverbinding. |
| `\d` | Hiermee geeft u een lijst weer met alle zichtbare tabellen, weergaven, gematerialiseerde weergaven, reeksen en externe tabellen. |
| `\dE` | Hiermee geeft u een lijst met externe tabellen weer. |
| `\df or \df+` | Hiermee wordt een lijst met functies weergegeven. |
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
| `\showtables` | Hier worden de volgende gegevens weergegeven: <br>naam: De naam waarmee naar de tabel wordt verwezen.<br>datasetId: De id van de gegevensset die wordt opgeslagen.<br>gegevensset: De naam van de gegevensset die wordt opgeslagen.<br>beschrijving: Een beschrijving van de gegevensset.<br>opgelost: Een booleaanse waarde die aangeeft of de dataset in de huidige sessie wordt opgelost. |
| `\timing` | Hiermee schakelt u de weergave in of uit. De weergave is in milliseconden. Intervallen langer dan één seconde worden weergegeven in minuten:seconden-indeling, waarbij uren- en dagvelden worden toegevoegd wanneer dat nodig is. |

Alle opdrachten die beginnen met `\d` kan worden gecombineerd. U kunt bijvoorbeeld `\dtsn` om een lijst van alle lijsten, opeenvolgingen, en schema&#39;s te tonen. `\d` op zichzelf toont alle zichtbare tabellen, weergaven, gematerialiseerde weergaven en reeksen.

Raadpleeg voor meer informatie over de bovenstaande opdrachten de documentatie op [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Houd er echter rekening mee dat niet alle opties in het dialoogvenster [!DNL PostgreSQL] documentatie wordt ondersteund door [!DNL Experience Platform].
