---
title: targetMigrationEnabled
description: De Web SDK toestaan Adobe Target cookies te lezen en te schrijven.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# `targetMigrationEnabled`

De `targetMigrationEnabled` eigenschap is een Booleaanse waarde waarmee de Web SDK de cookies mbox en mboxEdgeCluster die de Adobe Target 1.x- en 2.x-bibliotheken gebruiken, kan lezen en schrijven. Met deze optie kunt u het bezoekersprofiel tussen pagina&#39;s behouden met behulp van eerdere Adobe Target-implementaties en pagina&#39;s met behulp van de Web SDK.

## Doelmigratie vanuit at.js inschakelen met de Web SDK-tagextensie

Selecteer de **[!UICONTROL Migrate Target from at.js to the Web SDK]** selectievakje wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Personalization] en selecteert u vervolgens het selectievakje **[!UICONTROL Migrate Target from at.js to the Web SDK]**.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Doelmigratie vanuit at.js inschakelen met de Web SDK JavaScript-bibliotheek

Stel de `targetMigrationEnabled` boolean wanneer de `configure` gebruiken. Als u dit bezit weglaat wanneer het vormen van het Web SDK, blijft het in gebreke aan `false`. Deze waarde instellen op `true` als u sommige pagina&#39;s hebt die nog steeds de Adobe Target 1.x- of 2.x-bibliotheken gebruiken.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
