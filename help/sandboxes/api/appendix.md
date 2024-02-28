---
keywords: Experience Platform;home;populaire onderwerpen;api;API;sandbox;Sandbox;sandbox;sandboxen;Sandboxen
solution: Experience Platform
title: Bijlage API-naslaggids voor sandbox
description: Dit document bevat aanvullende informatie over het werken met de sandbox-API.
role: Developer
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '122'
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
