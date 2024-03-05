---
title: orgId
description: De eigenschap orgId is een tekenreeks die de Adobe vertelt naar welke organisatie de gegevens worden verzonden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# `orgId`

De `orgId` eigenschap is een tekenreeks die de Adobe vertelt naar welke organisatie de gegevens worden verzonden. **Dit bezit wordt vereist voor alle gegevens die gebruikend SDK van het Web worden verzonden.**

Als u uw `orgID`:

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Druk op **`[Ctrl]`** + **`[I]`**. A [!UICONTROL User Data Debugger] wordt geopend.
1. Klikken **[!UICONTROL Copy]** ![Kopiëren](../../assets/copy.png) naast de [!UICONTROL Current Org ID]of klik op de knop **[!UICONTROL Assigned Orgs]** om andere org-id&#39;s weer te geven die u kunt openen.
1. Wanneer u klaar bent met het zoeken naar de gewenste gegevens, klikt u op **[!UICONTROL Close]**.

Org-id&#39;s zijn altijd alfanumerieke tekenreeksen van 24 tekens en eindigen altijd in `@AdobeOrg`.

## Een `orgID` het gebruiken van de de markeringsuitbreiding van SDK van het Web

Voer de org-id in het dialoogvenster **[!UICONTROL IMS organization ID]** tekstveld wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Voer de gewenste org-id in de [!UICONTROL IMS organization ID] tekstveld boven.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Een `orgID` de Web SDK JavaScript-bibliotheek gebruiken

Stel de `orgId` tekenreeks bij het uitvoeren van de `configure` gebruiken. Als u dit bezit weglaat wanneer het vormen van het Web SDK, werpt SDK van het Web een consolefout en het gegeven wordt niet verzonden naar Adobe.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
