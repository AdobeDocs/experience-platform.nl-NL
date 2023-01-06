---
keywords: Experience Platform;voorvoegsel van gegevens;voorinstelling van gegevens, api;problemen oplossen;API
title: Overzicht van de API voor gegevenprep
description: Met de Data Prep-API kunt u via programmacode toewijzingssets en functies maken, zodat u uw gegevens kunt transformeren tussen bron- en doelschema's.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Handleiding Mapping Service API

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model). De Prep van gegevens verschijnt als &quot;Kaart&quot;stap in de processen van de Ingestie van Gegevens, met inbegrip van CSV Ingestiewerkschema.

De Mapping Service API, ook wel de Data Prep API genoemd, bevat meerdere eindpunten die hieronder worden beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

## Functies

Met toewijzingsfuncties kunt u gegevens transformeren tussen bron- en doelschema&#39;s. U kunt de `/languages/el` eindpunt om uw uitdrukkingen te bevestigen evenals een lijst van alle beschikbare afbeelding-vastgestelde functies en verrichtingen te krijgen.

Lees voor gedetailleerde informatie over het gebruik van toewijzingsfuncties de [Functiepuntgids](./functions.md).

## Toewijzingsset

Toewijzingssets kunnen worden gebruikt om te definiëren hoe gegevens in een bronschema worden toegewezen aan dat van een doelschema. U kunt de `/mappingSets` eindpunt in de Prep API van Gegevens om kaartreeksen programmatically terug te winnen, tot stand te brengen bij te werken en te bevestigen.

Lees voor meer informatie over het gebruik van sets voor toewijzingen de [eindhulplijn voor toewijzingstellen](./mapping-set.md).

## Volgende stappen

Als u begint met het maken van aanroepen met de API voor toewijzingsservice, leest u de [gids Aan de slag](./getting-started.md) dan selecteer één van de eindpuntgids om te leren hoe te om de specifieke eindpunten te gebruiken.
