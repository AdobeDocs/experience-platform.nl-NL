---
title: prehideStyle
description: Maak een CSS-definitie waarmee gepersonaliseerde inhoud zonder flikkeringen kan worden geladen.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# `prehidingStyle`

Met de eigenschap `prehidingStyle` kunt u een CSS-kiezer definiëren om gepersonaliseerde inhoud te verbergen totdat deze wordt geladen. Dit bezit is waardevol in synchrone implementaties van SDK van het Web om het flikkeren te vermijden. De Adobe adviseert het gebruiken van [ prehide fragment ](../../personalization/manage-flicker.md) voor asynchrone implementaties van SDK van het Web.

De CSS-kiezers die u in deze eigenschap definieert, beginnen inhoud te verbergen wanneer u de eerste opdracht [`sendEvent`](../sendevent/overview.md) op een pagina uitvoert. De inhoud is niet verborgen wanneer een reactie van de Adobe wordt ontvangen, die doorgaans gepersonaliseerde inhoud bevat. De inhoud wordt ook niet verborgen als de opdracht `sendEvent` mislukt of als de opdracht een keer wordt uitgevoerd.

Als u zowel `prehidingStyle` als het bovenliggende fragment in uw implementatie opneemt, heeft het bovenliggende fragment voorrang op deze configuratie-eigenschap.

## Stijl vooraf verbergen met de webSDK-tagextensie

Selecteer de **[!UICONTROL Provide prehiding style]** knoop wanneer [ het vormen van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Blader omlaag naar de sectie [!UICONTROL Personalization] en selecteer vervolgens de knop **[!UICONTROL Provide prehiding style]** .
1. Met deze knop opent u een modaal venster met een CSS-editor. Voeg de gewenste CSS-kiezer en het declaratieblok in en klik vervolgens op **[!UICONTROL Save]** om het modale venster te sluiten.
1. Klik op **[!UICONTROL Save]** onder extensie-instellingen en publiceer uw wijzigingen.

## Stijl vooraf verbergen met de Web SDK JavaScript-bibliotheek

Stel de tekenreeks `prehidingStyle` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt niets verborgen wanneer de eerste `sendEvent` -opdracht op een pagina wordt uitgevoerd. Stel deze waarde in op de gewenste CSS-kiezer en het declaratieblok voor synchroon geladen bibliotheken.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```
