---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui guide;mapper;mapping;data prep;data voorbereiden;voorbereiden van gegevens;
solution: Experience Platform
title: Overzicht van Data Prep
topic: overview
description: Dit document introduceert Data Prep in Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: 827a593c046530edba701edf26d9a47918cfd8f8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Overzicht van Data Prep

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model). De Prep van gegevens verschijnt als &quot;Kaart&quot;stap in de processen van de Ingestie van Gegevens, met inbegrip van CSV Ingestiewerkschema. De ingenieurs van gegevens kunnen Prep van Gegevens gebruiken om de volgende gegevensmanipulatie tijdens opname uit te voeren:

- Eenvoudige doorvoertoewijzingen definiëren om invoerkenmerken toe te wijzen aan XDM-kenmerken
- Berekende velden maken voor het uitvoeren van berekeningen in rijen die kunnen worden toegewezen aan XDM-kenmerken
- Transformeer de gegevens door tekenreeks-, numerieke of datummanipulatiefuncties toe te passen
- XDM-hiërarchieën maken met behulp van hiërarchische functies
- Een voorvertoning weergeven van de gegevens terwijl deze worden bewerkt in Voorvertoning gegevens

De Prep van gegevens past verscheidene intrinsieke gegevensbevestigingen ook toe om ervoor te zorgen dat de gegevensintegriteit wordt gehandhaafd aangezien het wordt opgenomen. Waar mogelijk worden met Gegevensvoorbeeld de inkomende gegevensschema&#39;s automatisch toegewezen aan XDM. De ingenieurs van gegevens kunnen, de voorgestelde afbeeldingen veranderen verbeteren en schrappen en hen vervangen met de afbeeldingen zoals aangewezen.

## Toewijzing

Een afbeelding is een koppeling van een invoerkenmerk of berekend veld naar één XDM-kenmerk. Eén kenmerk kan aan meerdere XDM-kenmerken worden toegewezen door afzonderlijke toewijzingen te maken.

Lees de [handleiding voor toewijzingsfuncties](./functions.md) voor meer informatie over de verschillende toewijzingsfuncties.

## Toewijzingsset

Een reeks afbeeldingen die een schema in een ander schema omzetten, wordt samen een toewijzingsset genoemd. Er wordt één toewijzingenset gemaakt als onderdeel van elke gegevensstroom. Een toewijzingenset is een integraal onderdeel van de gegevensstromen en wordt gemaakt, bewerkt en bewaakt als onderdeel van de gegevensstromen.

## Gegevensverwerking

De Prep van gegevens kan robuust verschillende formaten van gegevens behandelen die in Platform worden opgenomen. Lees [het overzicht van de verwerking van gegevensformaten](./data-handling.md) voor meer informatie over de manier waarop Data Prep met verschillende gegevenstypen omgaat.

## Volgende stappen

In dit document worden de basisbeginselen van Data Prep in Adobe Experience Platform besproken. Lees de [handleiding voor toewijzingsfuncties](./functions.md) voor meer informatie over verschillende toewijzingsfuncties. Lees de [handleiding voor de verwerking van gegevensformaten](./data-handling.md#dates) voor meer informatie over de manier waarop Data Prep met verschillende gegevenstypen omgaat. Lees voor meer informatie over het gebruik van de Data Prep API de [Data Prep developer guide](api/overview.md).
