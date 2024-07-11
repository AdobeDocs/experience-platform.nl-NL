---
title: clickCollection
description: Stel de instellingen van de klikverzameling nauwkeurig in.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# `clickCollection`

De `clickCollection` Het object bevat verschillende variabelen waarmee u de automatisch verzamelde koppelingsgegevens kunt beheren. Gebruik deze variabelen als u typen koppelingen wilt opnemen in of uitsluiten van gegevensverzameling.

Hiervoor is [`clickCollectionEnabled`](clickcollectionenabled.md) in.

Deze functie wordt ondersteund op Web SDK 2.25.0 of hoger.

De volgende variabelen zijn beschikbaar in de `clickCollection` object:

* **`clickCollection.internalLinkEnabled`**: Een Booleaanse waarde die bepaalt of koppelingen binnen het huidige domein automatisch worden bijgehouden. Bijvoorbeeld: `https://example.com/index.html` tot `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: Een Booleaanse waarde die bepaalt of de bibliotheek koppelingen bijhoudt die op basis van de [`downloadLinkQualifier`](downloadlinkqualifier.md) eigenschap.
* **`clickCollection.externalLinkEnabled`**: Een Booleaanse waarde die bepaalt of koppelingen naar externe domeinen automatisch worden bijgehouden. Bijvoorbeeld: `https://example.com` tot `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: Een Booleaanse waarde die bepaalt of de bibliotheek tot de volgende pagina wacht om gegevens voor het bijhouden van koppelingen te verzenden. Wanneer de volgende pagina wordt geladen, combineert u de gegevens voor het bijhouden van koppelingen met de gebeurtenis page load. Als u deze optie inschakelt, verkleint u het aantal gebeurtenissen dat u naar de Adobe verzendt. Indien `internalLinkEnabled` is uitgeschakeld, heeft deze variabele geen effect.
* **`clickCollection.sessionStorageEnabled`**: Een Booleaanse waarde die bepaalt of de gegevens voor het bijhouden van koppelingen worden opgeslagen in de sessieopslag in plaats van in lokale variabelen. Indien `internalLinkEnabled` of `eventGroupingEnabled` zijn uitgeschakeld, heeft deze variabele geen effect.

  Adobe beveelt sterk aan deze variabele toe te laten wanneer het gebruiken `eventGroupingEnabled`. Indien `eventGroupingEnabled` is ingeschakeld terwijl `sessionStorageEnabled` is uitgeschakeld. Als u op een nieuwe pagina klikt, gaan de gegevens voor het bijhouden van koppelingen verloren omdat deze gegevens niet behouden blijven in de sessieopslag. Terwijl het aanvaardbaar is om onbruikbaar te maken `sessionStorageEnabled` in toepassingen van één pagina, is het niet ideaal voor niet-SPA pagina&#39;s.
* **`filterClickDetails`**: Een callback-functie die volledige besturingselementen biedt voor koppelingsgegevens die u verzamelt. U kunt deze callback functie gebruiken om het verzenden van verbinding het volgen gegevens te veranderen, te verduisteren of te breken. Deze callback is nuttig wanneer u specifieke informatie, zoals persoonlijk identificeerbare informatie binnen verbindingen wilt weglaten.

## Klik inzamelingsmontages gebruikend de de markeringsuitbreiding van SDK van het Web

Selecteer de **[!UICONTROL Enable click data collection]** selectievakje wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Als u dit selectievakje inschakelt, worden de volgende opties weergegeven met betrekking tot het klikken op verzameling:

* [!UICONTROL Internal links]
   * [!UICONTROL Enable event grouping]
   * [!UICONTROL Enable session storage]
* [!UICONTROL External links]
* [!UICONTROL Download links]
* [!UICONTROL Filter click properties]

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens het selectievakje **[!UICONTROL Enable click data collection]**.
1. Selecteer de gewenste montages van de klikinzameling.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

De [!UICONTROL Filter click properties] callback opent een redacteur van de douanecode die u de gewenste code laat opnemen. In de code-editor hebt u toegang tot de volgende variabelen:

* **`content.clickedElement`**: Het DOM-element waarop is geklikt.
* **`content.pageName`**: De paginanaam wanneer de klik plaatsvond.
* **`content.linkName`**: De naam van de geklikte koppeling.
* **`content.linkRegion`**: Het gebied van de aangeklikte koppeling.
* **`content.linkType`**: Het type koppeling (afsluiten, downloaden of andere).
* **`content.linkURL`**: De doel-URL van de aangeklikte koppeling.
* **`return true`**: Sluit de callback onmiddellijk af met de huidige variabelewaarden.
* **`return false`**: Sluit de callback onmiddellijk af en sluit het verzamelen van gegevens af.

Willekeurige variabelen die buiten `content` kunnen worden gebruikt, maar worden niet opgenomen in de lading die naar de Adobe wordt verzonden.

## Klik inzamelingsmontages gebruikend de bibliotheek van SDK van het Web JavaScript

Stel de gewenste variabelen in de `clickCollection` object wanneer het [`configure`](overview.md) gebruiken. Indien niet ingesteld, zijn de standaardinstellingen voor dit object afhankelijk van de waarde van [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: overeenkomsten `clickCollectionEnabled`
* `downloadLinkEnabled`: overeenkomsten `clickCollectionEnabled`
* `externalLinkEnabled`: overeenkomsten `clickCollectionEnabled`
* `eventGroupingEnabled`: Standaard ingesteld op `false`; moet expliciet worden ingeschakeld
* `sessionStorageEnabled`: Standaard ingesteld op `false`; moet expliciet worden ingeschakeld
* `filterClickDetails`: Bevat geen functie; moet expliciet worden geregistreerd

>[!TIP]
>Adobe beveelt aan `eventGroupingEnabled`, omdat dit helpt het aantal gebeurtenissen te verminderen die meetellen voor contractueel gebruik.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```
