---
title: onBeforeLinkClickSend
description: Callback die net alvorens verbinding het volgen gegevens wordt verzonden.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Deze callback is vervangen. Gebruiken [`filterClickDetails`](clickcollection.md) in plaats daarvan.

De `onBeforeLinkClickSend` Met callback kunt u een JavaScript-functie registreren die de gegevens voor het bijhouden van koppelingen die u verzendt, kan wijzigen voordat de gegevens naar de Adobe worden verzonden. Met deze callback kunt u de `xdm` of `data` -object, inclusief de mogelijkheid om elementen toe te voegen, te bewerken of te verwijderen. U kunt het verzenden van gegevens ook voorwaardelijk annuleren, zoals met ontdekt cliënt-zijbot verkeer. Deze functie wordt ondersteund op Web SDK 2.15.0 of hoger.

Deze callback loopt slechts wanneer [`clickCollectionEnabled`](clickcollectionenabled.md) is ingeschakeld en [`filterClickDetails`](clickcollection.md) bevat geen geregistreerde functie. Indien `clickCollectionEnabled` is uitgeschakeld of als `filterClickDetails` bevat een geregistreerde functie, dan wordt deze callback niet uitgevoerd. Indien `onBeforeEventSend` en `onBeforeLinkClickSend` beide geregistreerde functies bevatten, `onBeforeLinkClickSend` wordt eerst uitgevoerd.

>[!WARNING]
>
>Deze callback staat het gebruik van douanecode toe. Als een code die u in de callback opneemt, een niet-afgevangen uitzondering genereert, wordt de verwerking voor de gebeurtenis gestopt. Gegevens worden niet naar de Adobe verzonden.

## Vorm vóór verbinding klikken verzend callback gebruikend de de markeringsuitbreiding van SDK van het Web {#tag-extension}

Selecteer de **[!UICONTROL Provide on before link click event send callback code]** knop wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Met deze knop opent u een modaal venster waarin u de gewenste code kunt invoegen.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens het selectievakje **[!UICONTROL Enable click data collection]**.
1. Selecteer de knop met het label **[!UICONTROL Provide on before link click event send callback code]**.
1. Met deze knop opent u een modaal venster met een code-editor. Voeg de gewenste code in en klik vervolgens op **[!UICONTROL Save]** om het modale venster te sluiten.
1. Klikken **[!UICONTROL Save]** publiceert u de wijzigingen onder extensie-instellingen.

In de code-editor hebt u toegang tot de volgende variabelen:

* **`content.clickedElement`**: Het DOM-element waarop is geklikt.
* **`content.xdm`**: De XDM-lading voor de gebeurtenis.
* **`content.data`**: De payload van het gegevensobject voor de gebeurtenis.
* **`return true`**: Sluit de callback onmiddellijk af met de huidige variabelewaarden. De `onBeforeEventSend` callback wordt uitgevoerd als het een geregistreerde functie bevat.
* **`return false`**: Sluit de callback onmiddellijk af en sluit het verzenden van gegevens naar de Adobe af. De `onBeforeEventSend` callback wordt niet uitgevoerd.

Willekeurige variabelen die buiten `content` kunnen worden gebruikt, maar worden niet opgenomen in de lading die naar de Adobe wordt verzonden.

```js
// Set an already existing value to something else
content.xdm.web.webPageDetails.URL = "https://example.com/current.html";

// Use nullish coalescing assignments to create objects if they don't yet exist, preventing undefined errors. 
// Can be omitted if you are certain that the object is already defined
content.xdm._experience ??= {};
content.xdm._experience.analytics ??= {};
content.xdm._experience.analytics.customDimensions ??= {};
content.xdm._experience.analytics.customDimensions.eVars ??= {};

// Then set the property to the clicked element
content.xdm._experience.analytics.customDimensions.eVars.eVar1 = content.clickedElement;

// Use optional chaining to check if each object is defined, preventing undefined errors
if(content.xdm.web?.webInteraction?.type === "other") content.xdm.web.webInteraction.type = "download";
```

Op dezelfde manier als [`onBeforeEventSend`](onbeforeeventsend.md), kunt u `return true` om de functie onmiddellijk te voltooien, of `return false` om het verzenden van gegevens naar de Adobe te annuleren. Als u het verzenden van gegevens afbreekt in `onBeforeLinkClickSend` wanneer beide `onBeforeEventSend` en `onBeforeLinkClickSend` bevat geregistreerde functies, de `onBeforeEventSend` functie wordt niet uitgevoerd.

## Configureer op voordat de koppeling klikt en stuur callback met behulp van de Web SDK JavaScript-bibliotheek {#library}

Registreer de `onBeforeLinkClickSend` callback wanneer de `configure` gebruiken. U kunt de `content` de naam van een variabele in een willekeurige waarde door de parametervariabele binnen de inline functie te wijzigen.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to complete the function immediately
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to cancel sending data immediately
    if(myBotDetector.isABot()){
      return false;
    }
  }
});
```

U kunt ook uw eigen functie registreren in plaats van een inline functie.

```js
function lastChanceLinkLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeLinkClickSend: lastChanceLinkLogic
});    
```
