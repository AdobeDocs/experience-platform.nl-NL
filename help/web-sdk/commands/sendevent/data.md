---
title: data
description: Leer hoe u niet-XDM-gegevens naar de Adobe verzendt.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# data

De `data` staat u toe om gegevens naar Adobe te verzenden die geen XDM schema aanpast. Het is nuttig in niet-XDM scenario&#39;s, zoals het bijwerken van en [Adobe Target-profiel](/help/web-sdk/personalization/adobe-target/target-overview.md). Wanneer gegevens bij Adobe aankomen, kunt u het hulpmiddel van de gegevenstoewijzing gebruiken om XDM gebieden aan elk gebied in toe te wijzen `data` eigenschap.

>[!IMPORTANT]
>
>Gegevens binnen deze eigenschap moeten ten minste een van de volgende handelingen hebben:
>
>* De dienst in de gegevensstroom moet worden gevormd om gegevens van een specifiek bezit in terug te winnen `data` object
>* Elke eigenschap moet worden toegewezen aan een XDM-veld
>
>Als een bepaald gebied niet aan een XDM gebied in kaart wordt gebracht of door de gevormde dienst wordt gebruikt, wordt dat gegeven permanent verloren.

## Gebruik het gegevensbezit gebruikend de de markeringsuitbreiding van SDK van het Web

Geef een gegevenselement op in het dialoogvenster **[!UICONTROL Data]** binnen de acties van een labelregel.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Send event]**.
1. Geef het gegevenselement op dat het gewenste object bevat in het dialoogvenster **[!UICONTROL Data]** veld.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## De eigenschap data gebruiken met de Web SDK JavaScript-bibliotheek

Stel de `data` eigenschap als onderdeel van het JSON-object binnen de parameter van het object `sendEvent` gebruiken. Voor gegevens die u in de gegevensstroom wilt toewijzen, kunt u deze eigenschap structureren op een manier die u wilt. Voor gegevens die door bepaalde diensten worden gebruikt, zorg ervoor dat de objecten hiërarchie aanpast wat de dienst verwacht. U kunt beide opties opnemen `data` en de [`xdm`](xdm.md) object in hetzelfde `sendEvent` gebruiken.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
