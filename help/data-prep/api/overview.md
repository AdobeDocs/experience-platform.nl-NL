---
keywords: Experience Platform;voorvoegsel van gegevens;voorinstelling van gegevens, api;problemen oplossen;API
title: Overzicht van de API voor gegevenprep
topic-legacy: guide
description: Met de Data Prep-API kunt u via programmacode toewijzingssets en functies maken, zodat u uw gegevens kunt transformeren tussen bron- en doelschema's.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Handleiding Mapping Service API

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model). De Prep van gegevens verschijnt als &quot;Kaart&quot;stap in de processen van de Ingestie van Gegevens, met inbegrip van CSV Ingestiewerkschema.

De Mapping Service API, ook wel de Data Prep API genoemd, bevat meerdere eindpunten die hieronder worden beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [begonnen gids](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

## Functies

Met toewijzingsfuncties kunt u gegevens transformeren tussen bron- en doelschema&#39;s. U kunt het `/languages/el` eindpunt gebruiken om uw uitdrukkingen te bevestigen evenals een lijst van alle beschikbare afbeelding-vastgestelde functies en verrichtingen te krijgen.

Voor gedetailleerde informatie over hoe te om afbeelding-vastgestelde functies te gebruiken, gelieve [functies eindpuntgids](./functions.md) te lezen.

## Toewijzingsset

Toewijzingssets kunnen worden gebruikt om te definiëren hoe gegevens in een bronschema worden toegewezen aan dat van een doelschema. U kunt het `/mappingSets` eindpunt in de Prep API van Gegevens gebruiken om kaartreeksen programmatically terug te winnen, tot stand te brengen bij te werken en te bevestigen.

Voor gedetailleerde informatie over hoe te om kaartreeksen te gebruiken, te lezen gelieve [kaartseteindpuntgids](./mapping-set.md).

## Volgende stappen

Als u begint met het maken van aanroepen met behulp van de API voor toewijzingsservice, leest u de [gids Aan de slag](./getting-started.md) en selecteert u vervolgens een van de eindpunthulplijnen om te leren hoe u de specifieke eindpunten kunt gebruiken.
