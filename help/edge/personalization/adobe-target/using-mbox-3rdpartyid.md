---
title: Real-time profielsynchronisatie voor mbox3rdPartyId
description: Leer hoe u mbox3rdPartyId gebruikt met de Adobe Experience Platform Web SDK.
keywords: personalisatie;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
source-git-commit: 439f26177837e985ef95e972c3102cc2db37d539
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 2%

---


# Wat is `mbox3rdPartyId`

De mbox3rdPartyId in Adobe Target is de bezoekersidentiteitskaart van uw bedrijf, zoals lidmaatschapsidentiteitskaart voor het loyaliteitsprogramma van uw bedrijf.

Wanneer een bezoeker zich aanmeldt bij de site van een bedrijf, maakt het bedrijf doorgaans een id die is gekoppeld aan de account, de loyaliteitskaart, het lidmaatschapsnummer of andere toepasselijke id&#39;s voor dat bedrijf. [Meer informatie](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## Hoe wordt het gebruikt `mbox3rdPartyId` met de Web SDK

### Stap 1: Configureer de `Target Third Party ID Namespace`

Configureer de `Target Third Party ID Namespace` in uw [DataStream](../../fundamentals/datastreams.md), met de id-naamruimte die u als een box-id van een andere fabrikant wilt gebruiken.
[Meer informatie over naamruimten in id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![](assets/mbox3rdpartyid.png)

### Stap 2: Verzend de `mbox3rdpartyId` naar doel

Verzend de `mbox3rdpartyId` naar doel in de `sendEvent` bevel, gebruikend identiteitskaart namespace die u in Stap 1 vormde.
[Meer informatie over het verzenden van id&#39;s](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```


