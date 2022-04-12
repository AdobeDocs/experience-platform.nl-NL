---
title: Referentie voor consistentietest van tag
description: Leer hoe de controlefunctie de consistentie van tags test in Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# Referentie voor de consistentietest van de tag

Deze verwijzing verstrekt meer informatie over hoe de controleureigenschap in Foutopsporing van Adobe Experience Platform op markeringsconsistentie test.

>[!NOTE]
>
>Voor meer informatie over controleurstests in Foutopsporing van het Platform, zie [overzicht van de controlefunctie](./overview.md).

Bij het testen van de consistentie van tags wordt gezocht naar inconsistenties op alle gescande pagina&#39;s. Dit zijn waarden of configuraties die voor alle pagina&#39;s op de site hetzelfde moeten zijn om nauwkeurige gegevensverzameling te garanderen.

| Testen | Dikte | Criteria | Aanbeveling |
| --- | --- | --- | --- |
| Adobe Analytics - Consistente codeversie | 5 | Er zijn meerdere versies van de Analytics-code gevonden. | Vervang alle instanties van Analytics door de huidige versie.<br><br>[Aanvullende informatie](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |

{style=&quot;table-layout:auto&quot;}
