---
keywords: Experience Platform;home;populaire onderwerpen;api;API;sandbox;Sandbox;sandbox;sandboxen;Sandboxen
solution: Experience Platform
title: Bijlage sandbox API-handleiding
description: Dit document bevat aanvullende informatie over het werken met de sandbox-API.
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Handboek sandbox-API

Dit document bevat aanvullende informatie over het werken met de [!DNL Sandbox] API.

## Query-parameters gebruiken {#query}

De [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) ondersteunt het gebruik van queryparameters voor pagina- en filterresultaten bij het weergeven van sandboxen.

>[!NOTE]
>
>De `limit` en `offset` queryparameters moeten samen worden opgegeven. Als u slechts één specificeert, zal API een fout terugkeren. Als u geen opgeeft, is de standaardlimiet 50 en is de verschuiving 0.

| Parameter | Beschrijving |
| --- | --- |
| `limit` | Het maximumaantal records dat in de reactie moet worden geretourneerd. |
| `offset` | Het aantal entiteiten van de eerste record waaruit de lijst met reacties moet worden gestart (verschuiving). |
