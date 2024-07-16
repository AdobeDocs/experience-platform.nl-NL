---
title: Web Extension Flow
description: Leer hoe webextensiecomponenten tijdens runtime in Adobe Experience Platform met elkaar communiceren.
exl-id: 90a0c64c-d240-4e2c-876b-22f05d6f3f82
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Web extension flow

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

In webextensies heeft elk type gebeurtenis, voorwaarde, handeling en gegevenselement zowel een weergave waarmee gebruikers instellingen kunnen wijzigen als een bibliotheekmodule die op deze door de gebruiker gedefinieerde instellingen kan werken.

Zoals het volgende diagram op hoog niveau toont, zal de de gebeurtenistypemening van de uitbreiding binnen iframe binnen de toepassing worden getoond die met Adobe Experience Platform wordt geïntegreerd. De gebruiker gebruikt dan de mening om montages te wijzigen die dan binnen Platform worden bewaard. Wanneer de tagruntimebibliotheek is gemaakt, worden zowel de gebeurtenisbibliotheekmodule van de extensie als de door de gebruiker gedefinieerde instellingen opgenomen in de runtimebibliotheek. Tijdens runtime injecteert Platform de door de gebruiker gedefinieerde instellingen in de module Bibliotheek.

![ diagram van de uitbreidingsstroom ](../images/flow/web/extension-flow.png)

In het volgende diagram kunt u het verband tussen gebeurtenissen, voorwaarden en acties binnen de stroom van de regelverwerking zien.

![ diagram van de regelverwerking van stroom ](../images/flow/web/rule-processing-flow.png)

De stroom van de regelverwerking bevat de volgende fasen:

1. De methoden `settings` en `trigger` worden bij het opstarten aan de gebeurtenisbibliotheekmodule geleverd.
1. Wanneer de gebeurtenisbibliotheekmodule bepaalt dat de gebeurtenis heeft plaatsgevonden, roept de gebeurtenisbibliotheekmodule `trigger` aan.
1. De markeringen gaat `settings` in de modules van de voorwaardenbibliotheek van de regel over waar de voorwaarden worden geëvalueerd.
1. Elke module van de voorwaardenbibliotheek keert terug of een voorwaarde aan waar evalueert.
1. Als alle voorwaarden overgaan, worden de acties van de regel uitgevoerd.
