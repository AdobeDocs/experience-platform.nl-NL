---
title: orgId
description: De eigenschap orgId is een tekenreeks die de Adobe vertelt naar welke organisatie de gegevens worden verzonden.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---

# `orgId`

De eigenschap `orgId` is een tekenreeks die de Adobe opgeeft naar welke organisatie de gegevens worden verzonden. **Dit bezit wordt vereist voor alle gegevens die gebruikend SDK van het Web worden verzonden.**

Ga als volgt te werk om de `orgID` te zoeken:

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Druk op **`[Ctrl]`** + **`[I]`** op een willekeurige plaats in de Adobe Experience Cloud. Er wordt een [!UICONTROL User Data Debugger] -venster geopend.
1. Klik **[!UICONTROL Copy]** ![ Exemplaar ](../../assets/copy.png) naast [!UICONTROL Current Org ID], of klik het **[!UICONTROL Assigned Orgs]** lusje om andere org IDs te zien die u kunt toegang hebben.
1. Klik op **[!UICONTROL Close]** wanneer u de gewenste gegevens hebt gevonden.

Org-id&#39;s zijn altijd alfanumerieke tekenreeksen van 24 tekens en eindigen altijd in `@AdobeOrg` .

## Een `orgID` configureren met de extensie van de Web SDK-tag

Ga org identiteitskaart op het **[!UICONTROL IMS organization ID]** tekstgebied in wanneer [ vormend de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Voer de gewenste org-id in het tekstveld [!UICONTROL IMS organization ID] boven in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Een `orgID` configureren met de Web SDK JavaScript-bibliotheek

Stel de tekenreeks `orgId` in wanneer u de opdracht `configure` uitvoert. Als u dit bezit weglaat wanneer het vormen van het Web SDK, werpt SDK van het Web een consolefout en het gegeven wordt niet verzonden naar Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
