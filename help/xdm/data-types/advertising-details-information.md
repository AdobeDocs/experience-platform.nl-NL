---
title: Gegevenstype Advertentiedetails
description: Leer meer over het gegevenstype Advertising Details Information Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# [!UICONTROL Advertising Details Information] gegevenstype

[!UICONTROL Advertising Details Information] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat zeer belangrijke attributen met betrekking tot reclame vangt. Het bevat informatie zoals de advertentie-id, adverteerder en campagne-id&#39;s, lengte, positie binnen een reeks, details over de speler die de advertentie rendert, enzovoort. U kunt dit gegevenstype gebruiken om verschillende aspecten van de prestaties en betrokkenheid van advertenties te volgen en te analyseren, en inzichten te verschaffen in de interactie van het publiek met en de reactie op verschillende advertenties.

+++Selecteer om een diagram van het gegevenstype Reclamedetails weer te geven.
![Een diagram van het gegevenstype Reclamedetails.](../images/data-types/advertising-details-information.png)
+++

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|----------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Ad Name] | `friendlyName` | string | **Vereist** De leesbare naam van de advertentie. Bij de rapportage is &quot;Advertentienaam&quot; de classificatie en &quot;Advertentienaam (variabele)&quot; de eVar. |
| [!UICONTROL Ad ID] | `name` | string | De id van de advertentie. Een geheel getal en/of lettercombinatie. |
| [!UICONTROL Ad Length Or Duration] | `length` | integer | **Vereist** De lengte van de videodemo in seconden. |
| [!UICONTROL Ad In Pod Position (Ad Start)] | `podPosition` | integer | **Vereist** De index van de advertentie binnen de bovenliggende en bovenliggende advertentie, bijvoorbeeld de eerste advertentie, heeft index 0 en de tweede advertentie index 1. |
| [!UICONTROL Ad Player Name] | `playerName` | string | **Vereist** De naam van de speler die verantwoordelijk is voor het renderen van de advertentie. |
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
