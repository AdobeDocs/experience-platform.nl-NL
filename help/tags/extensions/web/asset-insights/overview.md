---
title: Overzicht van de extensie Asset Insights AEM
description: Meer informatie over de tagextensie AEM Asset Insights in Adobe Experience Platform.
source-git-commit: 1d3415146335d3011963c969d5b6aeea1f1a51d0
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Overzicht van de extensie Asset Insights AEM

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Deze extensie is bedoeld voor gebruik in combinatie met [AEM Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html). Meer bepaald vervangt deze code het proces pageTracker en sluit deze in. Als deze extensie is geconfigureerd, verzendt deze extensie Asset *Impression* en *Click* metrics naar Adobe Analytics, waarna deze worden geïmporteerd in de rapporten AEM Asset Insights. De gegevens van de activa kunnen dan worden gerapporteerd door of AEM Inzichten van Activa of de Werkruimten van het Project van Adobe Analytics te gebruiken.

## Voorwaarden voor extensies

### Analytics

De rapporten AEM Asset in Analytics bevatten drie AEM:

* Element-id
* Middelbron
* Element geklikt

Er zijn ook twee meetwaarden:
* Impressies van elementen
* Elementklikken.

Deze rapporten moeten worden toegelaten gebruikend de Beheerder van de Analyse (uitgezocht **[!UICONTROL Analytics]> [!UICONTROL Admin] > [!UICONTROL Report Suites] > `<report suite>` > [!UICONTROL Edit Settings] > [!UICONTROL AEM] >[!UICONTROL AEM Assets Reporting]**) alvorens zij kunnen worden bevolkt gebruikend deze uitbreiding.

De tagextensie &quot;*Adobe Analytics*&quot; voor Adobe Experience Platform moet in dezelfde webeigenschap worden geïnstalleerd.

### Adobe Experience Manager (AEM)

1. Schakel [AEM Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) in. Selecteer in AEM **[!UICONTROL Tools > Assets]** en open vervolgens het deelvenster **[!UICONTROL Insights Configuration]**.

1. UUID-tracking uitschakelen.

   >[!IMPORTANT]
   >
   >Deze extensie werkt *niet* als de instelling **[!UICONTROL Disable UUID Tracking]** voor configuratie van AEM element is ingeschakeld. Deze optie is standaard uitgeschakeld.

   ![UUID-tracking uitschakelen](images/disableassets.jpg)

## Adobe Experience Manager configureren (AEM)

In deze sectie wordt beschreven hoe u AEM kunt configureren met tags in Adobe Experience Platform, hoe u Asset Insight kunt inschakelen in AEM en hoe u het bijhouden van UID-codes kunt inschakelen voor elementen.

### AEM integreren met tags

De aanbevolen integratie van [Platform](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) met Adobe Experience Manager gebeurt via Adobe I/O.

1. [AEM met tags verbinden met behulp van Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

2. [Maak een Adobe Experience Platform Cloud Service configuratie](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/create-launch-cloud-service.html).

### Asset Insight inschakelen in AEM

Zie [Experience Manager 6.5 Assets-gebruikershandleiding](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) voor instructies voor het inschakelen van Asset Insights.

### UUID-tracking inschakelen voor middelen

Elementen bijhouden in Analytics met behulp van de UUID van het element in AEM.

Om het volgen met UUID van de activa toe te laten, open de console van het componentenbeleid van het editable malplaatje en uncheck het &quot;UUID het volgen&quot;bezit onbruikbaar maken. (Deze eigenschap wordt standaard gecontroleerd op de OOTB-afbeeldingscomponent.)

![](images/uuid.png)

Nadat u de UUID hebt ingeschakeld, moet u zien dat het gegevenselement &#39;data-asset-id&#39; wordt gevuld met de UUID van het element. Analytics houdt de elementklik of de indruk bij met deze UUID.

![](images/uuid-code.png)

## Extensiegebruik

Deze extensie heeft twee gebeurtenissen en één actie.

* **Op element geklikt:** Een  __ gebeurtenis die wordt geactiveerd wanneer de bezoeker een AEM Asset selecteert dat is ingeschakeld voor tracering en een bestemming heeft (href-kenmerk).

* **Op element geklikt (geen bestemming):** Een  __ gebeurtenis die wordt geactiveerd wanneer de bezoeker een AEM element selecteert dat is ingeschakeld voor tracering en geen bestemming heeft (geen href-kenmerk).

* **AA-variabelen instellen:** een  __ handeling waarmee de voor AEM Assets gereserveerde variabelen voor Analytics (context data variables  `a.assets.source`,  `a.assets.idlist` en  `a.asset.clickedid`) worden ingesteld, afhankelijk van welke gebeurtenis is gebruikt en hoe de gebeurtenis en handeling zijn geconfigureerd. Voor deze extensie worden geen Analytics-gebeurtenissen, props of eVars gebruikt.

### Asset-impressies

Voeg de handeling &quot;AA-variabelen instellen&quot; toe aan een nieuwe of bestaande labelregel die op elke pagina wordt geactiveerd en een verzoek voor een analytische afbeelding verzendt. De actie &quot;Stel AA-variabelen in&quot; moet **voor** de actie &quot;Adobe Analytics - Send Beacon&quot; worden weergegeven. U kunt desgewenst aanvullende acties toevoegen.

Selecteer in de configuratiepagina **[AA-variabelen instellen]** de optie **[Weergegeven elementen]** (standaard). Hiermee wordt alleen de gebeurtenis Impressions ingesteld voor elementen die daadwerkelijk door de bezoeker worden gezien.

>[!NOTE]
>
>Hoewel niet aanbevolen, biedt de actie &quot;AA-variabelen instellen&quot; ook ondersteuning voor een &quot;geladen&quot; optie, die voor elk element op de pagina elementindrukkingen verzendt, ongeacht of de bezoeker deze heeft gezien of niet.

![Impressies](images/sendImpressions.jpg)


### Elementklikken

Configureer een tweede regel met behulp van de gebeurtenis &quot;Asset Clicked&quot; en de actie &quot;Set AA Variables&quot;. De gebeurtenis &quot;Asset Clicked&quot; moet zo worden geconfigureerd dat &quot;Asset Clicked image request&quot; is ingesteld op &quot;On PageLoad&quot; (standaardwaarde). Deze regel vereist geen Adobe Analytics-handelingen (zoals Verzenden van baken) omdat de element-id wordt opgeslagen in `sessionStorage` en verzonden door de volgende regel voor impressies.

De gebeurtenis &quot;Asset Clicked&quot; ondersteunt ook de instelling &quot;On Click&quot; voor het aanvragen van afbeeldingen waarop wordt geklikt. Dit verzendt klikmetrisch naar Analytics onmiddellijk en vereist ook de &quot;Send Beacon&quot;actie van Analytics.

![Elementklikken bij laden van pagina](images/sendClickOnPageload.jpg)

Vorm een derde regel die zal in brand steken wanneer er Activa op de pagina&#39;s zijn die geen bestemming (geen `href` attribuut) hebben. Op zijn minst moet de nieuwe regel de gebeurtenis &quot;Asset Clicked (No Destination)&quot; en de acties &quot;Set AA Variables&quot; en &quot;Adobe Analytics - Send Beacon&quot; gebruiken. Er kunnen desgewenst aanvullende voorwaarden en handelingen worden toegevoegd.

![Asset Kliks op geen bestemming](images/sendClickOnClickNoDestination.jpg)

### Tips voor het testen van extensies

Vorm drie Regels zoals hierboven beschreven:

* Impressies van elementen
* Elementklikken
* Elementklikken zonder bestemming

**Impressies**

1. Navigeer naar een pagina die AEM elementen bevat.

1. Als er geen elementen zichtbaar zijn in de browser, bladert u totdat u minstens één element ziet en selecteert u dat element, of navigeert u gewoon naar een andere pagina.

1. Bekijk het verzoek voor Analytics-afbeeldingen.

   Als `a.assets.idlist` de Activum-id&#39;s bevat die op de vorige pagina zichtbaar waren, werkt de regel correct.

   Als `a.assets.idlist` niet in het beeldverzoek is, is het hoogstwaarschijnlijk één van twee redenen:

   * Er is nooit een element gevonden in het weergavegebied van de browser

   * Er waren geen activa op de pagina die met [Inzicht van Activa ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) in AEM wordt gevormd toegelaten.

**Klikken**

1. Navigeer naar een pagina die AEM elementen bevat.

1. Selecteer een van de elementen.

Als `a.assets.idlist` op de doelpagina de element-id&#39;s heeft en `a.assets.clickedid` de element-id heeft van het element dat op de startpagina is geselecteerd, werkt de regel correct in de resulterende afbeeldingsaanvraag Analytics (van de volgende pagina).

Als `a.assets.clickedid` niet in het beeldverzoek is, is het meestal waarschijnlijk omdat het geselecteerde element [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) niet heeft ingeschakeld in AEM.

**Klikken zonder bestemming**

1. Navigeer naar een pagina die minstens één AEM element bevat dat geen doel heeft (geen `href` kenmerk).

1. Selecteer dat element.

Als `a.assets.clickedid` in het resulterende verzoek voor Analytics-afbeeldingen de Asset ID heeft, werkt de regel correct.

Als `a.assets.clickedid` niet in het beeldverzoek is, is het meestal waarschijnlijk omdat het geselecteerde element [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) niet heeft ingeschakeld in AEM.
