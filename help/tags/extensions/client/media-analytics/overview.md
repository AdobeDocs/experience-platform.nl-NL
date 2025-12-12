---
title: Overzicht van Adobe Media Analytics for Audio and Video Extension
description: Meer informatie over de extensie Adobe Media Analytics for Audio and Video in Adobe Experience Platform.
exl-id: 426cfd08-aead-4b35-824c-45494bca2fc8
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 0%

---

# Overzicht van Adobe Media Analytics voor audio- en video-extensie

Gebruik deze documentatie voor informatie over het installeren, configureren en implementeren van de extensie Adobe Media Analytics voor audio en video (extensie Media Analytics). Omvat zijn de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel, samen met voorbeelden en verbindingen aan steekproeven te bouwen.

De extensie Media Analytics (MA) voegt de core JavaScript Media SDK (Media 2.x SDK) toe. Deze extensie biedt de functionaliteit voor het toevoegen van de `MediaHeartbeat` tracker-instantie aan een tagsite of -project. De extensie MA vereist twee extra extensies:

* [Extensie Analytics](../analytics/overview.md)
* [Experience Cloud ID Extension](../id-service/overview.md)

>[!IMPORTANT]
>
>Voor audiotracering is Analytics Extension v1.6 of hoger vereist.

Nadat u alle drie bovengenoemde uitbreidingen in uw markeringsproject hebt omvat, kunt u op één van twee manieren te werk gaan:

* `MediaHeartbeat` API&#39;s van uw webtoepassing gebruiken
* Neem een spelerspecifieke extensie op of maak een Player-specifieke extensie die specifieke media Player-gebeurtenissen toewijst aan de API&#39;s in de `MediaHeartbeat` tracker-instantie. Deze instantie wordt blootgesteld door de uitbreiding van MA.

## De extensie MA installeren en configureren

* **installeer -** om de uitbreiding van MA te installeren, open uw uitbreidingsbezit, uitgezochte **[!UICONTROL Extensions > Catalog]**, beweegt over de **[!UICONTROL Adobe Media Analytics for Audio and Video]** uitbreiding, en selecteert **[!UICONTROL Install]**.

* **vormt -** om de uitbreiding van MA te vormen, open het [!UICONTROL Extensions] lusje, over de uitbreiding te bewegen, en dan te selecteren **[!UICONTROL Configure]**:

![&#x200B; de Configuratie van de Uitbreiding van MA &#x200B;](../../../images/ext-va-config.jpg)

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
| Naam variabele | Een variabele die u gebruikt om Media Analytics API&#39;s te exporteren onder het `window` -object |

**Herinnering:** de uitbreiding van MA vereist de [&#x200B; Analytics &#x200B;](../analytics/overview.md) en [&#x200B; identiteitskaart van Experience Cloud &#x200B;](../id-service/overview.md) uitbreidingen. U moet deze uitbreidingen aan uw uitbreidingsbezit ook toevoegen en hen vormen.

## De extensie MA gebruiken

### Werken via een webpagina/JS-app

De extensie MA exporteert de MediaHeartbone-API&#39;s in het algemene vensterobject door de instelling &#39;API&#39;s exporteren naar vensterobject&#39; in te schakelen op de pagina [!UICONTROL Configuration] . Het exporteert de API&#39;s onder de naam van de geconfigureerde variabele. Als de variabelenaam bijvoorbeeld is ingesteld op `ADB` , kan MediaHeartbeat worden benaderd door `window.ADB.MediaHeartbeat` .

>[!IMPORTANT]
>
>De extensie MA exporteert de API&#39;s alleen wanneer `window["CONFIGURED_VARIABLE_NAME"]` ongedefinieerd is en bestaande variabelen niet overschrijft.

1. **creeer MediaHeartbone Instantie:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **Params:** Een geldig afgevaardigde voorwerp dat deze functies blootstelt.

   | Methode |  Beschrijving   |
   | :--- | :--- |
   | `getQoSObject()` | Retourneert `theMediaObject` -instantie die de huidige QoS-informatie bevat. Deze methode wordt meerdere keren aangeroepen tijdens een afspeelsessie. De implementatie van de speler moet altijd de recentst beschikbare gegevens terugkeren QoS. |
   | `getCurrentPlaybackTime()` | Retourneert de huidige positie van de afspeelkop. Voor het bijhouden van VOD wordt de waarde opgegeven in seconden vanaf het begin van het media-item. Voor het bijhouden van LIVE-/LIVE-waarden wordt de waarde opgegeven in seconden vanaf het begin van het programma. |

   **Waarde van de Terugkeer:** Een belofte die of met a `MediaHeartbeat` instantie of verwerpt met een foutenmelding lost.

1. **De Constanten van MediaHeartbeat van de Toegang:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   Dit stelt alle constanten en statische methodes van de [`MediaHeartbeat` &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) klasse bloot.

   U kunt de steekproefspeler hier verkrijgen: [&#x200B; Speler van de Steekproef van MA &#x200B;](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). De voorbeeldspeler fungeert als een referentie waarmee u kunt laten zien hoe u de extensie MA kunt gebruiken om Media Analytics rechtstreeks vanuit een webapp te ondersteunen.

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

De extensie MA stelt de gedeelde `get-instance` en `media-heartbeat` modules beschikbaar voor andere extensies. (Voor extra informatie over Gedeelde Modules, zie [&#x200B; Gedeelde documentatie van Modules &#x200B;](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Gedeelde modules zijn alleen toegankelijk via andere extensies. Een webpagina/JS-toepassing heeft dus geen toegang tot de gedeelde modules of kan `turbine` (zie het codevoorbeeld hieronder) buiten een extensie gebruiken.

1. **creeer de Instantie MediaHeartbeat:** `get-instance` Gedeelde Module

   **Params:**

   * Een geldig gedelegeerd object dat deze functies toegankelijk maakt:

     | Methode |  Beschrijving   |
     | :--- | :--- |
     | `getQoSObject()` | Retourneert de `MediaObject` -instantie die de huidige QoS-informatie bevat. Deze methode wordt meerdere keren aangeroepen tijdens een afspeelsessie. De spelerimplementatie moet altijd de laatst beschikbare gegevens terugkeren QoS. |
     | `getCurrentPlaybackTime()` | Retourneert de huidige positie van de afspeelkop. Voor het bijhouden van VOD wordt de waarde opgegeven in seconden vanaf het begin van het media-item. Voor het bijhouden van LIVE-/LIVE-waarden wordt de waarde opgegeven in seconden vanaf het begin van het programma. |

   * Een optioneel config-object dat deze eigenschappen toegankelijk maakt:

     | Eigenschap | Beschrijving | Vereist |
     | :--- | :--- | :--- |
     | Onlinevideoprovider | Naam van het online videoplatform waarmee inhoud wordt gedistribueerd. | Nee. Indien aanwezig, treedt de waarde met voeten die tijdens uitbreidingsconfiguratie wordt bepaald. |
     | Naam speler | Naam van de mediaspeler in gebruik (bijvoorbeeld &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) | Nee. Indien aanwezig, treedt de waarde met voeten die tijdens uitbreidingsconfiguratie wordt bepaald. |
     | Kanaal | Channel name, eigenschap | Nee. Indien aanwezig, treedt de waarde met voeten die tijdens uitbreidingsconfiguratie wordt bepaald. |

   **Waarde van de Terugkeer:** Een belofte die of met a `MediaHeartbeat` instantie of verwerpt met een foutenmelding lost.

1. **De Constanten van MediaHeartbeat van de Toegang:** `media-heartbeat` Gedeelde Module

   Deze module stelt alle constanten en statische methodes van deze klasse bloot: [&#x200B; https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

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

1. Gebruikend de instantie van de Hartslag van Media, volg de [&#x200B; documentatie van SDK JS van Media &#x200B;](https://experienceleague.adobe.com/docs/media-analytics/using/legacy-implementations/legacy-media-sdks/setup-javascript/set-up-js-2.html?lang=nl-NL) en [&#x200B; JS API documentatie &#x200B;](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html) om media het volgen uit te voeren.

>[!NOTE]
>
>**het Testen:** voor deze versie, om uw uitbreiding te testen moet u het aan [&#x200B; Experience Platform &#x200B;](../../../extension-dev/submit/upload-and-test.md) uploaden, waar u toegang tot alle afhankelijke uitbreidingen hebt.


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
