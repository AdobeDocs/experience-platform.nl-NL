---
title: prehideStyle
description: Maak een CSS-definitie waarmee gepersonaliseerde inhoud zonder flikkeringen kan worden geladen.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

Met de eigenschap `prehidingStyle` kunt u een CSS-kiezer definiëren om gepersonaliseerde inhoud te verbergen totdat deze wordt geladen. Dit bezit is waardevol in synchrone implementaties van SDK van het Web om het flikkeren te vermijden. Adobe adviseert het gebruiken van [&#x200B; prehide fragment &#x200B;](/help/collection/use-cases/personalization/manage-flicker.md) voor asynchrone implementaties van SDK van het Web.

De CSS-kiezers die u in deze eigenschap definieert, beginnen inhoud te verbergen wanneer u de eerste opdracht [`sendEvent`](../sendevent/overview.md) op een pagina uitvoert. De inhoud is niet verborgen wanneer een reactie van Adobe wordt ontvangen, die doorgaans inhoud met een persoonlijk tintje bevat. De inhoud wordt ook niet verborgen als de opdracht `sendEvent` mislukt of als de opdracht een keer wordt uitgevoerd.

Als u zowel `prehidingStyle` als het bovenliggende fragment in uw implementatie opneemt, heeft het bovenliggende fragment voorrang op deze configuratie-eigenschap.

Stel de tekenreeks `prehidingStyle` in wanneer u de opdracht `configure` uitvoert. Wanneer u deze eigenschap weglaat bij het configureren van de Web SDK, wordt niets verborgen wanneer de eerste opdracht `sendEvent` op een pagina wordt uitgevoerd. Stel deze waarde in op de gewenste CSS-kiezer en het declaratieblok voor synchroon geladen bibliotheken.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## Stijl vooraf verbergen met de weblabelextensie SDK

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [&#x200B; de configuratiemontages van Personalization &#x200B;](/help/tags/extensions/client/web-sdk/configure/personalization.md).
