---
title: onBeforeEventSend
description: Callback die precies loopt alvorens het gegeven wordt verzonden.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# `onBeforeEventSend`

De `onBeforeEventSend` Met callback kunt u een JavaScript-functie registreren die de gegevens kan wijzigen die u verzendt vlak voordat die gegevens naar de Adobe worden verzonden. Met deze callback kunt u de `xdm` of `data` -object, inclusief de mogelijkheid om elementen toe te voegen, te bewerken of te verwijderen. U kunt het verzenden van gegevens ook voorwaardelijk annuleren, zoals met ontdekt cliënt-zijbot verkeer.

>[!WARNING]
>
>Deze callback staat het gebruik van douanecode toe. Als een code die u in de callback opneemt, een niet-afgevangen uitzondering genereert, wordt de verwerking voor de gebeurtenis gestopt. Gegevens worden niet naar de Adobe verzonden.

## Voor de gebeurtenis verzendt u callback met de Web SDK-tagextensie

Selecteer de **[!UICONTROL Provide on before event send callback code]** knop wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Met deze knop opent u een modaal venster waarin u de gewenste code kunt invoegen.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens de knop **[!UICONTROL Provide on before event send callback code]**.
1. Met deze knop opent u een modaal venster met een code-editor. Voeg de gewenste code in en klik vervolgens op **[!UICONTROL Save]** om het modale venster te sluiten.
1. Klikken **[!UICONTROL Save]** publiceert u de wijzigingen onder extensie-instellingen.

Binnen de code-editor kunt u elementen toevoegen, bewerken of verwijderen in de `content` object. Dit object bevat de lading die naar de Adobe is verzonden. U hoeft de `content` code binnen een functie plaatsen. Willekeurige variabelen die buiten `content` kunnen worden gebruikt, maar worden niet opgenomen in de lading die naar de Adobe wordt verzonden.

>[!TIP]
>
>De objecten `content.xdm` en `content.data` worden altijd in deze context gedefinieerd, zodat u niet hoeft te controleren of ze bestaan. Sommige variabelen binnen deze voorwerpen hangen van uw implementatie en gegevenslaag af. Adobe raadt aan om ongedefinieerde waarden in deze objecten te controleren om JavaScript-fouten te voorkomen.

Als u bijvoorbeeld wilt:

* Het XDM-element toevoegen `xdm.commerce.order.purchaseID`
* Alle tekens afdwingen in `xdm.marketing.trackingCode` in kleine letters
* Verwijderen `xdm.environment.operatingSystemVersion`
* Als een gebeurtenistype een koppelingsklik is, verzendt onmiddellijk gegevens ongeacht de code hieronder
* Het verzenden van gegevens naar de Adobe annuleren als een bot wordt aangetroffen

De equivalente code binnen het modale venster is als volgt:

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

>[!NOTE]
>
>Vermijd het terugkeren `false` op de eerste gebeurtenis op een pagina. Terugkeren `false` op de eerste gebeurtenis kan de personalisatie negatief beïnvloeden.

## Voor de gebeurtenis moet u callback verzenden met de Web SDK JavaScript-bibliotheek

Registreer de `onBeforeEventSend` callback wanneer de `configure` gebruiken. U kunt de `content` de naam van een variabele in een willekeurige waarde door de parametervariabele binnen de inline functie te wijzigen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": lastChanceLogic
});    
```
