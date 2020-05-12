---
title: Gebeurtenisgegevens samenvoegen
seo-title: Adobe Experience Platform Web SDK-gebeurtenisgegevens samenvoegen
description: Meer informatie over het samenvoegen van Experience Platform Web SDK-gebeurtenisgegevens
seo-description: Meer informatie over het samenvoegen van Experience Platform Web SDK-gebeurtenisgegevens
translation-type: tm+mt
source-git-commit: 767f0e1bfdfcc898313b546c804ba1287f2aec50
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# (bèta) Gebeurtenisgegevens samenvoegen

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Soms zijn niet alle gegevens beschikbaar wanneer een gebeurtenis plaatsvindt. U zou de gegevens kunnen willen vangen u _hebt_ zodat wordt het niet verloren als, bijvoorbeeld, de gebruiker browser sluit. Anderzijds kunt u ook gegevens opnemen die later beschikbaar komen.

In dergelijke gevallen kunt u gegevens samenvoegen met eerdere gebeurtenissen door `eventMergeId` als volgt een optie aan `event` opdrachten door te geven:

```javascript
alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
  "eventMergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  }
  "eventMergeId": "ABC123"
});
```

Door dezelfde waarde voor de samenvoegen-id van de gebeurtenis aan beide gebeurtenisopdrachten in dit voorbeeld door te geven, worden de gegevens in de opdracht voor de tweede gebeurtenis aangevuld met gegevens die eerder zijn verzonden met de opdracht voor de eerste gebeurtenis. Een verslag voor elk gebeurtenisbevel wordt gecreeerd in het Platform van de Gegevens van de Ervaring, maar tijdens het melden worden de verslagen samengevoegd gebruikend identiteitskaart van de gebeurtenisfusie en verschijnen als één enkele gebeurtenis.

Als u gegevens over een bepaalde gebeurtenis naar externe providers verzendt, kunt u dezelfde gebeurtenis ook samenvoegen-id met die gegevens opnemen. Later, als u de gegevens van derden wilt importeren in het Adobe Experience Platform, wordt de id voor het samenvoegen van gebeurtenissen gebruikt om alle gegevens samen te voegen die zijn verzameld als gevolg van de specifieke gebeurtenis die op uw webpagina heeft plaatsgevonden.

## Een samenvoegen-id voor een gebeurtenis genereren

De waarde van de ID van de gebeurtenisfusie kan om het even welk koord zijn u kiest, maar herinner dat alle gebeurtenissen die gebruikend zelfde identiteitskaart worden verzonden als één enkele gebeurtenis worden gemeld, zodat ben zorgvuldig om uniciteit af te dwingen wanneer de gebeurtenissen niet zouden moeten worden samengevoegd. Als u wilt dat de SDK namens u een unieke gebeurtenis samenvoegt-id genereert (volgens de algemeen aanvaarde [UUID v4-specificatie](https://www.ietf.org/rfc/rfc4122.txt)), kunt u de `createEventMergeId` opdracht gebruiken om dit te doen.

Zoals met alle bevelen, is een belofte teruggekeerd omdat u het bevel zou kunnen uitvoeren alvorens SDK klaar is met laden. De belofte wordt zo snel mogelijk opgelost met een unieke samengevoegd-id voor de gebeurtenis. U kunt op de belofte wachten om worden opgelost alvorens gegevens naar de server te verzenden als volgt:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  alloy("event", {
    "xdm": {
      "commerce": {
        "order": {
          "purchaseID": "a8g784hjq1mnp3",
          "purchaseOrderNumber": "VAU3123",
          "currencyCode": "USD",
          "priceTotal": 999.98
        }
      }
    }
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("event", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    }
    "mergeId": results.eventMergeId
  });
});
```

Volg hetzelfde patroon als u om andere redenen toegang wilt tot de samenvoegen-id voor de gebeurtenis (bijvoorbeeld om deze naar een externe provider te verzenden):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Opmerking over XDM-indeling

Binnen het gebeurtenisbevel, `mergeId` wordt eigenlijk toegevoegd aan de `xdm` lading.  Indien gewenst, `mergeId` kan het als deel van de xdm optie in plaats daarvan, als dit worden verzonden:

```javascript
alloy("event", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    },
    "eventMergeId": "ABC123"
  }
});
```
