---
title: Handleiding voor Privacy Service-API
description: Leer hoe u de Privacy Service-API kunt gebruiken voor het programmatisch beheren van privacytaken voor ondersteunde Adobe Experience Cloud-toepassingen.
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# [!DNL Privacy Service] API-handleiding

De Privacy Service-API bevat verschillende eindpunten waarmee u via programmacode privacytaken voor uw organisatie kunt beheren. Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

>[!NOTE]
>
>In deze handleiding wordt uitgelegd hoe u de [!DNL Privacy Service] API. Voor meer informatie over het gebruik van de gebruikersinterface raadpleegt u de [Overzicht van de gebruikersinterface voor Privacys Service](../ui/overview.md).

Ga naar de [Privacy Service API-naslaggids](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Privacytaken

Wanneer de Privacy Service een verzoek ontvangt om toegang te krijgen tot of de persoonsgegevens van een onderwerp te verwijderen, creëert het systeem privacytaken om aan dat verzoek te voldoen. Elke privacytaak bevat identiteitsgegevens die betrekking hebben op de betrokkene, metagegevens over het Adobe Experience Cloud-product waarop de taak van toepassing is en de verwerkingsstatus van de taak.

De `/jobs` het eindpunt staat u toe om privacybanen voor uw organisatie tot stand te brengen en terug te winnen. Om te leren hoe te om dit eindpunt te gebruiken, zie [eindgebruikershandleiding voor privacytaken](./privacy-jobs.md).

## Toestemming

Bepaalde voorschriften vereisen uitdrukkelijke toestemming van de klant voordat de persoonsgegevens kunnen worden verzameld. De `/consent` het eindpunt staat u toe om verzoeken van de klantentoestemming te verwerken en hen in uw privacywerkschema te integreren. Zie de [leidraad voor het eindpunt van de overeenkomst](./consent.md) voor meer informatie.

## Volgende stappen

Als u begint met het maken van aanroepen met de Privacy Service-API, leest u de [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.
