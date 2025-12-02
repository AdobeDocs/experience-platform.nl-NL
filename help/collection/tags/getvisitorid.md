---
title: getVisitorId
description: Haal de Experience Cloud Visitor ID service tag extension instance op.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# `getVisitorId()`

De `_satellite.getVisitorId()` methode keert een geval van de [&#x200B; dienst van identiteitskaart van Adobe Experience Cloud &#x200B;](https://experienceleague.adobe.com/en/docs/id-service/using/home) binnen uw markeringsbezit terug, **als** u de geïnstalleerde en gepubliceerde de dienstuitbreiding van identiteitskaart hebt. Deze methode is nuttig wanneer u directe toegang tot de instantie van bezoekersidentiteitskaart voor gebruik in de blokken van de douanecode, de geavanceerde configuratie van het gegevenselement, of de kwesties van de het oplossen van problemenidentiteit van de bezoeker wilt.

>[!IMPORTANT]
>
>Deze methode is alleen van toepassing op eigenschappen die de zelfstandige extensie van Experience Cloud ID-servicetag bevatten. Het is niet op de impliciete de dienstmogelijkheden van identiteitskaart beschikbaar in de de markeringsuitbreiding van SDK van het Web van toepassing. Zie de opdracht [`getIdentity`](/help/collection/js/commands/getidentity.md) als u een bezoekersidentiteit wilt ophalen met behulp van de impliciete id-servicemogelijkheden van Web SDK.

Als u deze methode met de geïnstalleerde en gepubliceerde de dienstuitbreiding van identiteitskaart roept, is een voorwerp teruggekeerd gelijkaardig aan het voorwerp dat na het roepen van de [`Visitor.getInstance()` wordt verkregen &#x200B;](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/getinstance) methode. Als u deze methode aanroept wanneer de id-service-extensie niet is geïnstalleerd of gepubliceerd, retourneert de methode `null` .

```ts
_satellite.getVisitorId(): Visitor | null
```

## Beschikbare velden en methoden

Zie de dienst van Experience Cloud identiteitskaart [&#x200B; Methoden &#x200B;](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/get-set) in de de dienstdocumentatie van identiteitskaart van de Bezoeker van Experience Cloud om te zien welke gebieden en methodes aan u beschikbaar zijn.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
