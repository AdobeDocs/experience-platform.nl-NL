---
title: Adobe Media Analytics (3.x SDK) voor overzicht van audio- en videoextensie
description: Leer meer over de Adobe Media Analytics (3.x SDK) voor Audio en Video markeringsuitbreiding in Adobe Experience Platform.
exl-id: 7289d57d-7e7f-4832-9469-3b5a62183a32
source-git-commit: e21ed1e9fd0c2678551cfc664b611076c198a157
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Overzicht van Adobe Media Analytics (3.x SDK) voor audio- en video-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Gebruik deze documentatie voor informatie over het installeren, configureren en implementeren van Adobe Media Analytics (3.x SDK) voor audio- en video-extensie (extensie Media Analytics). Omvat zijn de opties beschikbaar wanneer het gebruiken van deze uitbreiding om een regel, samen met voorbeelden en verbindingen aan steekproeven te bouwen.

De extensie Media Analytics (MA) voegt de core JavaScript Media SDK (Media 3.x SDK) toe. Deze extensie biedt de functionaliteit voor het toevoegen van de `Media` tracker-instantie aan een site of project waarvoor tags zijn ingeschakeld. De extensie MA vereist twee extra extensies:

* [Extensie Analytics](../analytics/overview.md)
* [Extensie Experience Cloud-id](../id-service/overview.md)

>[!IMPORTANT]
>
>Deze uitbreiding stelt met Media 3.x SDK op, die niet achterwaarts compatibel met Media 2.x SDK is. Aangezien 2.x is afgekeurd, moet u een update naar 3.x uitvoeren.

Nadat u alle drie bovengenoemde uitbreidingen in uw markering-toegelaten project hebt omvat, kunt u op één van twee manieren te werk gaan:

* `Media` API&#39;s van uw webtoepassing gebruiken
* Neem een spelerspecifieke extensie op of maak een Player-specifieke extensie die specifieke media Player-gebeurtenissen toewijst aan de API&#39;s in de `Media` tracker-instantie. Deze instantie wordt blootgesteld door de uitbreiding van MA.

## De extensie MA installeren en configureren

* **installeer:** om de uitbreiding van MA te installeren, open uw uitbreidingsbezit, selecteer **[!UICONTROL Extensions > Catalog]**, beweegt over de **[!UICONTROL Adobe Media Analytics (3.x SDK) for Audio and Video]** uitbreiding, en selecteert **[!UICONTROL Install]**.

* **vormt:** om de uitbreiding van MA te vormen, open het [!UICONTROL Extensions] lusje, over de uitbreiding te bewegen, en dan te selecteren **[!UICONTROL Configure]**:

![ de Configuratie van de Uitbreiding van MA ](../../../images/ext-ma-config.png)

### Configuratieopties:

| Optie | Beschrijving |
| :--- | :--- |
| Verzameling-API Server | Definieert de API-server voor mediagroep (neem contact op met uw Adobe om deze server op te halen) |
| Toepassingsversie | De versie van de mediaspeler-app/SDK |
| Naam speler | Naam van de mediaspeler in gebruik (bijvoorbeeld &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Kanaal | Channel name, eigenschap |
| Foutopsporingsregistratie | Logboekregistratie in- of uitschakelen |
| SSL inschakelen | Enable or Disable sending pings over HTTPS |
| API&#39;s exporteren naar vensterobject | Het exporteren van media-API&#39;s voor analyse naar een algemeen bereik in- of uitschakelen |
| Naam variabele | Een variabele die u gebruikt om Media Analytics API&#39;s te exporteren onder het `window` -object |

**Herinnering:** de uitbreiding van MA vereist de [ Analytics ](../analytics/overview.md) en [ identiteitskaart van het Experience Cloud ](../id-service/overview.md) uitbreidingen. U moet deze uitbreidingen aan uw uitbreidingsbezit ook toevoegen en hen vormen.

## De extensie MA gebruiken

### Werken via een webpagina/JS-app

De extensie MA exporteert de media-API&#39;s in het algemene vensterobject door de instelling &quot;API&#39;s exporteren naar vensterobject&quot; in te schakelen op de pagina [!UICONTROL Configuration] . Het exporteert de API&#39;s onder de naam van de geconfigureerde variabele. Als de variabelenaam bijvoorbeeld is ingesteld op `ADB` , kunnen media-API&#39;s worden benaderd door `window.ADB.Media` .

>[!IMPORTANT]
>
>De extensie MA exporteert de API&#39;s alleen wanneer `window["CONFIGURED_VARIABLE_NAME"]` ongedefinieerd is en bestaande variabelen niet overschrijft.

1. **Media APIs:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Dit stelt alle APIs en constanten van Media SDK bloot: [ https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **creeer de Instantie van de Beheerder van Media:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **de Waarde van de Terugkeer:** A `Media` controle instantie voor het volgen van een media zitting.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. Gebruikend de instantie van de Tracker van Media, volg de [ JS API documentatie ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) om media het volgen uit te voeren.

U kunt de steekproefspeler hier verkrijgen: [ Speler van de Steekproef van MA ](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). De voorbeeldspeler fungeert als een referentie waarmee u kunt laten zien hoe u de extensie MA kunt gebruiken om Media Analytics rechtstreeks vanuit een webapp te ondersteunen.


### Werken met andere extensies

De extensie MA stelt `media` als een gedeelde module beschikbaar voor andere extensies. (Voor extra informatie over Gedeelde Modules, zie [ Gedeelde documentatie van Modules ](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Gedeelde modules zijn alleen toegankelijk via andere extensies. Een webpagina/JavaScript-toepassing heeft dus geen toegang tot de gedeelde modules of kan `turbine` (zie het codevoorbeeld hieronder) buiten een extensie gebruiken.

1. **Media APIs:** `media` Gedeelde Module

   Dit stelt alle APIs en constanten van Media SDK bloot: [ https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Maak de instantie van Media tracker als volgt:

   **de Waarde van de Terugkeer:** A `Media` controle instantie voor het volgen van een media zitting.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. Gebruikend de instantie van de Tracker van Media, volg de [ JS API documentatie ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) om media het volgen uit te voeren.

>[!NOTE]
>
>**het Testen:** voor deze versie, om uw uitbreiding te testen moet u het aan [ Platform ](../../../extension-dev/submit/upload-and-test.md) uploaden, waar u toegang tot alle afhankelijke uitbreidingen hebt.
