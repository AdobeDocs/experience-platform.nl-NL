---
title: gesprek
description: Chatinstellingen voor Brand Concierge configureren.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '111'
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
| **`stickyConversationSession`** | `boolean` | Hiermee wordt bepaald of de Web SDK een sessiecookie instelt om Brand Concierge-chatsessies te behouden bij het laden van pagina&#39;s. Wordt standaard ingesteld op `false` . Als u deze waarde weglaat of instelt op `false` , wordt bij elke laadpagina een nieuwe sessie gestart tijdens een chat met Brand Concierge. |

## Voorbeeld

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    stickyConversationSession: true
  }
});
```

## gespreksinstellingen configureren met de webtagextensie SDK

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ montages van Brand Concierge ](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
