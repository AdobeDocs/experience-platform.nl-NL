---
title: edgeBasePath
description: Het basispad van het eindpunt dat wordt gebruikt voor interactie met Adobe-services.
exl-id: 3542575d-ad02-415c-8e47-97c877dfdd9d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 1%

---

# `edgeBasePath`

De eigenschap `edgeBasePath` wijzigt het doelpad wanneer u werkt met Adobe-services. De meeste organisaties hoeven deze eigenschap niet in te stellen of te wijzigen.

## Edge-basispad met de Web SDK-tagextensie

Ga de gewenste tekst op het **[!UICONTROL Edge base path]** tekstgebied in wanneer [ vormend de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Blader omlaag naar de sectie [!UICONTROL Advanced Settings] en voer in het tekstveld **[!UICONTROL Edge base path]** de gewenste waarde in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Edge-basispad met de Web SDK JavaScript-bibliotheek

Stel het tekstveld `edgeBasePath` in wanneer u de opdracht `configure` uitvoert. Wanneer u deze eigenschap weglaat, krijgt deze standaard de waarde `ee` . Adobe raadt aan deze eigenschap uit de meeste configuraties weg te laten.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeBasePath: "ee"
});
```
