---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: De recentste versienota's voor het Web SDK van Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;versie nota's;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Releaseopmerkingen

## Versie 2.3.0

* Nonce-ondersteuning toegevoegd om een strenger beleid voor inhoudsbeveiliging mogelijk te maken.
* Extra ondersteuning voor personalisatie voor toepassingen van één pagina.
* Verbeterde compatibiliteit met andere JavaScript-code op de pagina die wellicht API&#39;s van `window.console` overschrijft.
* Opgeloste problemen: `sendBeacon` werd niet gebruikt wanneer `documentUnloading` aan `true` werd geplaatst of wanneer de verbinding kliks automatisch werd gevolgd.
* Opgeloste problemen: Een koppeling wordt niet automatisch bijgehouden als het ankerelement HTML-inhoud bevat.
* Opgeloste problemen: Bepaalde browserfouten met een alleen-lezen `message`-eigenschap zijn niet correct verwerkt, waardoor een andere fout aan de klant wordt gemeld.
* Opgeloste problemen: Als de SDK in een iframe wordt uitgevoerd, treedt een fout op als de HTML-pagina van het iframe afkomstig is uit een ander subdomein dan de HTML-pagina van het bovenliggende venster.

## Versie 2.2.0

* Opgeloste problemen: Het Opt-in voorwerp blokkeerde Alloy om vraag te maken wanneer `idMigrationEnabled` `true` is.
* Opgeloste problemen: Alloy bewust maken van verzoeken die de aanbiedingen van de verpersoonlijking zouden moeten terugkeren om een flikkerende kwestie te verhinderen.

## Versie 2.1.0

* Verwijder het `syncIdentity` bevel en steun die die IDs in het `sendEvent` bevel overgaan.
* Ondersteuning voor IAB 2.0 Consent Standard.
* Ondersteuning voor het doorgeven van aanvullende id&#39;s in de opdracht `setConsent`.
* Ondersteuning voor het overschrijven van `datasetId` in de opdracht `sendEvent`.
* Ondersteuningslantmonitoren ([Meer informatie](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Geef `environment: browser` door in de contextgegevens van de implementatiedetails.
