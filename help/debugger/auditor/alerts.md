---
title: Referentie alarmtest
description: Leer hoe de controlefunctie in Adobe Experience Platform Debugger waarschuwingen test.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# Referentie alarmtest

Deze verwijzing verstrekt meer informatie over hoe de controleureigenschap in Adobe Experience Platform Debugger waakzame tests in werking stelt.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Debugger van Experience Platform, zie het [ overzicht van de controleeigenschap ](./overview.md).

Waarschuwingen tonen problemen waarvan je op de hoogte moet zijn, maar die geen invloed hebben op je score. Dit zijn aanbevelingen voor best practices die in sommige gevallen niet van toepassing zijn op uw implementatie.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Cloud voor advertenties - Geïmporteerde conversietag corrigeren | 0 | Controleer of de juiste conversietag wordt gebruikt.<br><br>**Waarschuwing**: Het gebruiken van de verouderde Tags van de Omzetting TubeMogul kan in gegevensverlies resulteren. | Voer een upgrade uit op de conversiepixels naar de nieuwe conversietags voor afbeeldingen in de cloud voor advertenties. Dit kan het gemakkelijkst met de [ Advertising de markeringsuitbreiding van de Wolk ](../../destinations/catalog/advertising/adobe-advertising-cloud.md) worden verwezenlijkt. |
| Advertising Cloud - JS-tag corrigeren gebruikt | 0 | De nieuwste JavaScript-tags moeten worden gebruikt voor de advertentiekolk. | Upgrade uw advertentie voor Cloud JavaScript naar de nieuwste versie. Het gebruik van verouderde JavaScript-versies kan resulteren in verloren functionaliteit. Dit kan gemakkelijker door het gebruik van de [ Advertising de markeringsuitbreiding van de Wolk ](../../destinations/catalog/advertising/adobe-advertising-cloud.md) worden verwezenlijkt. |
| Cloud voor advertenties - tag Alleen afbeelding | 0 | De pixelindeling voor Advertising Cloud moet overeenkomen met een van de volgende aanbevolen indelingen: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Upgrade uw Cloud-advertentiepixels naar de nieuwe Cloud-afbeeldingstags voor Advertising, zodat u de volledige functionaliteit voor Advertising Cloud kunt gebruiken. Dit kan het gemakkelijkst met de [ Advertising de markeringsuitbreiding van de Wolk ](../../destinations/catalog/advertising/adobe-advertising-cloud.md) worden verwezenlijkt. |
| Cloud voor adverteren - Segmentpixels DSP synchroniseren ingeschakeld | 0 | Controleer of de TubeMogul-segmentpixel een instelling voor DSP Syncing bevat en adviseer dat de instelling aan de pixel wordt toegevoegd. De instelling DSP Syncing wordt bepaald door het gebruik van een parameter voor een queryreeks. Samenvatten: <ul><li>ALS de tag op een van de volgende manieren wordt geactiveerd:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>EN de tag bevat de URL-parameter `sid=`</li><li>Controleer vervolgens of de URL-parameter `cs=0` of `cs=1` bestaat en geef de aanbeveling `cs=1` aan deze pixels toe te voegen zodat de overeenkomende frequenties van de doelgroep beter worden.</li></ul> | Voeg de URL-parameter `cs=1` toe aan uw Cloud-advertentiepixels, zodat er DSP-synchronisatie kan plaatsvinden. Hierdoor nemen de overeenkomende populaties toe. Dit kan het gemakkelijkst met de [ Advertising de markeringsuitbreiding van de Wolk ](../../destinations/catalog/advertising/adobe-advertising-cloud.md) worden verwezenlijkt. |
| Experience Cloud ID Service - slechts één AdobeOrg gebruiken | 0 | In een normale ECID-implementatie moet één AdobeOrg-toepassing worden gebruikt. | Controleer of er meerdere AdobeOrg-id&#39;s bestaan voor deze implementatie. <br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html?lang=nl-NL) |
| Starten - `pageBottom` callback-plaatsing | 0 | Tags werken alleen als de functie `_satellite.pageBottom()` aanwezig is. Voeg het inlinescript direct vóór de afsluitende tag `</body>` toe voor de juiste DTM-functionaliteit. Opmerking: het wordt aanbevolen dat de tag de laatste tag in de `<body>` is. Als het binnen de tag `<body>` wordt gevonden, heeft het een kans om te werken, maar omdat het niet de beste praktijk is, kan het onjuist functioneren of met onverwachte of ongewenste resultaten. | Voeg het inlinescript direct vóór de afsluitende tag `</body>` toe voor de juiste DTM-functionaliteit. <br><br>[ Aanvullende informatie ](../../tags/ui/client-side/asynchronous-deployment.md) |
| Starten - Zelf-gehost | 0 | De tagbibliotheek wordt gehost op de Akamai-instantie van Adobe op `assets.adobedtm.com` . Zelf-ontvangen is de geadviseerde benadering voor ladingmarkeringen omdat het grotere controle van websiteprestaties door geheim voorgeheugencontrole, verminderend derdemanuscriptgebiedsdelen, en grotere controle van het het publiceren proces verleent. Tagbibliotheken kunnen via uw eigen webhosting of CDN worden gehost en beheerd. | Bij het laden van tags op een pagina gaat u naar zelfhosting. Hoewel hosting via de Akamai CDN in de meeste gevallen werkt, verbetert zelforhosting de paginaprestaties. <br><br> Aanvullende informatie:<ul><li>[ Gids van het Snelle begin van Markeringen ](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[ Asynchrone plaatsing ](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Starten - moet asynchroon worden geïmplementeerd | 0 | Tags moeten asynchroon worden geïmplementeerd voor optimale prestaties. | Omvat de `async` parameter in het gealigneerde manuscript om juiste markeringsfunctionaliteit te verzekeren <br><br>[ Aanvullende informatie ](../../tags/ui/client-side/asynchronous-deployment.md) |
| Doel - Inhoud in `mboxDefault` | 0 | Inhoud moet bestaan in `mboxDefault` wanneer u `at.js` gebruikt. | Controleer of de inhoud beschikbaar is. <br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=nl-NL) |

{style="table-layout:auto"}
