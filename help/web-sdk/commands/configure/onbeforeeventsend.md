---
title: onBeforeEventSend
description: Leer hoe te om SDK van het Web te vormen om een functie van JavaScript te registreren die de gegevens kunt veranderen u net vóór dat gegeven wordt verzonden naar Adobe.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# `onBeforeEventSend`

De `onBeforeEventSend` Met callback kunt u een JavaScript-functie registreren die de gegevens kan wijzigen die u verzendt vlak voordat de gegevens naar de Adobe worden verzonden. Met deze callback kunt u de `xdm` of `data` -object, inclusief de mogelijkheid om elementen toe te voegen, te bewerken of te verwijderen. U kunt het verzenden van gegevens ook voorwaardelijk annuleren, zoals met ontdekt cliënt-zijbot verkeer.

>[!WARNING]
>
>Deze callback staat het gebruik van douanecode toe. Als een code die u in de callback opneemt, een niet-afgevangen uitzondering genereert, wordt de verwerking voor de gebeurtenis gestopt. Gegevens worden niet naar de Adobe verzonden.

## Vorm vóór gebeurtenis verzend callback gebruikend de de markeringsuitbreiding van SDK van het Web {#tag-extension}

Selecteer de **[!UICONTROL Provide on before event send callback code]** knop wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Met deze knop opent u een modaal venster waarin u de gewenste code kunt invoegen.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens de knop **[!UICONTROL Provide on before event send callback code]**.
1. Met deze knop opent u een modaal venster met een code-editor. Voeg de gewenste code in en klik vervolgens op **[!UICONTROL Save]** om het modale venster te sluiten.
1. Klikken **[!UICONTROL Save]** publiceert u de wijzigingen onder extensie-instellingen.

In de code-editor hebt u toegang tot de volgende variabelen:

* **`content.xdm`**: De [XDM](../sendevent/xdm.md) payload voor de gebeurtenis.
* **`content.data`**: De [data](../sendevent/data.md) objectlading voor de gebeurtenis.
* **`return true`**: Sluit de callback onmiddellijk af en verstuur gegevens naar de Adobe met de huidige waarden in het dialoogvenster `content` object.
* **`return false`**: Sluit de callback onmiddellijk af en sluit het verzenden van gegevens naar de Adobe af.

Willekeurige variabelen die buiten `content` kunnen worden gebruikt, maar worden niet opgenomen in de lading die naar de Adobe wordt verzonden.

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Vermijd het terugkeren `false` op de eerste gebeurtenis op een pagina. Terugkeren `false` op de eerste gebeurtenis kan de personalisatie negatief beïnvloeden.

## Vorm vóór gebeurtenis verzendt callback gebruikend de bibliotheek van JavaScript van SDK van het Web {#library}

Registreer de `onBeforeEventSend` callback wanneer de `configure` gebruiken. U kunt de `content` de naam van een variabele in een willekeurige waarde door de parametervariabele binnen de inline functie te wijzigen.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: function(content) {
    // Use nullish coalescing assignments to add a new value
    content.xdm._experience ??= {};
    content.xdm._experience.analytics ??= {};
    content.xdm._experience.analytics.customDimensions ??= {};
    content.xdm._experience.analytics.customDimensions.eVars ??= {};
    content.xdm._experience.analytics.customDimensions.eVars.eVar1 = "Analytics custom value";
    
    // Use optional chaining to change an existing value
    if(content.xdm.web?.webPageDetails) content.xdm.web.webPageDetails.URL = content.xdm.web.webPageDetails.URL.toLowerCase();
    
    // Remove an existing value
    if(content.xdm.web?.webReferrer) delete content.xdm.web.webReferrer.URL;
    
    // Return true to immediately send data
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
    if(myBotDetector.isABot()){
      return false;
    }
    
    // Assign the value in the 'cid' query string to the tracking code XDM element
    content.xdm.marketing ??= {};
    content.xdm.marketing.trackingCode = new URLSearchParams(window.location.search).get('cid');
  }
});
```

U kunt ook uw eigen functie registreren in plaats van een inline functie.

```js
function lastChanceLogic(content) {
  content.xdm.application ??= {};
  content.xdm.application.name = "App name";
}

alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```
