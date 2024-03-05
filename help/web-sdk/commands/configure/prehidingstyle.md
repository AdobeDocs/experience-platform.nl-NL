---
title: prehideStyle
description: Maak een CSS-definitie waarmee gepersonaliseerde inhoud zonder flikkeringen kan worden geladen.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# `prehidingStyle`

De `prehidingStyle` kunt u een CSS-kiezer definiëren om gepersonaliseerde inhoud te verbergen totdat deze wordt geladen. Dit bezit is waardevol in synchrone implementaties van SDK van het Web om het flikkeren te vermijden. Adobe raadt u aan de [fragment vooraf verbergen](../../personalization/manage-flicker.md) voor asynchrone implementaties van SDK van het Web.

De CSS-kiezers die u in deze eigenschap definieert, beginnen de inhoud te verbergen wanneer u de eerste [`sendEvent`](../sendevent/overview.md) op een pagina. De inhoud is niet verborgen wanneer een reactie van de Adobe wordt ontvangen, die doorgaans gepersonaliseerde inhoud bevat. De inhoud is ook niet verborgen als de `sendEvent` mislukt of time-out.

Als u beide `prehidingStyle` en het bovenliggende codefragment in uw implementatie, heeft het bovenliggende codefragment voorrang op deze configuratie-eigenschap.

## Stijl vooraf verbergen met de webSDK-tagextensie

Selecteer de **[!UICONTROL Provide prehiding style]** knop wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Personalization] en selecteert u vervolgens de knop **[!UICONTROL Provide prehiding style]**.
1. Met deze knop opent u een modaal venster met een CSS-editor. Voeg de gewenste CSS-kiezer en het declaratieblok in en klik vervolgens op **[!UICONTROL Save]** om het modale venster te sluiten.
1. Klikken **[!UICONTROL Save]** publiceert u de wijzigingen onder extensie-instellingen.

## Stijl vooraf verbergen met de Web SDK JavaScript-bibliotheek

Stel de `prehidingStyle` tekenreeks bij het uitvoeren van de `configure` gebruiken. Als u dit bezit weglaat wanneer het vormen van het Web SDK, is niets verborgen wanneer het runnen van eerste `sendEvent` op een pagina. Stel deze waarde in op de gewenste CSS-kiezer en het declaratieblok voor synchroon geladen bibliotheken.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
