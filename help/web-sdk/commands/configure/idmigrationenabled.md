---
title: idMigrationEnabled
description: Hiermee kan de Web SDK AMCV-cookies lezen.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# `idMigrationEnabled`

Met de eigenschap `idMigrationEnabled` kan de Web SDK AMCV-cookies lezen die zijn ingesteld door eerdere Adobe Experience Cloud-implementaties. Als uw organisatie uw implementatie aan de SDK van het Web bevordert, staat dit het plaatsen een vlottere overgang aan de huidige dienst van identiteitskaart van Adobe Experience Cloud toe. Deze instelling is waardevol, zodat u geen sterke toename ziet van unieke bezoekers wanneer u een upgrade uitvoert naar de SDK van het web.

Als uw organisatie een nieuwe implementatie van SDK van het Web in werking stelt, heeft het toelaten van dit plaatsen geen invloed op gegevensinzameling of bezoekersidentificatie. Er zijn geen nadelen om het voor alle implementaties toe te laten.

## ID-migratie inschakelen met de Web SDK-tagextensie

Selecteer **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]** checkbox wanneer [ het vormen van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Zoek de sectie [!UICONTROL Identity] en selecteer vervolgens het selectievakje **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]** .
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## ID-migratie inschakelen met de Web SDK JavaScript-bibliotheek

Stel de Booleaanse waarde `idMigrationEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze eigenschap in als u de mogelijkheid wilt uitschakelen om AMCV-cookies te lezen die zijn ingesteld door de Bezoeker-API. De meeste organisaties hoeven dit bezit niet te plaatsen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
