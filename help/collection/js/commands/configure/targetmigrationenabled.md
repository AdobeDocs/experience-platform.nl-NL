---
title: targetMigrationEnabled
description: Laat de Web SDK Adobe Target cookies lezen en schrijven.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 051374def898d3797711525c5343e0a8454970a2
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# `targetMigrationEnabled`

De eigenschap `targetMigrationEnabled` is een Booleaanse waarde waarmee de Web SDK de cookies [`mbox` en `mboxEdgeCluster` ](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) die de Adobe Target 1.x- en 2.x-bibliotheken gebruiken, kan lezen en schrijven. Met deze optie kunt u het bezoekersprofiel tussen pagina&#39;s behouden met behulp van eerdere Adobe Target-implementaties en pagina&#39;s met behulp van de Web SDK.

Stel de Booleaanse waarde `targetMigrationEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `false` gebruikt. Stel deze waarde in op `true` als u sommige pagina&#39;s hebt die nog steeds de Adobe Target 1.x- of 2.x-bibliotheken gebruiken.

Wanneer u deze eigenschap gebruikt, moet u [`overrideMboxEdgeServer` ](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) in `targetGlobalSettings()` ook inschakelen in de Adobe Target-implementatie.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```

## Doelmigratie inschakelen met de Web SDK-tagextensie

Dit plaatsen kan in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ de configuratiemontages van Personalization ](/help/tags/extensions/client/web-sdk/configure/personalization.md#migrate-target-from-atjs-to-the-web-sdk).
