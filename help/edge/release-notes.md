---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
seo-title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: Opmerkingen bij de release van Adobe Experience Platform Web SDK.
seo-description: Opmerkingen bij de release van Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Release-opmerkingen

## Versie 2.3.0

* Nonce-ondersteuning toegevoegd om een strenger beleid voor inhoudsbeveiliging mogelijk te maken.
* Extra ondersteuning voor personalisatie voor toepassingen van één pagina.
* Verbeterde compatibiliteit met andere JavaScript-code op de pagina die mogelijk API&#39; `window.console` s overschrijft.
* Opgeloste problemen: `sendBeacon` werd niet gebruikt toen `documentUnloading` werd geplaatst aan `true` of wanneer de verbinding klikte automatisch werd gevolgd.
* Opgeloste problemen: Een koppeling wordt niet automatisch bijgehouden als het ankerelement HTML-inhoud bevat.
* Opgeloste problemen: Bepaalde browserfouten met een alleen-lezen- `message` eigenschap zijn niet correct verwerkt, waardoor een andere fout aan de klant wordt gemeld.
* Opgeloste problemen: Als de SDK in een iframe wordt uitgevoerd, treedt een fout op als de HTML-pagina van het iframe afkomstig is uit een ander subdomein dan de HTML-pagina van het bovenliggende venster.

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
