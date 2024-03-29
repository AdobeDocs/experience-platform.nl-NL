---
title: Edge Extension Flow
description: Leer hoe de componenten van een randuitbreiding in Adobe Experience Platform met elkaar in runtime communiceren.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Edge-extensiestroom

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In randuitbreidingen heeft elke voorwaarde, actie, en het type van gegevenselement zowel een mening die gebruikers toestaat om montages te wijzigen als een bibliotheekmodule om op die user-defined montages te handelen.

Zoals het volgende diagram op hoog niveau toont, wordt de de actietype mening van de uitbreiding getoond binnen iframe binnen de toepassing die met Adobe Experience Platform wordt geïntegreerd. De weergave wordt vervolgens gebruikt om instellingen te wijzigen die vervolgens in het Platform worden opgeslagen. Wanneer de tagruntimebibliotheek is gemaakt, worden zowel de actietype van de extensie-bibliotheekmodule als de door de gebruiker gedefinieerde instellingen opgenomen in de runtimebibliotheek die wordt geïmplementeerd op het randknooppunt. Door de gebruiker gedefinieerde instellingen uit het Platform worden tijdens runtime in de module Bibliotheek geïnjecteerd.

![extensiestroom diagram](../images/flow/edge/event-processing-flow.png)

In het volgende diagram kunt u het verband tussen gebeurtenissen, voorwaarden en acties binnen de stroom van de regelverwerking zien.

![regelverwerkingsstroomdiagram](../images/flow/edge/rule-processing-flow.png)

De stroom van de regelverwerking bevat de volgende fasen:

1. De `settings` en de `trigger` Deze methode wordt bij het opstarten aan de module van de gebeurtenisbibliotheek gegeven.
1. Wanneer de module van de gebeurtenisbibliotheek bepaalt de gebeurtenis is voorgekomen, roept de module van de gebeurtenisbibliotheek `trigger`.
1. Platform passeert `settings` in de voorwaarde-type van de regel bibliotheekmodules waar de voorwaarden dan worden geëvalueerd.
1. Elk voorwaardetype keert terug of een voorwaarde aan waar evalueert.
1. Als alle voorwaarden overgaan, worden de acties van de regel uitgevoerd.
