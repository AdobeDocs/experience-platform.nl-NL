---
title: data
description: Leer hoe te om niet-XDM gegevens naar Adobe, door het gegevensvoorwerp te verzenden.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# `data`

Met het `data` -object kunt u een payload naar een Adobe verzenden die niet overeenkomt met een XDM-schema. Het is handig in niet-XDM-scenario&#39;s, zoals het rechtstreeks verzenden van gegevens naar Adobe Analytics, Adobe Target of Adobe Audience Manager. Wanneer de gegevens bij de gegevensstroom aankomen, kunt u [&#x200B; Afbeelding van de Prep van Gegevens gebruiken &#x200B;](/help/data-prep/ui/mapping.md) om gebieden XDM aan elk gebied in het `data` voorwerp toe te wijzen.

>[!IMPORTANT]
>
>Gegevens binnen dit object moeten ten minste een van de volgende handelingen hebben:
>
>* Een service in de gegevensstroom moet zijn geconfigureerd om gegevens op te halen uit een bepaalde eigenschap in het `data` -object.
>* De opgegeven eigenschap moet aan een XDM-veld worden toegewezen met behulp van data prep.
>
>Als een bepaald bezit niet aan een XDM gebied in kaart wordt gebracht of door de gevormde dienst wordt gebruikt, wordt dat gegeven permanent verloren.

## Gebruik het object `data` via de extensie van de Web SDK-tag {#tag-extension}

Geef een gegevenselement op in het veld **[!UICONTROL Data]** binnen de handelingen van een labelregel.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Send event]** .
1. Geef het gegevenselement met het gewenste object op in het veld **[!UICONTROL Data]** .
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

## Het object `data` gebruiken via de Web SDK JavaScript-bibliotheek {#library}

Stel het `data` -object in als onderdeel van het JSON-object binnen de parameter van de opdracht `sendEvent` . Voor gegevens die u wilt toewijzen in de gegevensstroom, kunt u dit object structureren op de manier die u wilt. Voor gegevens die door bepaalde diensten worden gebruikt, zorg ervoor dat de objecten hiërarchie aanpast wat de dienst verwacht. U kunt zowel het object `data` als het object [`xdm`](xdm.md) in dezelfde opdracht `sendEvent` opnemen.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Het object `data` gebruiken met Adobe Analytics {#analytics}

U kunt het `data` -object met Adobe Analytics gebruiken om gegevens naar een rapportsuite zonder een XDM-schema te verzenden. Variabelen zijn geconfigureerd om dezelfde syntaxis te gebruiken als [!DNL AppMeasurement] variabelen, waardoor het upgradeproces naar de SDK van het web wordt vereenvoudigd. Zie [&#x200B; objecten van Gegevens veranderlijke afbeelding aan Adobe Analytics &#x200B;](https://experienceleague.adobe.com/nl/docs/analytics/implementation/aep-edge/data-var-mapping) in de de implementatiegids van Adobe Analytics voor meer informatie.
