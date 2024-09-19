---
title: getIdentity
description: Verkrijg de identiteit van een bezoeker zonder gebeurtenisgegevens te verzenden.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# `getIdentity`

Met de opdracht `getIdentity` kunt u een bezoeker-id verkrijgen zonder gebeurtenisgegevens te verzenden. Wanneer u de opdracht `sendEvent` uitvoert, verkrijgt de web-SDK automatisch de identiteit van de bezoeker als deze nog niet aanwezig is.

Als u afzonderlijke vraag vereist om een bezoekersidentiteitskaart te produceren en gegevens te verzenden, kunt u dit bevel gebruiken.

## Identiteit ophalen met de webSDK-tagextensie

De de markeringsuitbreiding van SDK van het Web biedt dit bevel door de markering van de uitbreiding UI niet aan. Gebruik de aangepaste code-editor met de syntaxis van de JavaScript-bibliotheek.

## Identiteit ophalen met de Web SDK JavaScript-bibliotheek

Voer het `getIdentity` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. De volgende opties zijn beschikbaar wanneer het vormen van dit bevel:

* **`namespaces`**: een array van naamruimten. De standaardwaarde is `["ECID"]` . Andere ondersteunde waarden zijn: `["CORE"]`, `null`, `undefined` . U kunt [!DNL ECID] en [!DNL CORE ID] tegelijkertijd aanvragen. Voorbeeld: `"namespaces": ["ECID","CORE"]` .
* **`edgeConfigOverrides`**: Een [ datastream configuratieopheffingsvoorwerp ](datastream-overrides.md).

```js
alloy("getIdentity",{
  "namespaces": ["ECID","CORE"] //this command retrieves both ECID and CORE IDs.
});
```

## Object Response

Als u besluit om [ reacties ](command-responses.md) met dit bevel te behandelen, zijn de volgende eigenschappen beschikbaar in het reactievoorwerp:

* **`identity.ECID`**: Een tekenreeks die de ECID van de bezoeker bevat.
* **`identity.CORE`**: Een tekenreeks met de CORE-id van de bezoeker.
* **`edge.regionID`**: Een geheel getal dat het gebied van de Edge Network vertegenwoordigt dat de browser detecteert bij het verkrijgen van een identiteit. Dit is hetzelfde als de locatiehint van de verouderde Audience Manager.
