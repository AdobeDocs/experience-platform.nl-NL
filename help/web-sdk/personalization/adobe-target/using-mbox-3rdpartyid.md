---
title: Real-time profielsynchronisatie voor mbox3rdPartyId
description: Leer hoe u mbox3rdPartyId kunt gebruiken met de Adobe Experience Platform Web SDK.
keywords: personalisatie;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# Wat is `mbox3rdPartyId`

De mbox3rdPartyId in Adobe Target is de bezoekersidentiteitskaart van uw bedrijf, zoals lidmaatschapsidentiteitskaart voor het loyaliteitsprogramma van uw bedrijf.

Wanneer een bezoeker zich aanmeldt bij de site van een bedrijf, maakt het bedrijf doorgaans een id die is gekoppeld aan de account, de loyaliteitskaart, het lidmaatschapsnummer of andere toepasselijke id&#39;s voor dat bedrijf. [Meer informatie](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=nl-NL#)


## `mbox3rdPartyId` gebruiken met de Web SDK

### Stap 1: Configureer de `Target Third Party ID Namespace`

Vorm `Target Third Party ID Namespace` in uw [ DataStream ](../../../datastreams/overview.md), gebruikend identiteitskaart Namespace u als 3de partijidentiteitskaart wilt gebruiken.
[ Leer meer over identiteitskaart namespaces ](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl)

![ Experience Platform UI die het van de Derde van het Doel namespace gebied toont.](assets/mbox3rdpartyid.png)

### Stap 2: De `mbox3rdpartyId` naar doel verzenden

Verzend `mbox3rdpartyId` naar Doel in het `sendEvent` bevel, gebruikend identiteitskaart namespace die u in Stap 1 vormde.
[ leer meer over het verzenden van IDs ](../../identity/overview.md#syncing-identities)

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
