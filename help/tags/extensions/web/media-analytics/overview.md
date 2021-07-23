---
title: Overzicht van Adobe Media-analyse voor audio- en videoextensie
description: Meer informatie over de extensie Adobe Media Analytics for Audio and Video in Adobe Experience Platform.
source-git-commit: 7f694310b17ab257eae459003bb820f7221bb55e
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 1%

---

# Overzicht van Adobe Media Analytics voor audio- en video-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze documentatie voor informatie over het installeren, het vormen, en het uitvoeren van de Adobe Media Analytics voor Audio en Video uitbreiding (de uitbreiding van de Analyse van Media). Omvat zijn de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel, samen met voorbeelden en verbindingen aan steekproeven te bouwen.

De uitbreiding Media Analytics (MA) voegt de kernJavaScript Media SDK (Media 2.x SDK) toe. Deze extensie biedt de functionaliteit voor het toevoegen van de tracker `MediaHeartbeat` aan een tagsite of -project. De extensie MA vereist twee extra extensies:

* [Extensie Analytics](../analytics/overview.md)
* [Experience Cloud ID-extensie](../id-service/overview.md)

>[!IMPORTANT]
>
>Voor audiotracering is Analytics Extension v1.6 of hoger vereist.

Nadat u alle drie bovengenoemde uitbreidingen in uw markeringsproject hebt omvat, kunt u op één van twee manieren te werk gaan:

* Gebruik `MediaHeartbeat` API&#39;s van uw webtoepassing
* Neem een spelerspecifieke extensie op of maak een extensie die specifieke mediaspelergebeurtenissen toewijst aan de API&#39;s in de tracker-instantie `MediaHeartbeat`. Deze instantie wordt blootgesteld door de uitbreiding van MA.

## De extensie MA installeren en configureren

* **Installeer -** om de uitbreiding van MA te installeren, open uw uitbreidingsbezit, selecteer  **[!UICONTROL Extensions > Catalog]**, houd over de  **[!UICONTROL Adobe Media Analytics for Audio and Video]** uitbreiding, en selecteer  **[!UICONTROL Install]**.

* **Vorm -** om de uitbreiding van MA te vormen, open het  [!UICONTROL Extensions] lusje, beweeg over de uitbreiding, en selecteer dan  **[!UICONTROL Configure]**:

![Configuratie MA-extensie](../../../images/ext-va-config.jpg)

### Configuratieopties:

| Optie | Beschrijving |
| :--- | :--- |
| Trackingserver | Definieert de server voor het bijhouden van mediakoppen (dit is niet dezelfde server als de analytische trackingserver). |
| Toepassingsversie | De versie van de mediaspeler-app/SDK |
| Naam speler | Naam van de mediaspeler in gebruik (bijvoorbeeld &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Kanaal | Channel name, eigenschap |
| Onlinevideoprovider | Naam van het onlinevideoplatform waarmee inhoud wordt gedistribueerd |
| Foutopsporingsregistratie | Logboekregistratie in- of uitschakelen |
| SSL inschakelen | Enable or Disable sending pings over HTTPS |
| API&#39;s exporteren naar vensterobject | Het exporteren van media-API&#39;s voor analyse naar een algemeen bereik in- of uitschakelen |
| Naam variabele | Een variabele die u gebruikt om media Analytics API&#39;s te exporteren onder het object `window` |

**Herinnering:** De extensie MA vereist de  [](../analytics/overview.md) Analytics en  [Experience Cloud ](../id-service/overview.md) IDextensions. U moet deze uitbreidingen aan uw uitbreidingsbezit ook toevoegen en hen vormen.

## De extensie MA gebruiken

### Werken via een webpagina/JS-app

De extensie MA exporteert de MediaHeartbone-API&#39;s in het algemene vensterobject door de instelling &#39;API&#39;s exporteren naar vensterobject&#39; in te schakelen op de pagina [!UICONTROL Configuration]. Het exporteert de API&#39;s onder de naam van de geconfigureerde variabele. Bijvoorbeeld, als de veranderlijke naam om `ADB` wordt gevormd te zijn dan kan MediaHeartbeat door `window.ADB.MediaHeartbeat` worden betreden.

>[!IMPORTANT]
>
>De extensie MA exporteert de API&#39;s alleen wanneer `window["CONFIGURED_VARIABLE_NAME"]` ongedefinieerd is en bestaande variabelen niet overschrijft.

1. **MediaHeartbone-instantie maken:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **Params:** een geldig gedelegeerd object dat deze functies toegankelijk maakt.

   | Methode |  Beschrijving   |
   | :--- | :--- |
   | `getQoSObject()` | Retourneert `theMediaObject`-instantie die huidige QoS-informatie bevat. Deze methode wordt meerdere keren aangeroepen tijdens een afspeelsessie. De implementatie van de speler moet altijd de recentst beschikbare gegevens terugkeren QoS. |
   | `getCurrentPlaybackTime()` | Retourneert de huidige positie van de afspeelkop. Voor het bijhouden van VOD wordt de waarde opgegeven in seconden vanaf het begin van het media-item. Voor LIVE/LIVE-tracking wordt de waarde opgegeven in seconden vanaf het begin van het programma. |

   **Geretourneerde waarde:** een belofte die met een  `MediaHeartbeat` instantie wordt opgelost of die met een foutbericht wordt afgewezen.

1. **Toegang tot MediaHeartbone-constanten:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   Dit stelt alle constanten en statische methodes van de [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) klasse bloot.

   U kunt de voorbeeldspeler hier verkrijgen: [Voorbeeldspeler van MA](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). De voorbeeldspeler fungeert als een referentie waarmee u kunt laten zien hoe u de extensie MA kunt gebruiken om Media Analytics rechtstreeks vanuit een webapp te ondersteunen.

1. Maak als volgt de instantie van MediaHeartbone tracker:

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### Werken met andere extensies

De uitbreiding van MA stelt `get-instance` en `media-heartbeat` gedeelde modules aan andere uitbreidingen bloot. (Voor extra informatie over Gedeelde Modules, zie [Gedeelde documentatie van Modules](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Gedeelde modules zijn alleen toegankelijk via andere extensies. Een webpagina/JS-toepassing heeft dus geen toegang tot de gedeelde modules of gebruik `turbine` (zie codevoorbeeld hieronder) buiten een extensie.

1. **MediaHeartPlay-instantie maken:** `get-instance` Gedeelde module

   **Param:**

   * Een geldig gedelegeerd object dat deze functies toegankelijk maakt:

      | Methode |  Beschrijving   |
      | :--- | :--- |
      | `getQoSObject()` | Retourneert de instantie `MediaObject` die de huidige QoS-informatie bevat. Deze methode wordt meerdere keren aangeroepen tijdens een afspeelsessie. De spelerimplementatie moet altijd de laatst beschikbare gegevens terugkeren QoS. |
      | `getCurrentPlaybackTime()` | Retourneert de huidige positie van de afspeelkop. Voor het bijhouden van VOD wordt de waarde opgegeven in seconden vanaf het begin van het media-item. Voor LIVE/LIVE-tracking wordt de waarde opgegeven in seconden vanaf het begin van het programma. |

   * Een optioneel config-object dat deze eigenschappen toegankelijk maakt:

      | Eigenschap | Beschrijving | Vereist |
      | :--- | :--- | :--- |
      | Onlinevideoprovider | Naam van het onlinevideoplatform waarmee inhoud wordt gedistribueerd. | Nee. Indien aanwezig, treedt de waarde met voeten die tijdens uitbreidingsconfiguratie wordt bepaald. |
      | Naam speler | Naam van de mediaspeler in gebruik (bijvoorbeeld &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) | Nee. Indien aanwezig, treedt de waarde met voeten die tijdens uitbreidingsconfiguratie wordt bepaald. |
      | Kanaal | Channel name, eigenschap | Nee. Indien aanwezig, treedt de waarde met voeten die tijdens uitbreidingsconfiguratie wordt bepaald. |
   **Geretourneerde waarde:** een belofte die met een  `MediaHeartbeat` instantie wordt opgelost of die met een foutbericht wordt afgewezen.

1. **Toegang krijgen tot MediaHeartbone-constanten:** `media-heartbeat` Gedeelde module

   Deze module stelt alle constanten en statische methoden van deze klasse beschikbaar: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

1. Maak als volgt de instantie van MediaHeartbone tracker:

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. Gebruik de Media Heartbone-instantie om de JS-documentatie](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-javascript/set-up-js-2.html) en [JS API-documentatie](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html) van [Media SDK te gebruiken voor het implementeren van mediatracering.

>[!NOTE]
>
>**Testen:** voor deze release moet u de extensie uploaden naar het  [Platform](../../../extension-dev/submit/upload-and-test.md), waar u toegang hebt tot alle afhankelijke extensies.


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->
