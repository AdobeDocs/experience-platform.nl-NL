---
title: Edge Extension Flow
description: Leer hoe de componenten van een randuitbreiding in Adobe Experience Platform met elkaar in runtime communiceren.
exl-id: 99058e22-3e14-4ec6-858e-bb1c1fafdb7c
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Edge-extensiestroom

In randuitbreidingen heeft elke voorwaarde, actie, en het type van gegevenselement zowel een mening die gebruikers toestaat om montages te wijzigen als een bibliotheekmodule om op die user-defined montages te handelen.

Zoals het volgende diagram op hoog niveau toont, wordt de de actietype mening van de uitbreiding getoond binnen iframe binnen de toepassing die met Adobe Experience Platform wordt geïntegreerd. De weergave wordt vervolgens gebruikt om instellingen te wijzigen die vervolgens in Experience Platform worden opgeslagen. Wanneer de tagruntimebibliotheek is gemaakt, worden zowel de actietype van de extensie-bibliotheekmodule als de door de gebruiker gedefinieerde instellingen opgenomen in de runtimebibliotheek die wordt geïmplementeerd op het randknooppunt. Door de gebruiker gedefinieerde instellingen uit Experience Platform worden tijdens runtime in de module Bibliotheek geïnjecteerd.

![&#x200B; diagram van de uitbreidingsstroom &#x200B;](../images/flow/edge/event-processing-flow.png)

In het volgende diagram kunt u het verband tussen gebeurtenissen, voorwaarden en acties binnen de stroom van de regelverwerking zien.

![&#x200B; diagram van de regelverwerking van stroom &#x200B;](../images/flow/edge/rule-processing-flow.png)

De stroom van de regelverwerking bevat de volgende fasen:

1. De methoden `settings` en `trigger` worden bij het opstarten aan de gebeurtenisbibliotheekmodule geleverd.
1. Wanneer de gebeurtenisbibliotheekmodule bepaalt dat de gebeurtenis heeft plaatsgevonden, roept de gebeurtenisbibliotheekmodule `trigger` aan.
1. Experience Platform geeft `settings` door aan de conditietype-bibliotheekmodules van de regel waar de voorwaarden vervolgens worden geëvalueerd.
1. Elk voorwaardetype keert terug of een voorwaarde aan waar evalueert.
1. Als alle voorwaarden overgaan, worden de acties van de regel uitgevoerd.
