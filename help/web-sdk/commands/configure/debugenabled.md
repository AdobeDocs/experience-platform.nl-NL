---
title: debugEnabled
description: Gebruik code om het zuiveren mogelijkheden in het Web SDK toe te laten.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

De `debugEnabled` staat u toe om het zuiveren toe te laten of onbruikbaar te maken gebruikend de code van SDK van het Web. Het is een van de beschikbare manieren om [foutopsporing](../../use-cases/debugging.md). Het inschakelen van foutopsporing binnen uw implementatie kan handiger zijn dan andere methoden tijdens de ontwikkeling van websites wanneer u foutopsporing altijd wilt inschakelen. Deze methode van het zuiveren laat het voor alle bezoekers toe, zodat wordt het niet geadviseerd voor productiepagina&#39;s.

Zie de [Foutopsporing](../../use-cases/debugging.md) gebruik case page voor meer manieren om het zuiveren toe te laten.

## Foutopsporing inschakelen met de Web SDK-tagextensie

Er zijn geen opties voor foutopsporing beschikbaar die native de SDK-tagextensie van Web gebruiken. Een [alternatieve foutopsporingsmethode](../../use-cases/debugging.md).

## Foutopsporing inschakelen met de Web SDK JavaScript-bibliotheek

Stel de `debugEnabled` boolean naar `true` wanneer de `configure` gebruiken. Als u deze eigenschap weglaat bij het configureren van de SDK, wordt standaard ingesteld op `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
