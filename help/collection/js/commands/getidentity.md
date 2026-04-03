---
title: getIdentity
description: Verkrijg de identiteit van een bezoeker zonder gebeurtenisgegevens te verzenden.
exl-id: 28b99f62-14c4-4e52-a5c7-9f6fe9852a87
source-git-commit: b292b9243816b1eed7fd3939096ddc30d6be0606
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# `getIdentity`

Wanneer u de opdracht [`sendEvent`](sendevent/overview.md) uitvoert, verkrijgt de Web SDK automatisch de identiteit van de bezoeker als deze nog niet aanwezig is. Met de opdracht `getIdentity` kunt u een bezoeker-id verkrijgen zonder gebeurtenisgegevens te verzenden. Als u afzonderlijke vraag vereist om een bezoekersidentiteitskaart te produceren en gegevens te verzenden, kunt u dit bevel gebruiken.

>[!IMPORTANT]
>
>Gebruik `getIdentity` wanneer u identiteitsgegevens op de client nodig hebt. Als u slechts ECID in XDM in kaart moet brengen, gebruik [&#x200B; Prep van Gegevens voor de Inzameling van Gegevens &#x200B;](/help/datastreams/data-prep.md) of [&#x200B; markeringen ECID toegangsbegeleiding &#x200B;](/help/tags/extensions/client/web-sdk/accessing-the-ecid.md) in plaats daarvan.

De opdracht `getIdentity` doorloopt de volgende stroom om de `ECID` op te halen.

1. U gebruikt de Web SDK om `getIdentity` of [`appendIdentityToUrl`](appendidentitytourl.md) aan te roepen.
1. Web SDK wacht op informatie over toestemming.
1. Web SDK controleert of de naamruimte `ECID` is aangevraagd voor de aanroep. Standaard wordt de naamruimte `ECID` altijd opgenomen.
1. Web SDK leest het `kndctr` -cookie en retourneert de waarde ervan als `ECID` , als deze bestaat. Hiermee wordt alleen de waarde `ECID` geretourneerd, maar niet de waarde `regionId` .
1. Als het `kndctr` identiteitscookie niet is ingesteld of als de `"CORE"` -naamruimte is aangevraagd, vraagt Web SDK een aanvraag in bij de Edge Network.
1. De Edge Network retourneert zowel de `ECID` als de `regionId` (en de `CORE ID` , indien gevraagd).

Voer het `getIdentity` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. De volgende opties zijn beschikbaar wanneer het vormen van dit bevel:

* **`namespaces`**: een array van naamruimten. De standaardwaarde is `["ECID"]` . Andere ondersteunde waarden zijn:
   * `["CORE"]`
   * `["ECID","CORE"]`
   * `null`
   * `undefined`

  U kunt `"ECID"` en `"CORE ID"` tegelijkertijd aanvragen. Voorbeeld: `"namespaces": ["ECID","CORE"]` .

* **`edgeConfigOverrides`**: A [&#x200B; datastream configuratieopheffingsvoorwerp &#x200B;](configure/edgeconfigoverrides.md).

```js
alloy("getIdentity",{
  // This command retrieves both ECID and CORE IDs
  "namespaces": ["ECID","CORE"] 
});
```

## Object Response

Als u besluit om [&#x200B; reacties &#x200B;](command-responses.md) met dit bevel te behandelen, zijn de volgende eigenschappen beschikbaar in het reactievoorwerp:

* **`identity.ECID`**: Een tekenreeks die de ECID van de bezoeker bevat.
* **`identity.CORE`**: Een tekenreeks met de CORE-id van de bezoeker.
* **`edge.regionID`**: Een geheel getal dat het Edge Network-gebied vertegenwoordigt dat de browser detecteert bij het verkrijgen van een identiteit. Dit is hetzelfde als de oude Audience Manager-locatiehint.

```js
// Get the visitor's ECID
alloy('getIdentity').then(result => {
  console.log(result.identity.ECID);
});
```

## Identiteit ophalen met de webtagextensie SDK

De Web SDK-tagextensie biedt deze opdracht niet via de gebruikersinterface van de tagextensie. Gebruik de aangepaste code-editor met de syntaxis van de JavaScript-bibliotheek.
