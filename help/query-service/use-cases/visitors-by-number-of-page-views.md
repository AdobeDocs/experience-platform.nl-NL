---
keywords: Experience Platform;home;populaire onderwerpen;queryservice;Query-service;ExperienceEvent-query;ExperienceEvent-query;ExperienceEvent-query;
title: Bezoekers weergeven op basis van aantal paginaweergaven
description: Leer hoe u query's schrijft die Experience Events gebruiken om een lijst met bezoekers op te halen die is ingedeeld op basis van het aantal paginaweergaven.
exl-id: 6e8eed0c-838e-4cd0-ae8c-453114fbf4ea
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Bezoekers weergeven op basis van hun aantal paginaweergaven

Dit document bevat een voorbeeld van de SQL-code die nodig is om een lijst met bezoekers op te halen, ingedeeld op basis van het aantal paginaweergaven. Met Adobe Experience Platform Query Service kunt u query&#39;s schrijven die [!DNL Experience Events] gebruiken om verschillende gebruiksgevallen vast te leggen. De Gebeurtenissen van de ervaring worden vertegenwoordigd door de klasse ExperienceEvent van het Gegevensmodel van de Ervaring (XDM), die een onveranderlijke en niet-geaggregeerde momentopname van het systeem vangt wanneer een gebruiker met een website of de dienst interactie aangaat. De Gebeurtenissen van de ervaring kunnen zelfs voor tijd-domeinanalyse worden gebruikt. Zie [&#x200B; volgende stappen sectie &#x200B;](#next-steps) voor meer gebruiksgevallen die [!DNL Experience Events] impliceren om bezoekersrapporten te produceren.

Meer informatie over XDM en [!DNL Experience Events] kan in het [[!DNL XDM System]  overzicht &#x200B;](../../xdm/home.md) worden gevonden. Door de Dienst van de Vraag met [!DNL Experience Events] te combineren, kunt u gedragstendensen onder uw gebruikers effectief volgen. Het volgende document bevat voorbeelden van query&#39;s die [!DNL Experience Events] betreffen.

## Doelstelling

In het volgende voorbeeld wordt een rapport gemaakt met de tien id&#39;s van de gebruikers die de meeste pagina&#39;s hebben weergegeven.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

De resultaten van de query worden weergegeven in de onderstaande tabel.

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## Volgende stappen {#next-steps}

Door dit document te lezen, hebt u een beter inzicht in hoe u de Query-service met [!DNL Experience Events] kunt gebruiken om gebruikers weer te geven die de meeste pagina&#39;s hebben bekeken.

Raadpleeg de volgende gebruiksgevallen voor meer informatie over andere gebruikte gevallen die door bezoekers worden gebruikt:

- [De vorige sessies van een bezoeker weergeven.](./list-visitor-sessions.md)
- [Een roll-uprapport van een bezoeker weergeven.](./roll-up-report-of-a-visitor.md)
- [Maak een verouderd rapport van gebeurtenissen per dag.](./trended-report-of-events.md)
