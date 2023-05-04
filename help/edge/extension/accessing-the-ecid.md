---
title: Toegang tot de ECID
description: Leer hoe u de Experience Cloud-id kunt openen met Data Prep of Tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: dee04f2cdeb9057ac10e27a17f9db3f065712618
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Toegang tot de ECID

De [!DNL Experience Cloud Identity (ECID)] is een permanente id die aan een gebruiker wordt toegewezen wanneer deze uw website bezoekt. In bepaalde omstandigheden hebt u wellicht liever toegang tot de [!DNL ECID] (bijvoorbeeld om het naar een derde te verzenden). Een ander gebruiksgeval stelt het [!DNL ECID] in een aangepast XDM-veld, naast het opnemen ervan in het identiteitsoverzicht.

U kunt toegang krijgen tot de ECID via [Gegevensvoorvoegsel voor gegevensverzameling](../datastreams/data-prep.md) (aanbevolen) of via tags.

## Toegang tot de ECID via Data Prep (voorkeursmethode) {#accessing-ecid-data-prep}

Als u de ECID wilt instellen in een aangepast XDM-veld, kunt u dit niet alleen doen in het identiteitsoverzicht, maar ook `source` naar het volgende pad:

```js
xdm.identityMap.ECID[0].id
```

Stel het doel vervolgens in op een XDM-pad waar het veld van het type is `string`.

![](./assets/access-ecid-data-prep.png)

## Tags

Als u toegang moet krijgen tot de [!DNL ECID] op de client gebruikt u de onderstaande tagaanpak.

1. Verzeker uw bezit met wordt gevormd [regelcomponentvolgorde](../../tags/ui/managing-resources/rules.md#sequencing) ingeschakeld.
1. Maak een nieuwe regel.
1. Voeg een [!UICONTROL Library Loaded] aan de regel.
1. Voeg een [!UICONTROL Custom Condition] actie aan de regel met de volgende code (veronderstellend de naam u voor de instantie van SDK hebt gevormd is `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Sla de regel op.

U zou dan tot [!DNL ECID] in de volgende regels `%ECID%` of `_satellite.getVar("ECID")`, zoals u tot een ander gegevenselement zou toegang hebben.
