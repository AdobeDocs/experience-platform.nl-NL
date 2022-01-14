---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;het oplossen van problemengids;faq;het oplossen van problemen;
solution: Experience Platform
title: Handleiding voor het oplossen van problemen bij Query Service
topic-legacy: troubleshooting
description: Dit document bevat informatie over algemene foutcodes die u tegenkomt en de mogelijke oorzaken.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: ac313e2a23037507c95d6713a83ad5ca07e1cd85
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 4%

---

# [!DNL Query Service] gids voor problemen

Dit document verstrekt antwoorden op vaak gestelde vragen over de Dienst van de Vraag en verstrekt een lijst van algemeen gezien foutencodes wanneer het gebruiken van de Dienst van de Vraag. Voor vragen en problemen met betrekking tot andere services in Adobe Experience Platform raadpleegt u de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

## Veelgestelde vragen

Hier volgt een lijst met antwoorden op veelgestelde vragen over Query Service.

### Hoe kan ik slechts de meta-gegevens voor een vraag krijgen?

Als u alleen de metagegevens voor een query wilt ophalen, kunt u als volgt een query uitvoeren die nul rijen retourneert:

```sql
SELECT * FROM <table> WHERE 1=0
```

Deze query retourneert alleen de metagegevens voor de opgegeven tabel.

### Hoe kan ik snel op een vraag herhalen CTAS (Creeer Lijst zoals Uitgezochte) zonder het materialiseren?

U kunt tijdelijke lijsten tot stand brengen om een vraag snel te herhalen en te experimenteren alvorens het voor gebruik materializing. U kunt tijdelijke lijsten ook gebruiken om te bevestigen als een vraag functioneel is.

U kunt bijvoorbeeld een tijdelijke tabel maken:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Vervolgens kunt u de tijdelijke tabel als volgt gebruiken:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### Hoe moet ik mijn tijdreeksgegevens filteren?

Wanneer u gegevens uit tijdreeksen opvraagt, moet u het tijdstempelfilter gebruiken wanneer dat mogelijk is voor nauwkeurigere analyse.

>[!NOTE]
>
> De datumtekenreeks **moet** heeft de notatie `yyyy-mm-ddTHH24:MM:SS`.

Hieronder ziet u een voorbeeld van het gebruik van het tijdstempelfilter:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### Moet ik vervangingen, zoals * gebruiken om alle rijen van mijn datasets te krijgen?

U kunt geen vervangingen gebruiken om alle gegevens van uw rijen te krijgen, aangezien de Dienst van de Vraag als a zou moeten worden behandeld **columnar-store** in plaats van een traditioneel opslagsysteem op basis van rijen.

### Moet ik gebruiken `NOT IN` in mijn SQL-query?

De `NOT IN` wordt vaak gebruikt om rijen op te halen die niet in een andere lijst of SQL verklaring worden gevonden. Deze operator kan de prestaties vertragen en onverwachte resultaten opleveren als de kolommen die worden vergeleken, accepteren `NOT NULL`of u hebt een groot aantal records.

In plaats van `NOT IN`kunt u beide `NOT EXISTS` of `LEFT OUTER JOIN`.

Als u bijvoorbeeld de volgende tabellen hebt gemaakt:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Als u het `NOT EXISTS` -operator, kunt u repliceren met de `NOT IN` operator door de volgende query te gebruiken:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

U kunt ook de opdracht `LEFT OUTER JOIN` operator, kunt u repliceren met de `NOT IN` operator door de volgende query te gebruiken:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### Wat is het correcte gebruik van `OR` en `UNION` operatoren?

### Hoe gebruik ik de `CAST` operator om mijn tijdstempels om te zetten in SQL query&#39;s?

Wanneer u de `CAST` om een tijdstempel om te zetten, moet u beide datums opnemen **en** tijd.

Als bijvoorbeeld de tijdcomponent ontbreekt, zoals hieronder wordt weergegeven, resulteert dit in een fout:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Een correct gebruik van de `CAST` operator wordt hieronder weergegeven:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### Hoe kan ik mijn vraagresultaten als Csv- dossier downloaden?

Dit is geen functie die Query Service rechtstreeks aanbiedt. Als de [!DNL PostgreSQL] client gebruikt om verbinding te maken met de databaseserver heeft de mogelijkheid, de reactie van een SELECT-query kan worden geschreven en gedownload als een CSV-bestand. Raadpleeg de documentatie bij het hulpprogramma of het hulpprogramma van derden dat u gebruikt voor meer informatie over dit proces.

## REST API-fouten

| HTTP-statuscode | Beschrijving | Mogelijke oorzaken |
| ---------------- | ----------- | --------------- |
| 400 | Ongeldig verzoek | Onjuiste of ongeldige query |
| 401 | Verificatie mislukt | Ongeldig auteur-token |
| 500 | Interne serverfout | Interne systeemfout |

## PostSQL API-fouten

| Foutcode | Verbindingsstatus | Beschrijving | Mogelijke oorzaak |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | N.v.t. | Niet-ondersteund berichttype | Niet-ondersteund berichttype |
| **28P01** | Opstarten - verificatie | Ongeldig wachtwoord | Ongeldig verificatietoken |
| **28000** | Opstarten - verificatie | Ongeldig autorisatietype | Ongeldig autorisatietype. Moet `AuthenticationCleartextPassword`. |
| **42P12** | Opstarten - verificatie | Geen tabellen gevonden | Geen tabellen gevonden voor gebruik |
| **42601** | Query | Syntaxisfout | Ongeldige opdracht- of syntaxisfout |
| **42P01** | Query | Tabel niet gevonden | Tabel die is opgegeven in de query, is niet gevonden |
| **42P07** | Query | Tabel bestaat | Er bestaat al een tabel met dezelfde naam (CREATE TABLE) |
| **53400** | Query | LIMIT overschrijdt max. waarde | Gebruiker heeft een LIMIT-component opgegeven die hoger is dan 100.000 |
| **53400** | Query | Time-out instructie | De ingediende liveverklaring nam meer dan maximaal 10 minuten in beslag |
| **58000** | Query | Systeemfout | Interne systeemfout |
| **0A000** | Query/opdracht | Niet ondersteund | De functie/functionaliteit in de query/opdracht wordt niet ondersteund |
| **42501** | DROP TABLE-query | Droptable not created by Query Service | De lijst die wordt gelaten vallen werd niet gecreeerd door de Dienst van de Vraag gebruikend `CREATE TABLE` statement |
| **42501** | DROP TABLE-query | Tabel niet gemaakt door de geverifieerde gebruiker | De lijst die wordt gelaten vallen werd niet gecreeerd door de momenteel het programma geopende gebruiker |
| **42P01** | DROP TABLE-query | Tabel niet gevonden | De tabel die in de query is opgegeven, is niet gevonden |
| **42P12** | DROP TABLE-query | Geen tabel gevonden voor `dbName`: gelieve de `dbName` | Er zijn geen tabellen gevonden in de huidige database |
