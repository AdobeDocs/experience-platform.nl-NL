---
title: datastreamId
description: Bepaal de gegevensstroom-id waarnaar u gegevens wilt verzenden.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# `datastreamId`

Het `datastreamId` bezit is een koord dat bepaalt welke [ datastream ](../../../datastreams/overview.md) in Adobe Experience Platform u gegevens naar wilt verzenden. Dit bezit wordt vereist wanneer het verzenden van gegevens naar Adobe. Web SDK-versies 2.20.0 of eerder gebruiken `edgeConfigId` .

Een gegevensstroom-id zoeken:

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Gebruik het onderzoeksgebied om van de gewenste gegevensstroom de plaats te bepalen, dan selecteren **[!UICONTROL Copy]** ![ Exemplaar ](../../assets/copy.png) naast gegevensstroom identiteitskaart

U kunt ook de gewenste gegevensstroomnaam selecteren en de gegevensstroom-id verschijnt in de rechterkolom voor kopiëren.

## Selecteer de gegevensstroom-id met de web SDK-tagextensie

Kies van een lijst van beschikbare gegevensstromen, of ga direct een gegevensstroomidentiteitskaart in wanneer [ vormend de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Zoek de sectie [!UICONTROL Datastreams] en selecteer vervolgens de gewenste methode voor het bepalen van de gegevensstroom.
   * Als u een keuze maakt in een lijst, selecteert u de sandbox en de gegevensstroom in elke vervolgkeuzelijst.
   * Voer bij het invoeren van waarden de gewenste gegevensstroom-id in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

U kunt gegevens naar verschillende gegevensstromen voor productie, het opvoeren, en milieu&#39;s van ontwikkelingsmarkeringen verzenden.

## Selecteer de gegevensstroom-id met de Web SDK JavaScript-bibliotheek

Stel de eigenschap `datastreamID` string in wanneer u de opdracht `configure` uitvoert. Dit bezit wordt vereist voor alle implementaties van SDK van het Web. Als u dit bezit weglaat, weet SDK van het Web niet welke gegevensstroom om gegevens naar te verzenden, veroorzakend dat de gegevens permanent worden verloren.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Als u veelvoudige instanties van het Web SDK op één enkele pagina vormt, moet u verschillende `datastreamId` voor elke instantie vormen.
