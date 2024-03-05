---
title: onBeforeLinkClickSend
description: Callback die net alvorens verbinding het volgen gegevens wordt verzonden.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

De `onBeforeLinkClickSend` Met callback kunt u een JavaScript-functie registreren die de gegevens voor het bijhouden van koppelingen die u verzendt, kan wijzigen voordat de gegevens naar de Adobe worden verzonden. Met deze callback kunt u de `xdm` of `data` -object, inclusief de mogelijkheid om elementen toe te voegen, te bewerken of te verwijderen. U kunt het verzenden van gegevens ook voorwaardelijk annuleren, zoals met ontdekt cliënt-zijbot verkeer. Deze functie wordt ondersteund op Web SDK 2.15.0 of hoger.

Deze callback loopt slechts wanneer [`clickCollectionEnabled`](clickcollectionenabled.md) is ingeschakeld. Indien `clickCollectionEnabled` is uitgeschakeld, wordt deze callback niet uitgevoerd. Als beide `onBeforeEventSend` en `onBeforeLinkClickSend` bevat geregistreerde functies, de `onBeforeLinkClickSend` functie wordt eerst uitgevoerd. Wanneer de `onBeforeLinkClickSend` functie eindigt, de `onBeforeEventSend` wordt uitgevoerd.

>[!WARNING]
>
>Deze callback staat het gebruik van douanecode toe. Als een code die u in de callback opneemt, een niet-afgevangen uitzondering genereert, wordt de verwerking voor de gebeurtenis gestopt. Gegevens worden niet naar de Adobe verzonden.

## Voor de verbinding klikt verzend callback gebruikend de de markeringsuitbreiding van SDK van het Web

Selecteer de **[!UICONTROL Provide on before link click event send callback code]** knop wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Met deze knop opent u een modaal venster waarin u de gewenste code kunt invoegen.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens het selectievakje **[!UICONTROL Enable click data collection]**.
1. Selecteer de knop met het label **[!UICONTROL Provide on before link click event send callback code]**.
1. Met deze knop opent u een modaal venster met een code-editor. Voeg de gewenste code in en klik vervolgens op **[!UICONTROL Save]** om het modale venster te sluiten.
1. Klikken **[!UICONTROL Save]** publiceert u de wijzigingen onder extensie-instellingen.

Binnen de code-editor kunt u elementen toevoegen, bewerken of verwijderen in de `content` object. Dit object bevat de lading die naar de Adobe is verzonden. U hoeft de `content` code binnen een functie plaatsen. Willekeurige variabelen die buiten `content` kunnen worden gebruikt, maar worden niet opgenomen in de lading die naar de Adobe wordt verzonden.

>[!TIP]
>
>De objecten `content.xdm`, `content.data`, en `content.clickedElement` worden altijd in deze context gedefinieerd, zodat u niet hoeft te controleren of ze bestaan. Sommige variabelen binnen deze voorwerpen hangen van uw implementatie en gegevenslaag af. Adobe raadt aan om ongedefinieerde waarden in deze objecten te controleren om JavaScript-fouten te voorkomen.

Stel bijvoorbeeld dat u de volgende handelingen wilt uitvoeren:

* De URL van de huidige pagina wijzigen
* Leg het aangeklikte element in een Adobe Analytics-eVar vast
* Wijzig het koppelingstype van &quot;other&quot; in &quot;download&quot;

De equivalente code binnen het modale venster is als volgt:

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

Op dezelfde manier als [`onBeforeEventSend`](onbeforeeventsend.md), kunt u `return true` om de functie onmiddellijk te voltooien, of `return false` om het verzenden van gegevens onmiddellijk te annuleren. Als u het verzenden van gegevens annuleert in `onBeforeLinkClickSend` wanneer beide `onBeforeEventSend` en `onBeforeLinkClickSend` bevat geregistreerde functies, de `onBeforeEventSend` functie wordt niet uitgevoerd.

## Klik vóór de koppeling op callback verzenden met de Web SDK JavaScript-bibliotheek

Registreer de `onBeforeLinkClickSend` callback wanneer de `configure` gebruiken. U kunt de `content` de naam van een variabele in een willekeurige waarde door de parametervariabele binnen de inline functie te wijzigen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": function(content) {
    // Add, modify, or delete values
    content.xdm.web.webPageDetails.URL = "https://example.com/current.html";
    
    // Return true to immediately complete the function
    if (sendImmediate == true) {
      return true;
    }
    
    // Return false to immediately cancel sending data
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
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeLinkClickSend": lastChanceLinkLogic
});    
```
