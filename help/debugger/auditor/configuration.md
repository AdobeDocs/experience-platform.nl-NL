---
title: Referentie voor configuratietest
description: Leer hoe de controlefunctie configuraties in Adobe Experience Platform Debugger test.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 797d4f305b4a6884ada4e0619beadff6a45ab42d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 4%

---

# Referentie voor configuratietest

Deze verwijzing verstrekt meer informatie over hoe de controleeigenschap in Debugger van Adobe Experience Platform configuratietests in werking stelt.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Foutopsporing van het Platform, zie [overzicht van de controlefunctie](./overview.md).

De tests van de configuratie kunnen voor specifieke montages, waarden, of potentiële conflicten in uw implementatie aftasten. De Auditor van het Platform evalueert de markeringen tegen andere regels en geadviseerde beste praktijken.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Advertising Cloud - Conversienamen gebruiken alleen alfanumerieke tekens | 3 | De `ev_conversion_property_name` parameter mag alleen numerieke en decimale waarden bevatten, BEHALVE voor de `ev_transid` parameter, die tekst of numerieke waarden kan bevatten. Zoeken naar `everesttech.net` pixels met een URL-parameter die begint met  `ev_`. | Zorg ervoor dat de parameters van de transactieeigenschap alleen numerieke en decimale waarden bevatten.<br><br>Waarschuwing: Andere waardetypen kunnen gegevensverlies veroorzaken. |
| Advertising Cloud - Conversienamen gebruiken URL-veilige tekens | 3 | Namen van conversie-eigenschappen mogen geen en-teken of vraagteken bevatten. | Zorg ervoor dat de parameters van de transactieeigenschap geen niet-gecodeerd en/of vraagteken bevatten. Hiermee wordt de URL-indeling verbroken.<br><br>Waarschuwing: Eigenschapparameters die een niet-gecodeerd en/of vraagteken bevatten, (bijvoorbeeld:  `ev_formComplete?=1` of  `ev_formComplete&Submit=1`), kan leiden tot gegevensverlies. |
| Advertising Cloud - Transactie-ID correct geïmplementeerd | 1 | De eigenschapsnaam  `ev_transid=` mag niet leeg zijn. | De eigenschapsnaam  `ev_transid=` mag niet zonder waarde worden gelaten. Als dit zonder een waarde wordt verlaten, zou er verlies van transactiegegevens kunnen zijn. Een waarde toewijzen aan `ev_transid=` of verwijder de parameter uit de pixel. |
| Analytics - Instantiated in DOM | 5 | De Adobe Analytics-code is niet geïnstalleerd of kan niet worden uitgevoerd. Retourneert 0 wanneer geen analytische code op de webpagina is gevonden. | Controleer of de tag Analytics is geïmplementeerd op de pagina en niet wordt geblokkeerd door daaropvolgende scriptactiviteiten.<br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analyse - eenmaal geïnstantieerd | 5 | De Adobe Analytics-code is meerdere keren gedetecteerd op de pagina. . Retourneert 0 wanneer geen A-analytische code op de webpagina is gevonden. | Zorg ervoor dat er slechts één tag Analytics op de pagina staat.<br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analyse - nieuwste versie | 3 | De meest recente versie van de Codebibliotheek Analytics wordt niet uitgevoerd op uw pagina&#39;s. Codebibliotheken die Experience Cloud-technologieën van stroom voorzien, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. Retourneert 0 wanneer geen analytische code op de webpagina is gevonden. | Installeer de nieuwste versie van de bibliotheek Analytics.<br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html) |
| Starten - tags van derden worden asynchroon geladen nadat DOM gereed is | 3 | Om een evenwicht tussen een goede gebruikerservaring en het verzamelen van nauwkeurige gegevens te bereiken, zouden de markeringen van derde partijen bij DOM klaar moeten teweegbrengen. Zo zorgt u ervoor dat deze volgende scripts worden uitgevoerd zonder dat dit van invloed is op de functionaliteit van de site. | Los dit probleem op door alle regels aan te passen die derden-pixels uitvoeren om bij DOM Ready te branden.<br><br>[Aanvullende informatie](../../tags/ui/managing-resources/rules.md) |
| Experience Cloud ID-service - Laatste versie | 2 | De meest recente versie van de codeblok van de Bezoeker-id-service, bezoekerAPI.js, wordt niet uitgevoerd op uw pagina&#39;s. Codebibliotheken die Experience Cloud-technologieën van stroom voorzien, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. | Installeer de nieuwste versie van de bibliotheek met bezoekersidentiteiten.<br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Starten - Laatste versie | 2 | Op deze pagina&#39;s wordt niet de nieuwste versie van de codebibliotheek met tags (Turbine) uitgevoerd. Codebibliotheken die Experience Cloud-technologieën van stroom voorzien, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. | Maak de tagbibliotheek opnieuw en publiceer deze.<br><br>[Aanvullende informatie](../../tags/quick-start/quick-start.md) |
| Doel - Laatste versie | 2 | De meest recente versie van de doelcodebibliotheek wordt niet uitgevoerd op uw pagina&#39;s. Codebibliotheken die Experience Cloud-technologieën van stroom voorzien, worden voortdurend bijgewerkt en getweend om te profiteren van prestatieverbeteringen en de nieuwste functies te bieden. | Installeer de nieuwste versie van de doelbibliotheek.<br><br>[Aanvullende informatie](https://developer.adobe.com/target/implement/client-side/) |
| Doel - mboxDefault komt eerder dan mboxCreate | 5 | Het juiste gebruik van mboxCreate ziet er als volgt uit:<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Zorg ervoor dat u een  `<div class="mboxDefault"></div>` tag voordat mboxCreate() wordt aangeroepen. om.js zal geen één voor u toevoegen.<br><br>[Aanvullende informatie](https://developer.adobe.com/target/implement/client-side/) |
| Doel: geldig DOCTYPE | 5 | Er is een ongeldig DOCTYPE gedetecteerd. In dit scenario worden geen vakjes geactiveerd.  Voor at.js, moet DOCTYPE op de wijze van Normen zijn of het Doel zal niet werken. | Werk het DOCTYPE op de pagina bij.<br><br>[Aanvullende informatie](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style=&quot;table-layout:auto&quot;}
