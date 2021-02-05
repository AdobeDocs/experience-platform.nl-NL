---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de Vraag;het oplossen van problemengids;faq;het oplossen van problemen;
solution: Experience Platform
title: Handleiding voor het oplossen van problemen bij Query Service
topic: troubleshooting
description: Dit document bevat informatie over algemene foutcodes die u tegenkomt en de mogelijke oorzaken.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 2%

---


# [!DNL Query Service] Handleiding voor probleemoplossing

## REST API-fouten

| HTTP-statuscode | Beschrijving | Mogelijke oorzaken |
| ---------------- | ----------- | --------------- |
| 400 | Ongeldig verzoek | Onjuiste of ongeldige query |
| 401 | Verificatie mislukt | Ongeldig auteur-token |
| 500 | Interne serverfout | Interne systeemfout |

## PostSQL API-fouten

| Foutcode en verbindingsstatus | Beschrijving | Mogelijke oorzaak |
| ------------------------------- | ----------- | -------------- |
| **28P01** Opstarten - verificatie | Ongeldig wachtwoord | Ongeldig verificatietoken |
| **28000** Opstarten - verificatie | Ongeldig autorisatietype | Ongeldig autorisatietype. Moet `AuthenticationCleartextPassword` zijn. |
| **42P12** Opstarten - verificatie | Geen tabellen gevonden | Geen tabellen gevonden voor gebruik |
| **42601** Query | Syntaxisfout | Ongeldige opdracht- of syntaxisfout |
| **58000** Query | Systeemfout | Interne systeemfout |
| **42P01** Query | Tabel niet gevonden | Tabel die is opgegeven in de query, is niet gevonden |
| **42P07** Query | Tabel bestaat | Tabel bestaat al met dezelfde naam (CREATE TABLE) |
| **53400** Query | LIMIT overschrijdt max. waarde | Gebruiker heeft een LIMIT-component opgegeven die hoger is dan 100.000 |
| **53400** Query | Time-out instructie | De ingediende liveverklaring nam meer dan maximaal 10 minuten in beslag |
| **08P01** N.v.t. | Niet-ondersteund berichttype | Niet-ondersteund berichttype |
