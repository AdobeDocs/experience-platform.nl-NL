---
title: onBeforeEventSend
description: Leer hoe te om het Web SDK te vormen om een functie van JavaScript te registreren die de gegevens kunt veranderen u net vóór dat gegeven wordt verzonden naar Adobe.
exl-id: 945f4fa1-380c-46aa-a92a-bbcfd6644751
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# `onBeforeEventSend`

Met de callback van `onBeforeEventSend` kunt u een JavaScript-functie registreren die de gegevens kan wijzigen die u verzendt vlak voordat die gegevens naar Adobe worden verzonden. Met deze callback kunt u het object `xdm` of `data` bewerken, inclusief de mogelijkheid om elementen toe te voegen, te bewerken of te verwijderen. U kunt het verzenden van gegevens ook voorwaardelijk annuleren, zoals met ontdekt cliënt-zijbot verkeer.

>[!WARNING]
>
>Deze callback staat het gebruik van douanecode toe. Als om het even welke code die u in callback opneemt een uncaught uitzondering werpt, wordt de verwerking voor de gebeurtenishalts en **gegevens niet verzonden naar Adobe.**

Registreer de callback `onBeforeEventSend` wanneer u de opdracht `configure` uitvoert. U kunt de naam van de variabele `content` wijzigen in elke gewenste waarde door de parametervariabele binnen de inline functie te wijzigen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  onBeforeEventSend: lastChanceLogic
});    
```

## Vorm vóór gebeurtenis verzend callback gebruikend de de markeringsuitbreiding van SDK van het Web

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ de configuratiemontages van de inzameling van Gegevens ](/help/tags/extensions/client/web-sdk/configure/data-collection.md#on-before-event-send-callback).
