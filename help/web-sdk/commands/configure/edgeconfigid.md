---
title: edgeConfigId
description: Bepaal de gegevensstroom-id waarnaar u gegevens wilt verzenden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# `edgeConfigId`

De `edgeConfigId` eigenschap is een tekenreeks die bepaalt welke [datastream](../../../datastreams/overview.md) in Adobe Experience Platform waarnaar u gegevens wilt verzenden. Dit bezit wordt vereist wanneer het verzenden van gegevens naar Adobe.

Een gegevensstroom-id zoeken:

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Gebruik het zoekveld om de gewenste gegevensstroom te zoeken en selecteer **[!UICONTROL Copy]** ![Kopiëren](../../assets/copy.png) naast de gegevensstroom-id.

U kunt ook de gewenste gegevensstroomnaam selecteren en de gegevensstroom-id wordt in de rechterkolom weergegeven, zodat u deze kunt kopiëren.

## Selecteer de gegevensstroom-id met de web SDK-tagextensie

Maak een keuze in een lijst met beschikbare gegevensstromen of voer een gegevensstroom-id rechtstreeks in wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Zoek de [!UICONTROL Datastreams] selecteert u vervolgens de gewenste methode voor het bepalen van de gegevensstroom.
   * Als u een keuze maakt in een lijst, selecteert u de sandbox en de gegevensstroom in elke vervolgkeuzelijst.
   * Voer bij het invoeren van waarden de gewenste gegevensstroom-id in.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

U kunt gegevens naar verschillende gegevensstromen voor productie, het opvoeren, en milieu&#39;s van ontwikkelingsmarkeringen verzenden.

## Selecteer de gegevensstroom-id met de Web SDK JavaScript-bibliotheek

Stel de `edgeConfigId` tekenreekseigenschap wanneer de `configure` gebruiken. Dit bezit wordt vereist voor alle implementaties van SDK van het Web. Als u dit bezit weglaat, weet SDK van het Web niet welke gegevensstroom om gegevens naar te verzenden, veroorzakend dat de gegevens permanent worden verloren.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Als u veelvoudige instanties van het Web SDK op één enkele pagina vormt, moet u een verschillende vormen `edgeConfigId` voor elke instantie.
