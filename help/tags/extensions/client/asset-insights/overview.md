---
title: AEM Asset Insights Extension Overzicht
description: Meer informatie over de AEM Asset Insights-tagextensie in Adobe Experience Platform.
exl-id: 7d3edd42-09fe-4e40-93dc-1edd2fdbb121
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 4%

---

# AEM Asset Insights-extensie - overzicht

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor dataverzameling in Adobe Experience Platform.  Als gevolg hiervan zijn er verschillende terminologiewijzigingen in de productdocumentatie doorgevoerd. Raadpleeg het volgende [ document ](../../../term-updates.md) voor een geconsolideerde referentie van de terminologiewijzigingen.

Deze uitbreiding is bedoeld om samen met [ de Inzichten van het Activa van AEM ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) worden gebruikt. Meer bepaald vervangt deze code het proces pageTracker en sluit deze in. Wanneer gevormd, verzendt deze uitbreiding de Indrukking van Activa ** en *klikt* metriek aan Adobe Analytics, waarna zij in de rapporten van de Inzichten van de Activa van AEM zullen worden ingevoerd. De gegevens van de activa kunnen dan worden gemeld door of AEM Asset Insights of de Werkruimten van het Project van Adobe Analytics te gebruiken.

## Voorwaarden voor extensies

### Analytics

De AEM Asset-rapporten in Analytics bevatten drie AEM-dimensies:

* Element-id
* Source-element
* Op element geklikt

Er zijn ook twee meetwaarden:
* Impressies van elementen
* Elementklikken.

Deze rapporten moeten met de Beheerder van de Analyse worden toegelaten (selecteer **[!UICONTROL Analytics]> [!UICONTROL Admin] > [!UICONTROL Report Suites] > `<report suite>` > [!UICONTROL Edit Settings] > [!UICONTROL AEM] >[!UICONTROL AEM Assets Reporting]**) alvorens zij kunnen worden bevolkt gebruikend deze uitbreiding.

De &quot;*Adobe Analytics*&quot;markeringsuitbreiding voor Adobe Experience Platform moet in het zelfde Webbezit worden geïnstalleerd.

### Adobe Experience Manager (AEM)

1. Laat [ de Inzichten van Activa van AEM ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) toe. Selecteer **[!UICONTROL Tools > Assets]** in AEM en open vervolgens het deelvenster **[!UICONTROL Insights Configuration]** .

1. UUID-tracking uitschakelen.

   >[!IMPORTANT]
   >
   >Deze uitbreiding zal *niet* functioneren als het plaatsen van de configuratie van Activa van AEM **[!UICONTROL Disable UUID Tracking]** wordt gecontroleerd. Deze optie is standaard uitgeschakeld.

   ![ onbruikbaar maken het Volgen UUID ](images/disableassets.jpg)

## Adobe Experience Manager (AEM) configureren

In deze sectie wordt beschreven hoe u AEM kunt configureren met tags in Adobe Experience Platform, hoe u Asset Insight in AEM kunt inschakelen en hoe u UUID-tracking kunt inschakelen voor Assets.

### AEM integreren met tags

De geadviseerde integratie van [ Experience Platform ](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html) met Adobe Experience Manager wordt gedaan via Adobe I/O.

1. [ verbind AEM met markeringen gebruikend Adobe I/O ](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

2. [ creeer een configuratie van Adobe Experience Platform Cloud Service ](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/create-launch-cloud-service.html).

### Asset Insight inschakelen in AEM

Voor instructies bij het toelaten van de Inzichten van Activa, zie [ Experience Manager 6.5 de gebruikersgids van Assets ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html).

### UUID-tracking inschakelen voor Assets

Elementen bijhouden in Analytics met de UUID van het element in AEM.

Om het volgen met UUID van de activa toe te laten, open de console van het componentenbeleid van het editable malplaatje en uncheck het &quot;UUID het volgen&quot;bezit onbruikbaar maken. (Deze eigenschap wordt standaard gecontroleerd op de OOTB-afbeeldingscomponent.)

![](images/uuid.png)

Nadat u de UUID hebt ingeschakeld, moet u zien dat het gegevenselement &#39;data-asset-id&#39; wordt gevuld met de UUID van het element. Analytics houdt de elementklik of de indruk bij met deze UUID.

![](images/uuid-code.png)

## Extensiegebruik

Deze extensie heeft twee gebeurtenissen en één actie.

* **Geklikte Activa:** Een _gebeurtenis_ die brandt wanneer de bezoeker een Middel van AEM selecteert dat voor het volgen wordt toegelaten en een bestemming (href attribuut) heeft.

* **Geklikte Activa (Geen Bestemming):** Een _gebeurtenis_ die brandt wanneer de bezoeker een Activa van AEM selecteert die voor het volgen wordt toegelaten en geen bestemming (geen href attribuut) heeft.

* **plaats de Variabelen van A:** Een _actie_ die de variabelen van de Analyse die voor AEM Assets (de variabelen van contextgegevens `a.assets.source`, `a.assets.idlist` en `a.asset.clickedid`) worden gereserveerd afhankelijk van welke gebeurtenis werd gebruikt en hoe de gebeurtenis en de actie worden gevormd. Voor deze extensie worden geen Analytics-gebeurtenissen, props of eVars gebruikt.

### Asset-impressies

Voeg de handeling &quot;AA-variabelen instellen&quot; toe aan een nieuwe of bestaande labelregel die op elke pagina wordt geactiveerd en een verzoek voor een analytische afbeelding verzendt. De &quot;Reeks a Variabelen&quot;actie moet **vóór** &quot;Adobe Analytics - verzend Beacon&quot;actie verschijnen. U kunt desgewenst aanvullende acties toevoegen.

In de **[Vastgestelde a Veranderingen]** config pagina, selecteer **[Bekeken Assets]** (gebrek) optie. Hiermee wordt alleen de gebeurtenis Impressions ingesteld voor elementen die daadwerkelijk door de bezoeker worden gezien.

>[!NOTE]
>
>Hoewel niet aanbevolen, biedt de actie &quot;AA-variabelen instellen&quot; ook ondersteuning voor een &quot;geladen&quot; optie, die voor elk element op de pagina elementindrukkingen verzendt, ongeacht of de bezoeker deze heeft gezien of niet.

![ Impressies ](images/sendImpressions.jpg)


### Elementklikken

Configureer een tweede regel met behulp van de gebeurtenis &quot;Asset Clicked&quot; en de actie &quot;Set AA Variables&quot;. De gebeurtenis &quot;Asset Clicked&quot; moet zo worden geconfigureerd dat &quot;Asset Clicked image request&quot; is ingesteld op &quot;On PageLoad&quot; (standaardwaarde). Voor deze regel zijn geen Adobe Analytics-handelingen vereist (zoals Verzenden van baken) omdat de element-id wordt opgeslagen in `sessionStorage` en verzonden door de volgende regel voor impressies.

De gebeurtenis &quot;Asset Clicked&quot; ondersteunt ook de instelling &quot;On Click&quot; voor het aanvragen van afbeeldingen waarop wordt geklikt. Dit verzendt klikmetrisch naar Analytics onmiddellijk en vereist ook de &quot;Send Beacon&quot;actie van Analytics.

![ de Klikken van Activa op paginalading ](images/sendClickOnPageload.jpg)

Configureer een derde regel die wordt geactiveerd wanneer er Assets is op de pagina&#39;s die geen doel hebben (geen `href` -kenmerk). Op zijn minst moet de nieuwe regel de gebeurtenis &quot;Asset Clicked (No Destination)&quot; en de acties &quot;Set AA Variables&quot; en &quot;Adobe Analytics - Send Beacon&quot; gebruiken. Er kunnen desgewenst aanvullende voorwaarden en handelingen worden toegevoegd.

![ de Klikken van Activa op bestemming ](images/sendClickOnClickNoDestination.jpg)

### Tips voor het testen van extensies

Vorm drie Regels zoals hierboven beschreven:

* Impressies van elementen
* Elementklikken
* Elementklikken zonder bestemming

**Impressies**

1. Navigeer naar een pagina die AEM-elementen bevat.

1. Als er geen elementen zichtbaar zijn in de browser, bladert u totdat u minstens één element ziet en selecteert u dat element, of navigeert u gewoon naar een andere pagina.

1. Bekijk het verzoek voor Analytics-afbeeldingen.

   Als `a.assets.idlist` de element-id&#39;s bevat die op de vorige pagina zichtbaar waren, werkt de regel correct.

   Als `a.assets.idlist` niet in het beeldverzoek is, is het hoogstwaarschijnlijk één van twee redenen:

   * Er is nooit een element gevonden in het weergavegebied van de browser

   * Er waren geen activa op de pagina die met [ Inzichten van Activa ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) wordt gevormd die in AEM wordt toegelaten.

**klikken**

1. Navigeer naar een pagina die AEM-elementen bevat.

1. Selecteer een van de Assets.

Als `a.assets.idlist` in het resulterende verzoek om een analysebestand (van de volgende pagina) de element-id&#39;s op de doelpagina heeft en `a.assets.clickedid` de element-id heeft van het element dat op de startpagina is geselecteerd, werkt de regel correct.

Als `a.assets.clickedid` niet in het beeldverzoek is, is het meestal waarschijnlijk omdat het Activum dat werd geselecteerd niet [ Inzichten van Activa ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) toegelaten in AEM had.

**klikken zonder bestemming**

1. Navigeer naar een pagina die minstens één AEM-element bevat dat geen doel heeft (geen `href` -kenmerk).

1. Selecteer dat element.

Als `a.assets.clickedid` in de aanvraag voor de afbeelding Analytics de element-id heeft, werkt de regel correct.

Als `a.assets.clickedid` niet in het beeldverzoek is, is het meestal waarschijnlijk omdat de activa die werden geselecteerd niet [ Inzicht van Activa ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/touch-ui-configuring-asset-insights.html) hebben toegelaten in AEM.
