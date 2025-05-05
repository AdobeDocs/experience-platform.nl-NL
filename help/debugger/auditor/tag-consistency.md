---
title: Referentie voor consistentietest van tag
description: Leer hoe de controleur op markeringsconsistentie in Adobe Experience Platform Debugger test.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 1%

---

# Referentie voor de consistentietest van de tag

Deze naslaggids bevat meer informatie over de manier waarop de controlefunctie in Adobe Experience Platform Debugger de consistentie van tags test.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Debugger van Experience Platform, zie het [ overzicht van de controleeigenschap ](./overview.md).

Bij het testen van de consistentie van tags wordt gezocht naar inconsistenties op alle gescande pagina&#39;s. Dit zijn waarden of configuraties die voor alle pagina&#39;s op de site hetzelfde moeten zijn om nauwkeurige gegevensverzameling te garanderen.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Adobe Analytics - Consistente codeversie | 5 | Er zijn meerdere versies van de Analytics-code gevonden. | Vervang alle instanties van Analytics door de huidige versie.<br><br>[ Aanvullende informatie ](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=nl-NL) |

{style="table-layout:auto"}
