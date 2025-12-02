---
title: debugEnabled
description: Gebruik code om mogelijkheden voor foutopsporing in te schakelen op het web SDK.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

Met de eigenschap `debugEnabled` kunt u foutopsporing in- of uitschakelen met behulp van Web SDK-code. Het is één van de beschikbare manieren om [&#x200B; het zuiveren &#x200B;](/help/collection/use-cases/debugging.md) toe te laten. Het inschakelen van foutopsporing binnen uw implementatie kan handiger zijn dan andere methoden tijdens de ontwikkeling van websites wanneer u foutopsporing altijd wilt inschakelen. Deze methode van het zuiveren laat het voor alle bezoekers toe, zodat wordt het niet geadviseerd voor productiepagina&#39;s. Zie [&#x200B; het Zuiveren &#x200B;](/help/collection/use-cases/debugging.md) gebruiken gevalpagina voor meer manieren om het zuiveren toe te laten.

Stel `debugEnabled` boolean in op `true` wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de SDK, wordt standaard ingesteld op `false` .

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## Foutopsporing inschakelen met de Web SDK-tagextensie

Er zijn geen foutopsporingsopties beschikbaar die native de Web SDK-tagextensie gebruiken. Gebruik een [&#x200B; afwisselende het zuiveren methode &#x200B;](/help/collection/use-cases/debugging.md) wanneer het vormen van uw markeringsbezit.
