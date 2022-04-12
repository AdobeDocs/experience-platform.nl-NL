---
title: Referentie alarmtest
description: Leer hoe de controlefunctie in Adobe Experience Platform Debugger waarschuwingen test.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Referentie alarmtest

Deze verwijzing verstrekt meer informatie over hoe de controleureigenschap in Debugger van Adobe Experience Platform waakzame tests in werking stelt.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Foutopsporing van het Platform, zie [overzicht van de controlefunctie](./overview.md).

Waarschuwingen tonen problemen waarvan je op de hoogte moet zijn, maar die geen invloed hebben op je score. Dit zijn aanbevelingen voor best practices die in sommige gevallen niet van toepassing zijn op uw implementatie.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Advertising Cloud - Correct geïmplementeerde omzettingstag | 0 | Controleer of de juiste conversietag wordt gebruikt.<br><br>**Waarschuwing**: Het gebruik van verouderde conversietags voor TubeMogul kan gegevensverlies tot gevolg hebben. | Voer een upgrade uit op de conversiepixels naar de nieuwe Advertising Cloud-tags voor conversie van alleen afbeeldingen. Dit kan het gemakkelijkst worden verwezenlijkt met [Advertising Cloud-tagextensie](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - JS-tag corrigeren gebruikt | 0 | Advertising Cloud moet de nieuwste JavaScript-tags gebruiken. | Upgrade uw Advertising Cloud JavaScript naar de nieuwste versie. Als u de verouderde JavaScript-versies gebruikt, kan de functionaliteit verloren gaan. Dit kan gemakkelijker worden verwezenlijkt door het gebruik van [Advertising Cloud-tagextensie](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Tag met alleen afbeelding | 0 | De Advertising Cloud-indeling voor afbeeldingspixels moet overeenkomen met een van de volgende aanbevolen indelingen: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Upgrade uw Advertising Cloud-pixels naar de nieuwe Advertising Cloud-tags voor alleen afbeeldingen, zodat u de volledige Advertising Cloud-functionaliteit kunt benutten. Dit kan het gemakkelijkst worden verwezenlijkt met [Advertising Cloud-tagextensie](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Segmentpixels DSP synchroniseren ingeschakeld | 0 | Controleer of de TubeMogul-segmentpixel een DSP-instelling bevat en adviseer dat de instelling aan de pixel wordt toegevoegd. De instelling DSP synchroniseren wordt bepaald door het gebruik van een parameter voor een queryreeks. Samenvatten: <ul><li>ALS de tag op een van de volgende manieren wordt geactiveerd:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>EN de tag bevat de URL-parameter `sid=`</li><li>Controleer VERVOLGENS of de URL-parameter `cs=0` of `cs=1` bestaat, en als niet adviseert dat `cs=1` worden toegevoegd aan deze pixels, zodat de overeenkomende populatiegraad kan worden verbeterd.</li></ul> | De URL-parameter toevoegen `cs=1` op uw Advertising Cloud-pixels zodat DSP synchroniseren kan plaatsvinden. Hierdoor nemen de overeenkomende populaties toe. Dit kan het gemakkelijkst worden verwezenlijkt met [Advertising Cloud-tagextensie](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID-service - Gebruik slechts één AdobeOrg | 0 | In een normale ECID-implementatie moet één AdobeOrg worden gebruikt. | Controleer of er meerdere AdobeOrg-id&#39;s bestaan voor deze implementatie. <br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Starten - `pageBottom` callback-plaatsing | 0 | De `_satellite.pageBottom()` -functies moeten aanwezig zijn om tags te laten werken. Voeg het inlinescript onmiddellijk vóór het sluiten toe `</body>` -tag voor een correcte DTM-functionaliteit. Opmerking: Het wordt aanbevolen dat de tag de laatste tag in het dialoogvenster `<body>`. Als deze is gevonden in het dialoogvenster `<body>` -tag, heeft de kans om te werken, maar omdat dit niet de beste praktijk is, kan deze onjuist functioneren of onverwachte of ongewenste resultaten opleveren. | Voeg het inlinescript onmiddellijk vóór het sluiten toe `</body>` -tag voor een correcte DTM-functionaliteit. <br><br>[Aanvullende informatie](../../tags/ui/client-side/asynchronous-deployment.md) |
| Starten - Zelfgehost | 0 | De tag wordt gehost op de Akamai-instantie van de Adobe-bibliotheek op `assets.adobedtm.com`. Zelf-ontvangen is de geadviseerde benadering voor ladingmarkeringen omdat het grotere controle van websiteprestaties door geheim voorgeheugencontrole, verminderend derdemanuscriptgebiedsdelen, en grotere controle van het het publiceren proces verleent. Tagbibliotheken kunnen via uw eigen webhosting of CDN worden gehost en beheerd. | Bij het laden van tags op een pagina gaat u naar zelfhosting. Hoewel hosting via de Akamai CDN in de meeste gevallen werkt, verbetert zelforhosting de paginaprestaties. <br><br>Aanvullende informatie:<ul><li>[Gids voor snel opstarten van tags](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Asynchrone implementatie](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Starten - moet asynchroon worden geïmplementeerd | 0 | Tags moeten asynchroon worden geïmplementeerd voor optimale prestaties. | Inclusief de `async` parameter in het inlinescript om juiste markeringsfunctionaliteit te verzekeren <br><br>[Aanvullende informatie](../../tags/ui/client-side/asynchronous-deployment.md) |
| Doel - Inhoud in `mboxDefault` | 0 | Inhoud moet bestaan in `mboxDefault` wanneer u `at.js`. | Controleer of de inhoud beschikbaar is. <br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
