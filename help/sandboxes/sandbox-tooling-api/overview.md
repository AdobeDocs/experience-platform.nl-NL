---
title: Handleiding voor sandbox Tooling-API
description: Met sandboxgereedschappen in Adobe Experience Platform kunt u een momentopname van sandboxconfiguraties tussen sandboxen exporteren en importeren.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# [!DNL Sandbox] API-handleiding voor gereedschappen

De API voor gereedschappen van [!DNL Sandbox] biedt verschillende eindpunten waarmee u momentopnamen kunt exporteren en importeren tussen sandboxen die binnen uw organisatie voor u beschikbaar zijn. Alle interacties vinden plaats via HTTP-eindpunten. De bronsandbox wordt gecontroleerd op artefacten (de objecten in een pakket) voordat een momentopname wordt geëxporteerd. Wanneer een importverzoek wordt gedaan, wordt een [!DNL Azure Blob] momentopname verkregen en als malplaatje gebruikt om bijna gelijkaardige artefacten voor de bestemmingszandbak te veroorzaken. Zie het [ zandbak tooling ](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) documentatie voor een lijst van gesteunde voorwerpen en beperkingen.

Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [ begonnen gids ](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

## Pakketten {#packages}

Met het eindpunt van de gereedschapspakketten in de sandbox kunt u pakketten beheren. Het gereedschapspakket voor de sandbox bestaat uit een verzameling artefactdefinities, waaronder pakket-id, naam, beschrijving, org-id en maker-id. Zie de [ gids van het pakketeindpunt ](./packages.md) voor meer informatie bij het werken met pakketten in API.

## Tools {#tools}

Met het eindpunt van de gereedschappen voor sandboxgereedschappen kunt u de JSON-taakgegevens onafhankelijk ophalen. Zie de [ gids van het hulpmiddeleindpunt ](./tools.md) voor meer informatie bij het terugwinnen van baanJSON gegevens in API.

## Volgende stappen {#next-steps}

Beginnen makend vraag gebruikend zandbak het gebruiken van API, lees [ begonnen gids ](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
