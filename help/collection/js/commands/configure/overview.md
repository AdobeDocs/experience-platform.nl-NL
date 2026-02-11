---
title: Adobe Experience Platform Web SDK configureren
description: Gebruik vormen bevel om vereiste montages te plaatsen wanneer het gebruiken van het Web SDK.
exl-id: 05ba98ae-c004-4b7b-b55b-38290ca62cfa
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Adobe Experience Platform Web SDK configureren

De configuratie voor het Web SDK wordt gedaan met het **`configure`** bevel. Deze opdracht is vereist voor elke laadpagina voordat u andere Web SDK-opdrachten aanroept, zoals [`sendEvent`](../sendevent/overview.md) .

**De eigenschappen [`datastreamId`](datastreamid.md) en [`orgId`](orgid.md) zijn vereist.** Alle andere eigenschappen zijn optioneel, afhankelijk van de implementatievereisten van uw organisatie. In het volgende voorbeeld wordt een configuratieobject getoond met de meeste beschikbare eigenschappen:

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
    filterClickDetails: function(content) {
      content.linkUrl = "https://example.com/current.html";
    },
    sessionStorageEnabled: true
  },
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints", "oneTimeAnalyticsReferrer"],
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
  prehidingStyle: "#container { opacity: 0 !important }",
  conversation: {
    stickyConversationSession: false
  },
  targetMigrationEnabled: true,
  thirdPartyCookiesEnabled: false
});
```
