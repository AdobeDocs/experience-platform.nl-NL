---
title: idMigrationEnabled
description: Hiermee kan de Web SDK AMCV-cookies lezen.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# `idMigrationEnabled`

De `idMigrationEnabled` staat de Web SDK toe om de koekjes te lezen AMCV die door vorige implementaties van Adobe Experience Cloud worden geplaatst. Als uw organisatie uw implementatie aan de SDK van het Web bevordert, staat dit het plaatsen een vlottere overgang aan de huidige dienst van identiteitskaart van Adobe Experience Cloud toe. Deze instelling is waardevol, zodat u geen sterke toename ziet van unieke bezoekers wanneer u een upgrade uitvoert naar de SDK van het web.

Als uw organisatie een nieuwe implementatie van SDK van het Web in werking stelt, heeft het toelaten van dit plaatsen geen invloed op gegevensinzameling of bezoekersidentificatie. Er zijn geen nadelen om het voor alle implementaties toe te laten.

## ID-migratie inschakelen met de Web SDK-tagextensie

Selecteer de **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]** selectievakje wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Zoek de [!UICONTROL Identity] en selecteert u vervolgens het selectievakje **[!UICONTROL Migrate ECID from VisitorAPI to the web SDK]**.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## ID-migratie inschakelen met de Web SDK JavaScript-bibliotheek

Stel de `idMigrationEnabled` boolean wanneer de `configure` gebruiken. Als u dit bezit weglaat wanneer het vormen van het Web SDK, blijft het in gebreke aan `true`. Stel deze eigenschap in als u de mogelijkheid wilt uitschakelen om AMCV-cookies te lezen die zijn ingesteld door de Bezoeker-API. De meeste organisaties hoeven dit bezit niet te plaatsen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
