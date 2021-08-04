---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;het oplossen van problemengids;faq;het oplossen van problemen;
solution: Experience Platform
title: Handleiding voor het oplossen van problemen bij Query Service
topic-legacy: troubleshooting
description: Dit document bevat informatie over algemene foutcodes die u tegenkomt en de mogelijke oorzaken.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 2b118228473a5f07ab7e2c744b799f33a4c44c98
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 5%

---

# [!DNL Query Service] gids voor problemen

Dit document verstrekt antwoorden op vaak gestelde vragen over de Dienst van de Vraag en verstrekt een lijst van algemeen gezien foutencodes wanneer het gebruiken van de Dienst van de Vraag. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot andere services in Adobe Experience Platform.

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

U kunt geen vervangingen gebruiken om alle gegevens van uw rijen te krijgen, aangezien de Dienst van de Vraag als **column-store** eerder dan een traditioneel op rij-gebaseerd opslagsysteem zou moeten worden behandeld.

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
| **28000** | Opstarten - verificatie | Ongeldig autorisatietype | Ongeldig autorisatietype. Moet `AuthenticationCleartextPassword` zijn. |
| **42P12** | Opstarten - verificatie | Geen tabellen gevonden | Geen tabellen gevonden voor gebruik |
| **42601** | Query | Syntaxisfout | Ongeldige opdracht- of syntaxisfout |
| **42P01** | Query | Tabel niet gevonden | Tabel die is opgegeven in de query, is niet gevonden |
| **42P07** | Query | Tabel bestaat | Er bestaat al een tabel met dezelfde naam (CREATE TABLE) |
| **53400** | Query | LIMIT overschrijdt max. waarde | Gebruiker heeft een LIMIT-component opgegeven die hoger is dan 100.000 |
| **53400** | Query | Time-out instructie | De ingediende liveverklaring nam meer dan maximaal 10 minuten in beslag |
| **58000** | Query | Systeemfout | Interne systeemfout |
| **0A000** | Query/opdracht | Niet ondersteund | De functie/functionaliteit in de query/opdracht wordt niet ondersteund |
| **42501** | DROP TABLE-query | Droptable not created by Query Service | De lijst die wordt gelaten vallen werd niet gecreeerd door de Dienst van de Vraag gebruikend de `CREATE TABLE` verklaring |
| **42501** | DROP TABLE-query | Tabel niet gemaakt door de geverifieerde gebruiker | De lijst die wordt gelaten vallen werd niet gecreeerd door de momenteel het programma geopende gebruiker |
| **42P01** | DROP TABLE-query | Tabel niet gevonden | De tabel die in de query is opgegeven, is niet gevonden |
| **42P12** | DROP TABLE-query | Geen tabel gevonden voor `dbName`: gelieve te controleren `dbName` | Er zijn geen tabellen gevonden in de huidige database |
