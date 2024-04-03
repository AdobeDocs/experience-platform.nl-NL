---
title: Advertentiegegevens Rapportage Gegevenstype
description: Meer informatie over het gegevenstype Advertising Details Reporting Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# [!UICONTROL Advertising Details] Gegevenstype rapporteren

[!UICONTROL Advertising Details] Rapportage is een standaard XDM-gegevenstype (Experience Data Model) waarmee belangrijke kenmerken met betrekking tot advertenties worden vastgelegd. Het bevat informatie zoals de advertentie-id, adverteerder en campagne-id&#39;s, lengte, positie binnen een reeks, details over de speler die de advertentie rendert, enzovoort. U kunt dit gegevenstype gebruiken om verschillende aspecten van de prestaties en betrokkenheid van advertenties te volgen en te analyseren, en inzichten te verschaffen in de interactie van het publiek met en de reactie op verschillende advertenties.

+++Selecteer om een diagram van het gegevenstype Rapportage van advertentiedetails weer te geven.
![Een diagram van het gegevenstype Rapportage van advertentiegegevens.](../images/data-types/advertising-details-information.png)
+++

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Ad Name] | `friendlyName` | string | De leesbare naam van de advertentie. Bij de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de eVar. |
| [!UICONTROL Ad ID] | `name` | string | De id van de advertentie. Een geheel getal en/of lettercombinatie. |
| [!UICONTROL Ad Length Or Duration] | `length` | integer | De lengte van de videodemo in seconden. |
| [!UICONTROL Ad In Pod Position (Ad Start)] | `podPosition` | integer | De index van de advertentie binnen de bovenliggende en bovenliggende advertentie, bijvoorbeeld de eerste advertentie, heeft index 0 en de tweede advertentie index 1. |
| [!UICONTROL Ad Player Name] | `playerName` | string | De naam van de speler die verantwoordelijk is voor het renderen van de advertentie. |
| [!UICONTROL Ad Advertiser] | `advertiser` | string | De onderneming of het merk waarvan het product in de advertentie wordt vermeld. |
| [!UICONTROL Ad Campaign] | `campaignID` | string | De id van de advertentiecampagne. |
| [!UICONTROL Ad Creative ID] | `creativeID` | string | De id van de advertentie. |
| [!UICONTROL Ad Site ID] | `siteID` | string | De id van de advertentiesite. |
| [!UICONTROL Ad Creative URL] | `creativeURL` | string | De URL van de advertentie. |
| [!UICONTROL Ad Placement ID] | `placementID` | string | De plaatsing-id van de advertentie. |
| [!UICONTROL Ad Completed] | `isCompleted` | boolean | Traceert of de advertentie is voltooid. |
| [!UICONTROL Ad Started] | `isStarted` | boolean | Houdt bij of de advertentie is gestart. |
| [!UICONTROL Ad Time Played] | `timePlayed` | integer | De totale hoeveelheid tijd, in seconden, die wordt besteed aan het bekijken van de advertentie (dat wil zeggen, het aantal seconden dat wordt afgespeeld). |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
