---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
seo-title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: Opmerkingen bij de release van Adobe Experience Platform Web SDK.
seo-description: Opmerkingen bij de release van Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 738dfe782ee7d6bef06d14910e0c26540b0ec734
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 1%

---


# Release-opmerkingen

## Versie 2.2.0

* Opgeloste problemen: Het object Opt-in blokkeerde het gebruik van Alloy voor het maken van aanroepen wanneer `idMigrationEnabled` dat wel het geval is `true`.
* Opgeloste problemen: Alloy bewust maken van verzoeken die de aanbiedingen van de verpersoonlijking zouden moeten terugkeren om een flikkerende kwestie te verhinderen.

## Versie 2.1.0

* Verwijder het `syncIdentity` bevel en steun die die IDs in het `sendEvent` bevel overgaan.
* Ondersteuning voor IAB 2.0 Consent Standard.
* Ondersteuning voor het doorgeven van aanvullende id&#39;s in de `setConsent` opdracht.
* Ondersteuning voor het overschrijven van de opdracht `datasetId` in de `sendEvent` opdracht.
* Ondersteuningslantaarnmonitoren ([meer](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)informatie)
* Geef `environment: browser` de contextgegevens van de implementatiedetails door.
