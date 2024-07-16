---
title: Toegang tot de ECID
description: Leer hoe u de Experience Cloud-id kunt openen met Data Prep of Tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Toegang tot de ECID

De [!DNL Experience Cloud Identity (ECID)] is een permanente id die aan een gebruiker wordt toegewezen wanneer deze uw website bezoekt. In bepaalde omstandigheden hebt u wellicht liever toegang tot [!DNL ECID] (bijvoorbeeld om het bestand naar een derde partij te verzenden). Een ander gebruiksgeval is het plaatsen van [!DNL ECID] in een douane XDM gebied, naast het hebben van het in de identiteitskaart.

U kunt tot ECID of via [ Prep van Gegevens voor de Inzameling van Gegevens ](../../../../datastreams/data-prep.md) (geadviseerd) of via markeringen toegang hebben.

## Toegang tot de ECID via Data Prep (voorkeursmethode) {#accessing-ecid-data-prep}

Als u de ECID wilt instellen in een aangepast XDM-veld, kunt u deze niet alleen in het identiteitsoverzicht opnemen, maar u kunt dit ook doen door de `source` in te stellen op het volgende pad:

```js
xdm.identityMap.ECID[0].id
```

Stel het doel vervolgens in op een XDM-pad waar het veld van het type `string` is.

![](./assets/access-ecid-data-prep.png)

## Tags

Als u toegang wilt krijgen tot de [!DNL ECID] aan de clientzijde, gebruikt u de tagbenadering zoals hieronder beschreven.

1. Verzeker uw bezit met [ wordt gevormd regelcomponent die ](../../../ui/managing-resources/rules.md#sequencing) wordt toegelaten rangschikken.
1. Maak een nieuwe regel. Deze regel moet alleen worden gebruikt voor het vastleggen van de [!DNL ECID] zonder andere belangrijke handelingen.
1. Voeg een [!UICONTROL Library Loaded] -gebeurtenis aan de regel toe.
1. Voeg een handeling [!UICONTROL Custom Code] aan de regel toe met de volgende code (ervan uitgaande dat de naam die u voor de SDK-instantie hebt geconfigureerd `alloy` is en dat er nog geen gegevenselement met dezelfde naam is):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Sla de regel op.

Vervolgens hebt u toegang tot de [!DNL ECID] -regel in de volgende regels met `%ECID%` of `_satellite.getVar("ECID")` , net als tot elk ander gegevenselement.
