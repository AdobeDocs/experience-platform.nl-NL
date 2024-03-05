---
title: getIdentity
description: Verkrijg de identiteit van een bezoeker zonder gebeurtenisgegevens te verzenden.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# `getIdentity`

De `getIdentity` kunt u een bezoeker-id verkrijgen zonder gebeurtenisgegevens te verzenden. Wanneer u de `sendEvent` , verkrijgt de SDK van het Web automatisch de identiteit van de bezoeker als er nog geen is.

Als u afzonderlijke vraag vereist om een bezoekersidentiteitskaart te produceren en gegevens te verzenden, kunt u dit bevel gebruiken.

## Identiteit ophalen met de webSDK-tagextensie

De de markeringsuitbreiding van SDK van het Web biedt dit bevel door de markering van de uitbreiding UI niet aan. Gebruik de aangepaste code-editor met JavaScript-bibliotheeksyntaxis.

## Identiteit ophalen met de Web SDK JavaScript-bibliotheek

Voer de `getIdentity` bevel wanneer het roepen van uw gevormde instantie van het Web SDK. De volgende opties zijn beschikbaar wanneer het vormen van dit bevel:

* **`namespaces`**: Een array van naamruimten. De standaardwaarde is `["ECID"]`. Geldige waarden zijn `["ECID"]`, `null`, of `undefined`.
* **`edgeConfigOverrides`**: An [DataStream-configuratieoverschrijvingsobject](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID"]
});
```

## Object Response

Als u besluit [reacties verwerken](command-responses.md) met deze opdracht zijn de volgende eigenschappen beschikbaar in het reactieobject:

* **`identity.ECID`**: Een tekenreeks met de ECID van de bezoeker.
* **`edge.regionID`**: Een geheel getal dat het Edge Network-gebied vertegenwoordigt dat de browser detecteert bij het verkrijgen van een identiteit. Dit is hetzelfde als de locatiehint van de verouderde Audience Manager.
