---
title: data
description: Leer hoe u niet-XDM-gegevens via het gegevensobject naar Adobe verzendt.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

Met het `data` -object kunt u een payload naar Adobe verzenden die niet overeenkomt met een XDM-schema. Het is handig in niet-XDM-scenario&#39;s, zoals het rechtstreeks verzenden van gegevens naar Adobe Analytics, Adobe Target of Adobe Audience Manager. Wanneer de gegevens bij de gegevensstroom aankomen, kunt u [ Afbeelding van de Prep van Gegevens gebruiken ](/help/data-prep/ui/mapping.md) om gebieden XDM aan elk gebied in het `data` voorwerp toe te wijzen. Als Adobe al een product heeft geconfigureerd om velden binnen het `data` -object te detecteren, kunt u die gegevens ongewijzigd naar een gegevensstroom verzenden.

>[!IMPORTANT]
>
>Gegevens binnen dit object moeten ten minste een van de volgende handelingen hebben:
>
>* Een service in de gegevensstroom moet zijn geconfigureerd om gegevens op te halen uit een bepaalde eigenschap in het `data` -object.
>* De opgegeven eigenschap moet aan een XDM-veld worden toegewezen met behulp van data prep.
>
>Als een bepaald bezit niet aan een XDM gebied in kaart wordt gebracht of door de gevormde dienst wordt gebruikt, wordt dat gegeven permanent verloren.

Stel het `data` -object in als onderdeel van het JSON-object binnen de parameter van de opdracht `sendEvent` . Voor gegevens die u wilt toewijzen in de gegevensstroom, kunt u dit object structureren op de manier die u wilt. Voor gegevens die door bepaalde diensten worden gebruikt, zorg ervoor dat de objecten hiërarchie aanpast wat de dienst verwacht. U kunt zowel het object `data` als het object [`xdm`](xdm.md) in dezelfde opdracht `sendEvent` opnemen.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Het object `data` gebruiken met Adobe Analytics {#analytics}

U kunt het `data` -object met Adobe Analytics gebruiken om gegevens naar een rapportsuite zonder een XDM-schema te verzenden. Variabelen zijn geconfigureerd om dezelfde syntaxis te gebruiken als AppMeasurement-variabelen, waardoor het upgradeproces naar het web SDK wordt vereenvoudigd. Zie [ objecten van Gegevens veranderlijke afbeelding aan Adobe Analytics ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) in de de implementatiegids van Adobe Analytics voor meer informatie.

## Het `data` -object gebruiken met de extensie van de Web SDK-tag

Het `data` voorwerp is beschikbaar als a [ Variabel gegevenselement ](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) wanneer het gebruiken van de de markeringsuitbreiding van SDK van het Web.
