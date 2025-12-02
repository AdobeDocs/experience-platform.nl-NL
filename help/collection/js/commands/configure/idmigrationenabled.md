---
title: idMigrationEnabled
description: Hiermee kan de Web SDK AMCV-cookies lezen.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

Met de eigenschap `idMigrationEnabled` kan de Web SDK AMCV-cookies lezen die zijn ingesteld door eerdere Adobe Experience Cloud-implementaties. Als uw organisatie uw implementatie aan het Web SDK bevordert, staat dit het plaatsen een vlottere overgang aan de huidige dienst van identiteitskaart van Adobe Experience Cloud toe. Deze instelling is waardevol, zodat u geen sterke toename ziet van unieke bezoekers wanneer u een upgrade uitvoert naar de Web SDK.

Als uw organisatie een nieuwe implementatie van SDK van het Web in werking stelt, heeft het toelaten van dit plaatsen geen invloed op gegevensinzameling of bezoekersidentificatie. Er zijn geen nadelen om het voor alle implementaties toe te laten.

Stel de Booleaanse waarde `idMigrationEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze eigenschap in als u de mogelijkheid wilt uitschakelen om AMCV-cookies te lezen die zijn ingesteld door de Bezoeker-API. De meeste organisaties hoeven dit bezit niet te plaatsen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Migratie van bezoekersidentiteitskaart inschakelen met de Web SDK-tagextensie

Deze montages kunnen in de de markeringsuitbreiding van SDK van het Web worden gevormd gebruikend [ de configuratiemontages van de Identiteit ](/help/tags/extensions/client/web-sdk/configure/identity.md).
