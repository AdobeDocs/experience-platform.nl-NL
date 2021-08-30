---
keywords: Experience Platform;home;populaire onderwerpen;api;API;sandbox;Sandbox;sandbox;sandboxen;Sandboxen
solution: Experience Platform
title: Bijlage sandbox API-handleiding
description: Dit document bevat aanvullende informatie over het werken met de sandbox-API.
topic-legacy: developer guide
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# Handboek sandbox-API

Dit document bevat aanvullende informatie over het werken met de [!DNL Sandbox]-API.

## Query-parameters gebruiken {#query}

De [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) steunt het gebruik van vraagparameters aan pagina en filterresultaten wanneer het van een lijst maken van zandbakken.

>[!NOTE]
>
>De `limit` en `offset` vraagparameters moeten samen worden gespecificeerd. Als u slechts één specificeert, zal API een fout terugkeren. Als u geen opgeeft, is de standaardlimiet 50 en is de verschuiving 0.

| Parameter | Beschrijving |
| --- | --- |
| `limit` | Het maximumaantal records dat in de reactie moet worden geretourneerd. |
| `offset` | Het aantal entiteiten van de eerste record waaruit de lijst met reacties moet worden gestart (verschuiving). |
