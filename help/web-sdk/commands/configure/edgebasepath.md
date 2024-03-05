---
title: edgeBasePath
description: Het basispad van het eindpunt dat wordt gebruikt voor interactie met Adobe-services.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 1%

---

# `edgeBasePath`

De `edgeBasePath` Deze eigenschap wijzigt het doelpad wanneer u werkt met Adobe-services. De meeste organisaties hoeven deze eigenschap niet in te stellen of te wijzigen.

## Edge-basispad met de webSDK-tagextensie

Voer de gewenste tekst in het dialoogvenster **[!UICONTROL Edge base path]** tekstveld wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Advanced Settings] en voert u vervolgens de gewenste waarde in in het dialoogvenster **[!UICONTROL Edge base path]** tekstveld.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Edge-basispad met de Web SDK JavaScript-bibliotheek

Stel de `edgeBasePath` tekstveld wanneer het `configure` gebruiken. Als u deze eigenschap weglaat, wordt standaard de waarde van `ee`. Adobe raadt aan deze eigenschap uit de meeste configuraties weg te laten.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "edgeBasePath": "ee"
});
```
