---
title: Experience Cloud ID ophalen
seo-title: Adobe Experience Platform Web SDK Experience Cloud ID ophalen
description: Leer hoe u Adobe Experience Cloud ID kunt ophalen.
seo-description: Leer hoe u Adobe Experience Cloud ID kunt ophalen.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# (bètaversie) Experience Cloud ID ophalen

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Adobe Experience Cloud gebruikt een unieke id voor elke consument. Gebruik de `getIdentity` opdracht als u deze unieke id wilt gebruiken. `getIdentity` retourneert de bestaande ECID voor de huidige bezoeker. Voor nieuwe bezoekers die nog geen ECID hebben, genereert deze opdracht een nieuwe ECID.

>[!NOTE]
>
>Deze methode wordt meestal gebruikt met aangepaste oplossingen waarvoor de Experience Cloud-id moet worden gelezen. Het wordt niet gebruikt door een standaardimplementatie.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
