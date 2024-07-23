---
title: targetMigrationEnabled
description: De Web SDK toestaan Adobe Target cookies te lezen en te schrijven.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# `targetMigrationEnabled`

De eigenschap `targetMigrationEnabled` is een Booleaanse waarde waarmee de Web SDK de cookies mbox en mboxEdgeCluster die de Adobe Target 1.x- en 2.x-bibliotheken gebruiken, kan lezen en schrijven. Met deze optie kunt u het bezoekersprofiel tussen pagina&#39;s behouden met behulp van eerdere Adobe Target-implementaties en pagina&#39;s met behulp van de Web SDK.

## Doelmigratie vanuit at.js inschakelen met de Web SDK-tagextensie

Selecteer **[!UICONTROL Migrate Target from at.js to the Web SDK]** checkbox wanneer [ het vormen van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie [!UICONTROL Personalization] en schakel vervolgens het selectievakje **[!UICONTROL Migrate Target from at.js to the Web SDK]** in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Doelmigratie vanuit at.js inschakelen met de Web SDK JavaScript-bibliotheek

Stel de Booleaanse waarde `targetMigrationEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `false` gebruikt. Stel deze waarde in op `true` als u sommige pagina&#39;s hebt die nog steeds de Adobe Target 1.x- of 2.x-bibliotheken gebruiken.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```
