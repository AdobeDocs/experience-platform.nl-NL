---
title: Referentie voor test met tagaanwezigheid
description: Leer hoe de controleur op markeringsaanwezigheid in Adobe Experience Platform Debugger test.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---

# Referentie voor de test met de aanwezigheid van de tag

Deze verwijzing verstrekt meer informatie over hoe de controleureigenschap in Adobe Experience Platform Debugger op markeringsaanwezigheid test.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Debugger van het Platform, zie het [ overzicht van de controleeigenschap ](./overview.md).

Tests met de aanwezigheid van tags evalueren of bepaalde tags op de pagina voorkomen en of deze zich op de juiste plaats in de paginacode bevinden.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Advertising Cloud - Code-aanwezigheid | 5 | De Advertising Cloud-tag is niet beschikbaar in het DOM. | Voer de markering van Advertising Cloud uit gebruikend de [ de markeringsuitbreiding van Advertising Cloud ](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Geïmplementeerde segmentpixel | 5 | Upgrade de Advertising Cloud-segmentpixels naar de nieuwe Advertising Cloud-tags voor alleen afbeeldingen. Het gebruik van verouderde AMO-segmenttags kan leiden tot gegevensverlies. | Voer het het segmentpixel van Advertising Cloud uit gebruikend de [ markeringsuitbreiding van Advertising Cloud ](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analyse - geladen in DOM | 5 | De Adobe Analytics-tag is niet gedetecteerd. | Installeer de nieuwste versie van Analytics. <br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Starten - Bibliotheek geladen | 5 | Er is geen `global _satellite` -object gevonden in het DOM, wat betekent dat de tagbibliotheek niet is geïnstalleerd of niet kan worden uitgevoerd. | Controleer of de tagbibliotheek op de pagina is geïmplementeerd en niet wordt geblokkeerd door volgende scriptactiviteiten. |
| Starten - Er zijn niet meerdere ingesloten scripts | 5 | Productieplaatsen mogen slechts één insluitcode per pagina laden. | Controleer of alleen de productiebibliotheek op de pagina wordt geladen. |
| Starten - `pageBottom` callback bestaat in `<body>` | 5 | De vereiste callback van `_satellite.pageBottom()` is niet gevonden in `<body>` van de pagina. Deze test mislukt als de aanroep van `pageBottom` helemaal niet op de pagina staat of als deze in de tag `<head>` staat (of op een andere onverwachte locatie). Deze wordt alleen doorgegeven als `pageBottom` zich ergens binnen de tag `<body>` bevindt. | Voeg het inlinescript direct vóór de afsluitende tag `</body>` toe voor de juiste functionaliteit van tags.<br><br>[ Aanvullende informatie ](../../tags/ui/client-side/asynchronous-deployment.md) |
| Starten - callback bestaat niet als deze asynchroon wordt geïmplementeerd`pageBottom` | 5 | De callback van `_satellite.pageBottom()` is gevonden op de pagina, wat niet het geval zou moeten zijn wanneer de markeringen asynchroon worden opgesteld. | Verwijder het script van `_satellite.pageBottom()` om de juiste functionaliteit voor tags in te schakelen. <br><br>[ Aanvullende informatie ](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID Service - Code presence | 5 | De Experience Cloud ID Service-code is niet gevonden. Het gebruik van Experience Cloud-id&#39;s (ECID&#39;s) wordt ten zeerste aanbevolen om ervoor te zorgen dat u de meeste waarde uit uw Experience Cloud-oplossingen haalt en is van essentieel belang voor het beheer van id&#39;s in verschillende Experiencen Cloud. | De meest recente versie van ECID installeren.<br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud-id-service - Cookie-aanwezigheid | 5 | Het cookie `AMCV_` is niet gevonden. U moet een bezoekersobject instantiëren vanuit de `VisitorAPI.js` -code. | Als dit een implementatie van tags is, controleert u of de AdobeOrg-id correct is ingevoerd in de ECID-tool. <br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud-id-service - MID-waarde aanwezig | 5 | De MID-waarde is niet gevonden in het cookie `AMCV_` . | Test opnieuw om te controleren op een eventuele vertraging van de ECID API. Neem contact op met de klantenservice van de Adobe als de aandoening aanhoudt. <br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Doel - Code-aanwezigheid | 5 | Adobe Target moet in het DOM worden gedefinieerd. | Installeer de meest recente versie van Target (at.js). <br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Doel - Bibliotheek geladen in `<head>` | 4 | De doelbibliotheek moet in de tag `<head>` worden geladen. | Controleer of de doelbibliotheek is geladen in de tag `<head>` . <br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
