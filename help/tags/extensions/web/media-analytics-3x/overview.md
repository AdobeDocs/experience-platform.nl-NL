---
title: Adobe Media Analytics (3.x SDK) voor overzicht van audio- en videoextensie
description: Meer informatie over de Adobe Media Analytics (3.x SDK) voor de extensie van de tags Audio en Video in Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Overzicht van Adobe Media Analytics (3.x SDK) voor audio- en video-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze documentatie voor informatie over het installeren, configureren en implementeren van Adobe Media Analytics (3.x SDK) voor audio- en video-extensie (extensie Media Analytics). Omvat zijn de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel, samen met voorbeelden en verbindingen aan steekproeven te bouwen.

De uitbreiding Media Analytics (MA) voegt de kernJavaScript Media SDK (Media 3.x SDK) toe. Deze extensie biedt de functionaliteit voor het toevoegen van de tracker `Media` aan een site of project waarvoor tags zijn ingeschakeld. De extensie MA vereist twee extra extensies:

* [Extensie Analytics](../analytics/overview.md)
* [Experience Cloud ID-extensie](../id-service/overview.md)

>[!IMPORTANT]
>
>Deze uitbreiding stelt met Media 3.x SDK op, die niet achterwaarts compatibel met Media 2.x SDK is. Als de pagina al Media 2.x SDK gebruikt, gebruikt u [Adobe Media Analytics for Audio and Video Extension](../media-analytics/overview.md) in plaats van deze extensie.

Nadat u alle drie bovengenoemde uitbreidingen in uw markering-toegelaten project hebt omvat, kunt u op één van twee manieren te werk gaan:

* Gebruik `Media` API&#39;s van uw webtoepassing
* Neem een spelerspecifieke extensie op of maak een extensie die specifieke mediaspelergebeurtenissen toewijst aan de API&#39;s in de tracker-instantie `Media`. Deze instantie wordt blootgesteld door de uitbreiding van MA.

## De extensie MA installeren en configureren

* **Installeren:** Als u de extensie MA wilt installeren, opent u de extensie-eigenschap, selecteert u deze  **[!UICONTROL Extensions > Catalog]**, plaatst u de muis boven de  **[!UICONTROL Adobe Media Analytics (3.x SDK) for Audio and Video]** extensie en selecteert u  **[!UICONTROL Install]**.

* **Vorm:** om de uitbreiding van MA te vormen, open het  [!UICONTROL Extensions] lusje, over de uitbreiding te bewegen, en dan te selecteren  **[!UICONTROL Configure]**:

![Configuratie MA-extensie](../../../images/ext-ma-config.png)

### Configuratieopties:

| Optie | Beschrijving |
| :--- | :--- |
| Verzameling-API Server | Definieert de API-server voor mediagroep (neem contact op met uw Adobe-vertegenwoordiger om deze server op te halen) |
| Toepassingsversie | De versie van de mediaspeler-app/SDK |
| Naam speler | Naam van de mediaspeler in gebruik (bijvoorbeeld &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Kanaal | Channel name, eigenschap |
| Foutopsporingsregistratie | Logboekregistratie in- of uitschakelen |
| SSL inschakelen | Enable or Disable sending pings over HTTPS |
| API&#39;s exporteren naar vensterobject | Het exporteren van media-API&#39;s voor analyse naar een algemeen bereik in- of uitschakelen |
| Naam variabele | Een variabele die u gebruikt om media Analytics API&#39;s te exporteren onder het object `window` |

**Herinnering:** De extensie MA vereist de  [](../analytics/overview.md) Analytics en  [Experience Cloud ](../id-service/overview.md) IDextensions. U moet deze uitbreidingen aan uw uitbreidingsbezit ook toevoegen en hen vormen.

## De extensie MA gebruiken

### Werken via een webpagina/JS-app

De extensie MA exporteert de media-API&#39;s in het algemene vensterobject door de instelling &quot;API&#39;s exporteren naar vensterobject&quot; in te schakelen op de pagina [!UICONTROL Configuration]. Het exporteert de API&#39;s onder de naam van de geconfigureerde variabele. Als de variabelenaam bijvoorbeeld `ADB` is, kunnen media-API&#39;s worden benaderd door `window.ADB.Media`.

>[!IMPORTANT]
>
>De extensie MA exporteert de API&#39;s alleen wanneer `window["CONFIGURED_VARIABLE_NAME"]` ongedefinieerd is en bestaande variabelen niet overschrijft.

1. **Media-API&#39;s:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Hiermee worden alle API&#39;s en constanten van de Media SDK weergegeven: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **Instantie van mediabeheer maken:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **Waarde retourneren:** een  `Media` tracker-instantie voor het bijhouden van een mediasessie.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. Volg met de Media tracker-instantie de [JS API-documentatie](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) om mediatracering te implementeren.

U kunt de voorbeeldspeler hier verkrijgen: [Voorbeeldspeler van MA](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). De voorbeeldspeler fungeert als een referentie waarmee u kunt laten zien hoe u de extensie MA kunt gebruiken om Media Analytics rechtstreeks vanuit een webapp te ondersteunen.


### Werken met andere extensies

De extensie MA stelt `media` als een gedeelde module aan andere extensies beschikbaar. (Voor extra informatie over Gedeelde Modules, zie [Gedeelde documentatie van Modules](https://developer.adobelaunch.com/extensions/shared_modules/).)

>[!IMPORTANT]
>
>Gedeelde modules zijn alleen toegankelijk via andere extensies. Met andere woorden, een webpagina/JavaScript-toepassing heeft geen toegang tot de gedeelde modules of gebruik `turbine` (zie codevoorbeeld hieronder) buiten een extensie.

1. **media-API&#39;s:** `media` gedeelde module

   Hiermee worden alle API&#39;s en constanten van de Media SDK weergegeven: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Maak de instantie van Media tracker als volgt:

   **Waarde retourneren:** een  `Media` tracker-instantie voor het bijhouden van een mediasessie.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. Volg met de Media tracker-instantie de [JS API-documentatie](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) om mediatracering te implementeren.

>[!NOTE]
>
>**Testen:** voor deze release moet u de extensie uploaden naar het  [Platform](../../../extension-dev/submit/upload-and-test.md), waar u toegang hebt tot alle afhankelijke extensies.
