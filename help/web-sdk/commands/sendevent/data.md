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

De `data` kunt u een payload naar een Adobe verzenden die niet overeenkomt met een XDM-schema. Het is handig in niet-XDM-scenario&#39;s, zoals het rechtstreeks verzenden van gegevens naar Adobe Analytics, Adobe Target of Adobe Audience Manager. Wanneer gegevens bij de gegevensstroom aankomen, kunt u [Toewijzing van gegevensvoorvoegsel](/help/data-prep/ui/mapping.md) XDM-velden toewijzen aan elk veld in het dialoogvenster `data` object.

>[!IMPORTANT]
>
>Gegevens binnen dit object moeten ten minste een van de volgende handelingen hebben:
>
>* De dienst in de gegevensstroom moet worden gevormd om gegevens van een bepaald bezit in terug te winnen `data` object.
>* De opgegeven eigenschap moet aan een XDM-veld worden toegewezen met behulp van data prep.
>
>Als een bepaald bezit niet aan een XDM gebied in kaart wordt gebracht of door de gevormde dienst wordt gebruikt, wordt dat gegeven permanent verloren.

## Gebruik de `data` object via de Web SDK-tagextensie {#tag-extension}

Geef een gegevenselement op in het dialoogvenster **[!UICONTROL Data]** binnen de acties van een labelregel.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. Geef het gegevenselement op dat het gewenste object bevat in het dialoogvenster **[!UICONTROL Data]** veld.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Gebruik de `data` object via de Web SDK JavaScript-bibliotheek {#library}

Stel de `data` object als onderdeel van het JSON-object binnen de parameter van het object `sendEvent` gebruiken. Voor gegevens die u wilt toewijzen in de gegevensstroom, kunt u dit object structureren op de manier die u wilt. Voor gegevens die door bepaalde diensten worden gebruikt, zorg ervoor dat de objecten hiërarchie aanpast wat de dienst verwacht. U kunt beide opties opnemen `data` en de [`xdm`](xdm.md) object in hetzelfde `sendEvent` gebruiken.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Gebruik de `data` object met Adobe Analytics {#analytics}

U kunt de `data` -object met Adobe Analytics om gegevens naar een rapportsuite zonder een XDM-schema te verzenden. Variabelen zijn geconfigureerd om dezelfde syntaxis te gebruiken als [!DNL AppMeasurement] variabelen, die het verbeteringsproces aan het Web SDK vereenvoudigen. Zie [Gegevensobjectvariabele toewijzen aan Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) in de Adobe Analytics-implementatiegids voor meer informatie.
