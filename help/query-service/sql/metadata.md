---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Opdrachten Metagegevens
topic: metadata
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# Opdrachten Metagegevens

Voor meta-gegevens op uw dataset, worden de volgende bevelen PSQL momenteel gesteund voor het vragen:

>[!NOTE] De onderstaande opdrachten zijn hoofdlettergevoelig.

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

Alle opdrachten die beginnen met, `\d` kunnen worden gecombineerd. U kunt bijvoorbeeld een lijst weergeven met alle tabellen, reeksen en schema&#39;s. `\dtsn` `\d` op zichzelf toont alle zichtbare tabellen, weergaven, gematerialiseerde weergaven en reeksen.

Raadpleeg de documentatie op [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html)voor meer informatie over de bovenstaande opdrachten. Houd er echter rekening mee dat niet alle opties in de documentatie bij PostgreSQL worden ondersteund door het Experience Platform.

