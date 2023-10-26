---
title: Handleiding voor sandbox Tooling-API
description: Met sandboxgereedschappen in Adobe Experience Platform kunt u een momentopname van sandboxconfiguraties tussen sandboxen exporteren en importeren.
source-git-commit: e4e89c5250885bef177ba0d678629261a361a66d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# [!DNL Sandbox] API-handleiding voor gereedschap

De [!DNL Sandbox] De API voor gereedschappen biedt verschillende eindpunten waarmee u momentopnamen kunt exporteren en importeren tussen sandboxen die binnen uw organisatie voor u beschikbaar zijn. Alle interacties vinden plaats via HTTP-eindpunten. De bronsandbox wordt gecontroleerd op artefacten (de objecten in een pakket) voordat een momentopname wordt geëxporteerd. Wanneer een verzoek tot invoer wordt ingediend, [!DNL Azure Blob] momentopname wordt verkregen en gebruikt als een sjabloon om bijna gelijkaardige artefacten voor de bestemmingszandbak te produceren. Zie de [sandbox, gereedschap](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) documentatie voor een lijst met ondersteunde objecten en beperkingen.

Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

## Pakketten {#packages}

Met het eindpunt van de gereedschapspakketten in de sandbox kunt u pakketten beheren. Het gereedschapspakket voor de sandbox bestaat uit een verzameling artefactdefinities, waaronder pakket-id, naam, beschrijving, org-id en maker-id. Zie de [eindhulplijn voor pakketten](./packages.md) voor meer informatie over het werken met pakketten in de API.

## Tools {#tools}

Met het eindpunt van de gereedschappen voor sandboxgereedschappen kunt u de JSON-taakgegevens onafhankelijk ophalen. Zie de [hulplijn voor eindpunten van gereedschappen](./tools.md) voor meer informatie over het ophalen van JSON-taakgegevens in de API.

## Volgende stappen {#next-steps}

Als u aanroepen wilt uitvoeren met de API voor het gereedschap Sandbox, leest u de [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.
