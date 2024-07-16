---
title: Gegevenstype Advertising Details Collection
description: Meer informatie over het gegevenstype Advertising Details Collection Experience Data Model (XDM).
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!UICONTROL Advertising Details] Gegevenstype verzameling

[!UICONTROL Advertising Details] Verzameling is een standaard XDM-gegevenstype (Experience Data Model) waarmee de belangrijkste kenmerken van advertenties worden vastgelegd. Het bevat informatie zoals de advertentie-id, adverteerder en campagne-id&#39;s, lengte, positie binnen een reeks, details over de speler die de advertentie rendert, enzovoort. U kunt dit gegevenstype gebruiken om verschillende aspecten van de prestaties en betrokkenheid van advertenties te volgen en te analyseren, en inzichten te verschaffen in de interactie van het publiek met en de reactie op verschillende advertenties. Deze gegevens worden gebruikt om uw streaminggegevens bij te houden.

+++Select om een diagram van het gegevenstype van de Verzameling van Details van Advertising te tonen.
![ A diagram van het gegevenstype van de Inzameling van de Details van Advertising.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Elke weergavenaam bevat een koppeling naar meer informatie over de audio- en videoparameters. De gekoppelde pagina&#39;s bevatten gegevens over de video en gegevens die worden verzameld door Adobe, implementatiewaarden, netwerkparameters, rapportage en belangrijke overwegingen.

| Weergavenaam | Eigenschap | Gegevenstype | Vereist | Beschrijving |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Ad Advertiser]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | string | Nee | De onderneming of het merk waarvan het product in de advertentie wordt vermeld. |
| [[!UICONTROL Ad Campaign]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | string | Nee | De id van de advertentiecampagne. |
| [[!UICONTROL Ad Creative ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | string | Nee | De id van de advertentie. |
| [[!UICONTROL Ad Creative URL]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | string | Nee | De URL van de advertentie. |
| [[!UICONTROL Ad In Pod Position (Ad Start)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | integer | Ja | De index van de advertentie binnen de bovenliggende en bovenliggende advertentie, bijvoorbeeld de eerste advertentie, heeft index 0 en de tweede advertentie index 1. |
| [[!UICONTROL Ad Length Or Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | integer | Ja | De lengte van de videodemo in seconden. |
| [[!UICONTROL Ad Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | string | Ja | De leesbare naam van de advertentie. Bij de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de eVar. |
| [[!UICONTROL Ad Placement ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | string | Nee | De plaatsing-id van de advertentie. |
| [[!UICONTROL Ad Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | string | Ja | De naam van de speler die verantwoordelijk is voor het renderen van de advertentie. |
| [[!UICONTROL Ad Site ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | string | Nee | De id van de advertentiesite. |
