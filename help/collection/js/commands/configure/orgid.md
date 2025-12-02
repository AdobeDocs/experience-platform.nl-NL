---
title: orgId
description: De eigenschap orgId is een tekenreeks die Adobe vertelt naar welke organisatie de gegevens worden verzonden.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

De eigenschap `orgId` is een tekenreeks die Adobe vertelt naar welke organisatie de gegevens worden verzonden. **Dit bezit wordt vereist voor alle gegevens die het Web SDK worden verzonden.**

Ga als volgt te werk om de `orgID` te zoeken:

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Druk op **`[Ctrl]`** + **`[I]`** op een willekeurige plaats in de Adobe Experience Cloud. Er wordt een [!UICONTROL User Data Debugger] -venster geopend.
1. Klik **[!UICONTROL Copy]** ![ Exemplaar ](../../assets/copy.png) naast [!UICONTROL Current Org ID], of klik het **[!UICONTROL Assigned Orgs]** lusje om andere org IDs te zien die u kunt toegang hebben.
1. Klik op **[!UICONTROL Close]** wanneer u de gewenste gegevens hebt gevonden.

Org-id&#39;s zijn altijd alfanumerieke tekenreeksen van 24 tekens en eindigen altijd in `@AdobeOrg` .

Stel de tekenreeks `orgId` in wanneer u de opdracht `configure` uitvoert. Als u dit bezit weglaat wanneer het vormen van het Web SDK, werpt het Web SDK een consolefout en de gegevens worden niet verzonden naar Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## De organisatie-id instellen met de Web SDK-tagextensie

Dit plaatsen kan in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ de montages van de instantieconfiguratie van SDK ](/help/tags/extensions/client/web-sdk/configure/general.md). Het veld wordt automatisch ingevuld op basis van de organisatie waarin de eigenschap tag is gemaakt.
