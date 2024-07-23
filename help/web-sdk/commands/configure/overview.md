---
title: De SDK van Adobe Experience Platform Web configureren
description: Gebruik vormen bevel om vereiste montages te plaatsen wanneer het gebruiken van het Web SDK.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# De SDK van Adobe Experience Platform Web configureren

De configuratie voor het Web SDK wordt gedaan met het `configure` bevel. Het vormen van SDK van het Web is een essentiële en vereiste stap die moet gebeuren wanneer de bibliotheek of de markeringsuitbreiding wordt gebruikt.

## De SDK van het web configureren met de tagextensie {#configure-tag-extension}

Voer de onderstaande stappen uit om de SDK van het Web te configureren via de tagextensie.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Ga naar de [ pagina van de de de taguitbreiding van SDK van het Web ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) voor gedetailleerde informatie over alle configuratieopties.

Deze configuratiemontages worden geplaatst wanneer u de uitbreiding gebruikt om gegevens naar Adobe te verzenden.

## De SDK van het Web configureren met de JavaScript-bibliotheek {#configure-js}

Voer de opdracht `configure` uit. Dit bevel wordt vereist alvorens u een andere bevelen van SDK van het Web, zoals [`sendEvent`](../sendevent/overview.md) kunt roepen.

De eigenschappen [`datastreamId`](datastreamid.md) en [`orgId`](orgid.md) zijn vereist. Alle andere eigenschappen zijn optioneel, afhankelijk van de implementatievereisten van uw organisatie.

Zie de inhoudsopgave van deze gebruikershandleiding voor gedetailleerde informatie over elk van de ondersteunde opdrachten.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"],
  debugEnabled: true,
  defaultConsent: "pending",
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$",
  edgeBasePath: "ee",
  edgeConfigOverrides: { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  edgeDomain: "data.example.com",
  idMigrationEnabled: false,
  onBeforeEventSend: function(content) {
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
  },
  onBeforeLinkClickSend: function(content) {
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
  },
  prehidingStyle: "#container { opacity: 0 !important }",
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
