---
title: De SDK van Adobe Experience Platform Web configureren
description: Gebruik vormen bevel om vereiste montages te plaatsen wanneer het gebruiken van het Web SDK.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# De SDK van Adobe Experience Platform Web configureren

De configuratie voor Web SDK wordt gedaan met `configure` gebruiken. Het vormen van SDK van het Web is een essentiële en vereiste stap die moet gebeuren wanneer de bibliotheek of de markeringsuitbreiding wordt gebruikt.

## Configuratie-instellingen die de Web SDK-tagextensie gebruiken

Ga naar de [configuratiepagina voor extensie van tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.

Deze configuratiemontages worden geplaatst wanneer u de uitbreiding gebruikt om gegevens naar Adobe te verzenden.

## Configuratie-instellingen met de Web SDK JavaScript-bibliotheek

Voer de `configure` gebruiken. Dit bevel wordt vereist alvorens u een andere bevelen van SDK van het Web kunt roepen, zoals [`sendEvent`](../sendevent/overview.md). De eigenschappen [`edgeConfigId`](edgeconfigid.md) en [`orgId`](orgid.md) zijn vereist. Alle andere eigenschappen zijn optioneel, afhankelijk van de implementatievereisten van uw organisatie.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false,
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  "debugEnabled": true,
  "defaultConsent": "pending",
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  "edgeBasePath": "ee",
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "edgeDomain": "data.example.com",
  "idMigrationEnabled": false,
  "onBeforeEventSend": function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  "onBeforeLinkClickSend": function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  "prehidingStyle": "#container { opacity: 0 !important }",
  "targetMigrationEnabled": true,
  "thirdPartyCookiesEnabled": false
});
```
