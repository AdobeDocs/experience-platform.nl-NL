---
title: gesprek
description: Chatinstellingen voor Brand Concierge configureren.
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 2%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge voor het Web SDK is momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

Het `conversation` -object bevat configuratieopties voor Brand Concierge-chatsessies. Dit object wordt ondersteund in SDK 2.31.0 of hoger op het web.

## Properties

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| **`collectSources`** | `boolean` | Determines if the Web SDK reads the `adobe_brand_concierge_source` query string parameter and include it in `xdm.channel.referringSource` . Wordt standaard ingesteld op `false` . |
| **`stickyConversationSession`** | `boolean` | Hiermee wordt bepaald of de Web SDK een sessiecookie instelt om Brand Concierge-chatsessies te behouden bij het laden van pagina&#39;s. Wordt standaard ingesteld op `false` . Als u deze waarde weglaat of instelt op `false` , wordt bij elke laadpagina een nieuwe sessie gestart tijdens een chat met Brand Concierge. |

## Voorbeeld

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## gespreksinstellingen configureren met de webtagextensie SDK

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ montages van Brand Concierge ](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
