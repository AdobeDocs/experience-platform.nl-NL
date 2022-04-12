---
title: Referentie voor test met tagaanwezigheid
description: Leer hoe de controlefunctie de aanwezigheid van tags in Adobe Experience Platform Debugger test.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 5%

---

# Referentie voor de test met de aanwezigheid van de tag

Deze verwijzing verstrekt meer informatie over hoe de controleureigenschap in Debugger van Adobe Experience Platform op markeringsaanwezigheid test.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Foutopsporing van het Platform, zie [overzicht van de controlefunctie](./overview.md).

Tests met tagaanwezigheid evalueren of bepaalde tags op de pagina voorkomen en of deze zich op de juiste plaats in de paginacode bevinden.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Advertising Cloud - Code-aanwezigheid | 5 | De Advertising Cloud-tag is niet beschikbaar in het DOM. | Implementeer de Advertising Cloud-tag met de [Advertising Cloud-tagextensie](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Geïmplementeerde segmentpixel | 5 | Upgrade de Advertising Cloud-segmentpixels naar de nieuwe Advertising Cloud-tags voor alleen afbeeldingen. Het gebruik van verouderde AMO-segmenttags kan leiden tot gegevensverlies. | Implementeer de Advertising Cloud-segmentpixel met de [Advertising Cloud-tagextensie](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analyse - geladen in DOM | 5 | De Adobe Analytics-tag is niet gedetecteerd. | Installeer de nieuwste versie van Analytics. <br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Starten - Bibliotheek geladen | 5 | A `global _satellite` object niet gevonden in het DOM, wat betekent dat de tagbibliotheek niet is geïnstalleerd of niet kan worden uitgevoerd. | Controleer of de tagbibliotheek op de pagina is geïmplementeerd en niet wordt geblokkeerd door volgende scriptactiviteiten. |
| Starten - Er zijn niet meerdere ingesloten scripts | 5 | Productieplaatsen mogen slechts één insluitcode per pagina laden. | Controleer of alleen de productiebibliotheek op de pagina wordt geladen. |
| Starten - `pageBottom` callback bestaat in `<body>` | 5 | De vereiste `_satellite.pageBottom()` callback is niet gevonden in het dialoogvenster `<body>` van de pagina. Deze test mislukt als de `pageBottom` de vraag wordt niet gevonden bij allen op de pagina, of als het in `<head>` -tag (of een andere onverwachte locatie). Het gaat alleen door als `pageBottom` bevindt zich ergens in de `<body>` tag. | Voeg het inlinescript onmiddellijk vóór het sluiten toe `</body>` -tags gebruiken voor de juiste functionaliteit van tags.<br><br>[Aanvullende informatie](../../tags/ui/client-side/asynchronous-deployment.md) |
| Starten - `pageBottom` callback zou niet moeten bestaan wanneer asynchroon opgesteld | 5 | De `_satellite.pageBottom()` callback is gevonden op de pagina, wat niet het geval zou moeten zijn wanneer de markeringen asynchroon worden opgesteld. | Verwijder de `_satellite.pageBottom()` script om de juiste tagfunctionaliteit in te schakelen. <br><br>[Aanvullende informatie](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID-service - Code-aanwezigheid | 5 | De Experience Cloud ID-servicecode is niet gevonden. Het gebruik van Experience Cloud-id&#39;s (ECID&#39;s) wordt ten zeerste aanbevolen om ervoor te zorgen dat u de meeste waarde uit uw Experience Cloud-oplossingen haalt en is van essentieel belang voor het beheer van id&#39;s in verschillende Experience Cloud-oplossingen. | Installeer de meest recente versie van ECID.<br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) |
| Experience Cloud ID-service - aanwezigheid cookie | 5 | De `AMCV_` cookie niet gevonden. U moet een bezoekersobject instantiëren vanuit het dialoogvenster `VisitorAPI.js` code. | Als dit een implementatie van tags is, controleert u of de AdobeOrg-id correct is ingevoerd in de ECID-tool. <br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud ID-service - MID-waarde aanwezig | 5 | De MID-waarde is niet gevonden in het dialoogvenster `AMCV_` cookie. | Test opnieuw om te controleren op een eventuele vertraging van de ECID API. Neem contact op met de klantenservice van Adobe als de aandoening aanhoudt. <br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Doel - Code-aanwezigheid | 5 | Adobe Target moet in het DOM worden gedefinieerd. | Installeer de meest recente versie van Target (at.js). <br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Doel - Bibliotheek geladen in `<head>` | 4 | De doelbibliotheek moet in het dialoogvenster `<head>` tag. | Controleer of de doelbibliotheek is geladen in het dialoogvenster `<head>` tag. <br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
