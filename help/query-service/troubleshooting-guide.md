---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor het oplossen van problemen bij de Query-service van Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda

---


# Fouten en problemen oplossen

## REST API-fouten

| HTTP-statuscode | Beschrijving | Mogelijke oorzaken |
| ---------------- | ----------- | --------------- |
| 400 | Ongeldig verzoek | Onjuiste of ongeldige query |
| 401 | Verificatie mislukt | Ongeldig auteur-token |
| 500 | Interne serverfout | Interne systeemfout |

## PostSQL API-fouten

| Foutcode en verbindingsstatus | Beschrijving | Mogelijke oorzaak |
| ------------------------------- | ----------- | -------------- |
| **28P01** opstarten - verificatie | Ongeldig wachtwoord | Ongeldig verificatietoken |
| **28000** Opstarten - verificatie | Ongeldig autorisatietype | Ongeldig autorisatietype. Moet zijn `AuthenticationCleartextPassword`. |
| **42P12** Opstarten - verificatie | Geen tabellen gevonden | Geen tabellen gevonden voor gebruik |
| **42601** Query | Syntaxisfout | Ongeldige opdracht- of syntaxisfout |
| **58000** Query | Systeemfout | Interne systeemfout |
| **42P01** -query | Tabel niet gevonden | Tabel die is opgegeven in de query, is niet gevonden |
| **42P07** -query | Tabel bestaat | Tabel bestaat al met dezelfde naam (CREATE TABLE) |
| **53400** Query | LIMIT overschrijdt max. waarde | Gebruiker heeft een LIMIT-component opgegeven die hoger is dan 100.000 |
| **53400** Query | Time-out instructie | De ingediende liveverklaring nam meer dan maximaal 10 minuten in beslag |
| **08P01** N.v.t. | Niet-ondersteund berichttype | Niet-ondersteund berichttype |
