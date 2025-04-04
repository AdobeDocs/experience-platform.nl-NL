---
title: Referentie voor configuratietest
description: Leer hoe de controllerfunctie configuraties in Adobe Experience Platform Debugger test.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 1%

---

# Referentie voor configuratietest

Deze verwijzing verstrekt meer informatie over hoe de controleeigenschap in Adobe Experience Platform Debugger configuratietests in werking stelt.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Debugger van Experience Platform, zie het [ overzicht van de controleeigenschap ](./overview.md).

De tests van de configuratie kunnen voor specifieke montages, waarden, of potentiële conflicten in uw implementatie aftasten. Experience Platform Auditor evalueert de tags aan de hand van andere regels en aanbevolen aanbevolen procedures.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Advertising Cloud - Conversienamen gebruiken alleen alfanumerieke tekens | 3 | De parameter `ev_conversion_property_name` mag alleen numerieke en decimale waarden bevatten, behalve voor de parameter `ev_transid` , die tekst of numerieke waarden kan bevatten. Zoek naar `everesttech.net` pixels die een URL-parameter bevatten die begint met `ev_` . | Zorg ervoor dat de parameters van de transactieeigenschap alleen numerieke en decimale waarden bevatten.<br><br> Waarschuwing: Om het even welke andere waardetypes zouden gegevensverlies kunnen veroorzaken. |
| Advertising Cloud - Conversienamen gebruiken URL-veilige tekens | 3 | Namen van conversie-eigenschappen mogen geen en-teken of vraagteken bevatten. | Zorg ervoor dat de parameters van de transactieeigenschap geen niet-gecodeerd en/of vraagteken bevatten. Hiermee wordt de URL-indeling verbroken.<br><br> Waarschuwing: de parameters van het bezit die een niet-gecodeerd ampersand of vraagteken bevatten, (bijvoorbeeld: `ev_formComplete?=1` of `ev_formComplete&Submit=1`), zouden in gegevensverlies kunnen resulteren. |
| Advertising Cloud - Transactie-id correct geïmplementeerd | 1 | De eigenschapsnaam `ev_transid=` mag niet leeg zijn. | De eigenschapsnaam `ev_transid=` mag niet zonder een waarde worden gelaten. Als dit zonder een waarde wordt verlaten, zou er verlies van transactiegegevens kunnen zijn. Wijs een waarde toe aan `ev_transid=` of verwijder de parameter uit de pixel. |
| Analytics - Instantiated in DOM | 5 | De Adobe Analytics-code is niet geïnstalleerd of kan niet worden uitgevoerd. Retourneert 0 wanneer geen analytische code op de webpagina is gevonden. | Controleer of de tag Analytics is geïmplementeerd op de pagina en niet wordt geblokkeerd door daaropvolgende scriptactiviteiten.<br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analyse - eenmaal geïnstantieerd | 5 | De Adobe Analytics-code is meerdere keren gedetecteerd op de pagina. . Retourneert 0 wanneer geen A-analytische code op de webpagina is gevonden. | Zorg ervoor dat er slechts één tag Analytics op de pagina staat.<br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analyse - nieuwste versie | 3 | De meest recente versie van de Codebibliotheek Analytics wordt niet uitgevoerd op uw pagina&#39;s. Codebibliotheken die Experience Cloud-technologieën in staat stellen, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. Retourneert 0 wanneer geen analytische code op de webpagina is gevonden. | Installeer de nieuwste versie van de bibliotheek Analytics.<br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html) |
| Starten - tags van derden worden asynchroon geladen nadat DOM gereed is | 3 | Om een evenwicht tussen een goede gebruikerservaring en het verzamelen van nauwkeurige gegevens te bereiken, zouden de markeringen van derde partijen bij DOM klaar moeten teweegbrengen. Zo zorgt u ervoor dat deze volgende scripts worden uitgevoerd zonder dat dit van invloed is op de functionaliteit van de site. | Los dit probleem op door alle regels aan te passen die derden-pixels uitvoeren om bij DOM Ready te branden.<br><br>[ Aanvullende informatie ](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID Service - Laatste versie | 2 | De meest recente versie van de codeblok van de Bezoeker-id-service, bezoekerAPI.js, wordt niet uitgevoerd op uw pagina&#39;s. Codebibliotheken die Experience Cloud-technologieën in staat stellen, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. | Installeer de nieuwste versie van de bibliotheek met bezoekersidentiteiten.<br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Starten - Laatste versie | 2 | Op deze pagina&#39;s wordt niet de nieuwste versie van de codebibliotheek met tags (Turbine) uitgevoerd. Codebibliotheken die Experience Cloud-technologieën in staat stellen, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. | Maak de tagbibliotheek opnieuw en publiceer deze.<br><br>[ Aanvullende informatie ](../../tags/quick-start/quick-start.md) |
| Doel - Laatste versie | 2 | De meest recente versie van de doelcodebibliotheek wordt niet uitgevoerd op uw pagina&#39;s. Codebibliotheken die Experience Cloud-technologieën in staat stellen, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. | Installeer de nieuwste versie van de doelbibliotheek.<br><br>[ Aanvullende informatie ](https://developer.adobe.com/target/implement/client-side/) |
| Doel - mboxDefault komt eerder dan mboxCreate | 5 | Het juiste gebruik van mboxCreate kijkt gelijkaardig aan dit:<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Zorg ervoor dat u een tag `<div class="mboxDefault"></div>` opneemt voordat u mboxCreate() aanroept. om.js zal geen één voor u toevoegen.<br><br>[ Aanvullende informatie ](https://developer.adobe.com/target/implement/client-side/) |
| Doel: geldig DOCTYPE | 5 | Er is een ongeldig DOCTYPE gedetecteerd. In dit scenario worden geen vakjes geactiveerd.  Voor at.js, moet DOCTYPE op de wijze van Normen zijn of het Doel zal niet werken. | Werk het DOCTYPE op de pagina bij.<br><br>[ Aanvullende informatie ](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
