---
title: debugEnabled
description: Gebruik code om het zuiveren mogelijkheden in het Web SDK toe te laten.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

Met de eigenschap `debugEnabled` kunt u foutopsporing in- of uitschakelen met behulp van Web SDK-code. Het is één van de beschikbare manieren om [ het zuiveren ](../../use-cases/debugging.md) toe te laten. Het inschakelen van foutopsporing binnen uw implementatie kan handiger zijn dan andere methoden tijdens de ontwikkeling van websites wanneer u foutopsporing altijd wilt inschakelen. Deze methode van het zuiveren laat het voor alle bezoekers toe, zodat wordt het niet geadviseerd voor productiepagina&#39;s.

Zie [ het Zuiveren ](../../use-cases/debugging.md) gebruiken gevalpagina voor meer manieren om het zuiveren toe te laten.

## Foutopsporing inschakelen met de Web SDK-tagextensie

Er zijn geen opties voor foutopsporing beschikbaar die native de SDK-tagextensie van Web gebruiken. Gebruik een [ afwisselende het zuiveren methode ](../../use-cases/debugging.md).

## Foutopsporing inschakelen met de Web SDK JavaScript-bibliotheek

Stel `debugEnabled` boolean in op `true` wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de SDK, wordt standaard `false` gebruikt.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```
