---
title: Overzicht van de extensie Asset Insights AEM
description: Meer informatie over de tagextensie AEM Asset Insights in Adobe Experience Platform.
exl-id: 7d3edd42-09fe-4e40-93dc-1edd2fdbb121
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 0%

---

# Overzicht van de extensie Asset Insights AEM

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Deze extensie is bedoeld voor gebruik in combinatie met [Asset Insights AEM](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html). Meer bepaald vervangt deze code het proces pageTracker en sluit deze in. Als deze extensie is geconfigureerd, verzendt deze Asset *Impressie* en *Klikken* metriek naar Adobe Analytics, waarna deze worden geïmporteerd in de rapporten AEM Asset Insights. De gegevens van de activa kunnen dan worden gerapporteerd door of AEM Inzichten van Activa of de Werkruimten van het Project van Adobe Analytics te gebruiken.

## Voorwaarden voor extensies

### Analytics

De rapporten AEM Asset in Analytics bevatten drie AEM:

* Element-id
* Middelbron
* Element geklikt

Er zijn ook twee meetwaarden:
* Impressies van elementen
* Elementklikken.

Deze rapporten moeten worden toegelaten gebruikend de Beheerder van de Analyse (uitgezocht **[!UICONTROL Analytics]> [!UICONTROL Admin] > [!UICONTROL Report Suites] > `<report suite>` > [!UICONTROL Edit Settings] > [!UICONTROL AEM] >[!UICONTROL AEM Assets Reporting]**) voordat ze kunnen worden gevuld met deze extensie.

De &quot;*Adobe Analytics*&quot;-tagextensie voor Adobe Experience Platform moet in dezelfde webeigenschap worden geïnstalleerd.

### Adobe Experience Manager (AEM)

1. Inschakelen [Asset Insights AEM](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html). Selecteer in AEM **[!UICONTROL Tools > Assets]** en open vervolgens de **[!UICONTROL Insights Configuration]** deelvenster.

1. UUID-tracking uitschakelen.

   >[!IMPORTANT]
   >
   >Deze extensie zal *niet* functie als de configuratie-instelling voor AEM element **[!UICONTROL Disable UUID Tracking]** is ingeschakeld. Deze optie is standaard uitgeschakeld.

   ![UUID-tracking uitschakelen](images/disableassets.jpg)

## Adobe Experience Manager configureren (AEM)

In deze sectie wordt beschreven hoe u AEM kunt configureren met tags in Adobe Experience Platform, hoe u Asset Insight kunt inschakelen in AEM en hoe u het bijhouden van UID-codes kunt inschakelen voor elementen.

### AEM integreren met tags

De aanbevolen integratie van [Platform](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) met Adobe Experience Manager wordt gedaan via Adobe I/O.

1. [AEM met tags verbinden met Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

2. [Een Adobe Experience Platform Cloud Service-configuratie maken](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/create-launch-cloud-service.html).

### Asset Insight inschakelen in AEM

Raadpleeg voor instructies over het inschakelen van Asset Insights de [Experience Manager 6.5 Gebruikershandleiding voor middelen](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html).

### UUID-tracking inschakelen voor middelen

Elementen bijhouden in Analytics met behulp van de UUID van het element in AEM.

Om het volgen met UUID van de activa toe te laten, open de console van het componentenbeleid van het editable malplaatje en uncheck het &quot;UUID het volgen&quot;bezit onbruikbaar maken. (Deze eigenschap wordt standaard gecontroleerd op de OOTB-afbeeldingscomponent.)

![](images/uuid.png)

Nadat u de UUID hebt ingeschakeld, moet u zien dat het gegevenselement &#39;data-asset-id&#39; wordt gevuld met de UUID van het element. Analytics houdt de elementklik of de indruk bij met deze UUID.

![](images/uuid-code.png)

## Extensiegebruik

Deze extensie heeft twee gebeurtenissen en één actie.

* **Op element geklikt:** An _event_ die wordt geactiveerd wanneer de bezoeker een AEM Asset selecteert die is ingeschakeld voor tracering en een bestemming heeft (href-kenmerk).

* **Op element geklikt (geen bestemming):** An _event_ die wordt geactiveerd wanneer de bezoeker een AEM Asset selecteert die is ingeschakeld voor tracering en geen bestemming heeft (geen href-kenmerk).

* **AA-variabelen instellen:** An _action_ waarmee de variabelen voor Analytics worden ingesteld die zijn gereserveerd voor AEM Assets (context data variables) `a.assets.source`, `a.assets.idlist` en `a.asset.clickedid`), afhankelijk van welke gebeurtenis is gebruikt en hoe de gebeurtenis en handeling zijn geconfigureerd. Voor deze extensie worden geen Analytics-gebeurtenissen, props of eVars gebruikt.

### Asset-impressies

Voeg de handeling &quot;AA-variabelen instellen&quot; toe aan een nieuwe of bestaande labelregel die op elke pagina wordt geactiveerd en een verzoek voor een analytische afbeelding verzendt. De handeling &quot;Een variabele instellen&quot; moet worden weergegeven **voor** de actie &quot;Adobe Analytics - Send Beacon&quot;. U kunt desgewenst aanvullende acties toevoegen.

In de **[AA-variabelen instellen]** config pagina, selecteer **[Weergegeven elementen]** (standaard). Hiermee wordt alleen de gebeurtenis Impressions ingesteld voor elementen die daadwerkelijk door de bezoeker worden gezien.

>[!NOTE]
>
>Hoewel niet aanbevolen, biedt de actie &quot;AA-variabelen instellen&quot; ook ondersteuning voor een &quot;geladen&quot; optie, die voor elk element op de pagina elementindrukkingen verzendt, ongeacht of de bezoeker deze heeft gezien of niet.

![Impressies](images/sendImpressions.jpg)


### Elementklikken

Configureer een tweede regel met behulp van de gebeurtenis &quot;Asset Clicked&quot; en de actie &quot;Set AA Variables&quot;. De gebeurtenis &quot;Asset Clicked&quot; moet zo worden geconfigureerd dat &quot;Asset Clicked image request&quot; is ingesteld op &quot;On PageLoad&quot; (standaardwaarde). Voor deze regel zijn geen Adobe Analytics-handelingen vereist (zoals Verzendbaken) omdat de id van het element wordt opgeslagen in `sessionStorage` en verzonden door de volgende regel Impressies.

De gebeurtenis &quot;Asset Clicked&quot; ondersteunt ook de instelling &quot;On Click&quot; voor het aanvragen van afbeeldingen waarop wordt geklikt. Dit verzendt klikmetrisch naar Analytics onmiddellijk en vereist ook de &quot;Send Beacon&quot;actie van Analytics.

![Elementklikken bij laden van pagina](images/sendClickOnPageload.jpg)

Configureer een derde regel die wordt geactiveerd wanneer er middelen op de pagina&#39;s staan die geen doel hebben (geen `href` kenmerk). Op zijn minst moet de nieuwe regel de gebeurtenis &quot;Asset Clicked (No Destination)&quot; en de acties &quot;Set AA Variables&quot; en &quot;Adobe Analytics - Send Beacon&quot; gebruiken. Er kunnen desgewenst aanvullende voorwaarden en handelingen worden toegevoegd.

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

   Indien `a.assets.idlist` bevat de element-id&#39;s die op de vorige pagina zichtbaar waren, werkt de regel correct.

   Indien `a.assets.idlist` bevindt zich niet in het afbeeldingsverzoek, maar is waarschijnlijk een van de volgende twee redenen:

   * Er is nooit een element gevonden in het weergavegebied van de browser

   * Er zijn geen elementen op de pagina geconfigureerd met [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) ingeschakeld in AEM.

**Klikken**

1. Navigeer naar een pagina die AEM elementen bevat.

1. Selecteer een van de elementen.

In de resulterende Analytics-afbeeldingsaanvraag (van de volgende pagina), als `a.assets.idlist` bevat de element-id&#39;s op de doelpagina en `a.assets.clickedid` met de element-id van het element dat op de pagina van oorsprong is geselecteerd, werkt de regel correct.

Indien `a.assets.clickedid` niet in de aanvraag voor de afbeelding staat, is deze meestal waarschijnlijk omdat het geselecteerde element niet [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) ingeschakeld in AEM.

**Klikken zonder bestemming**

1. Navigeer naar een pagina die minstens één AEM element bevat dat geen doel heeft (geen `href` kenmerk).

1. Selecteer dat element.

In het resulterende analyseverzoek, als `a.assets.clickedid` heeft de element-id, de regel werkt correct.

Indien `a.assets.clickedid` niet in de aanvraag voor de afbeelding staat, is deze meestal waarschijnlijk omdat het geselecteerde element niet [Asset Insights](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) ingeschakeld in AEM.
