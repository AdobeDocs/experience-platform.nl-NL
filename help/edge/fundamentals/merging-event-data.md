---
title: Gebeurtenisgegevens samenvoegen
seo-title: Adobe Experience Platform Web SDK-gebeurtenisgegevens samenvoegen
description: Leer hoe te om de gebeurtenisgegevens van SDK van het Web van het Experience Platform samen te voegen
seo-description: Leer hoe te om de gebeurtenisgegevens van SDK van het Web van het Experience Platform samen te voegen
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---


# Gebeurtenisgegevens samenvoegen

>[!IMPORTANT]
>
>Deze functie is nog in ontwikkeling. Niet alle oplossingen kunnen gebeurtenisgegevens samenvoegen zoals op deze pagina wordt beschreven.

Soms zijn niet alle gegevens beschikbaar wanneer een gebeurtenis plaatsvindt. U zou de gegevens kunnen willen vangen u hebt zodat wordt het niet verloren als, bijvoorbeeld, de gebruiker browser sluit. Anderzijds kunt u ook gegevens opnemen die later beschikbaar komen.

In dergelijke gevallen kunt u gegevens samenvoegen met eerdere gebeurtenissen door `eventMergeId` als volgt een optie aan `event` opdrachten door te geven:

```javascript
alloy("sendEvent", {
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

alloy("sendEvent", {
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

Door dezelfde `eventMergeID` waarde aan beide gebeurtenisopdrachten in dit voorbeeld door te geven, worden de gegevens in de tweede gebeurtenisopdracht aangevuld met gegevens die eerder op de eerste gebeurtenisopdracht zijn verzonden. Er wordt een record voor elke gebeurtenisopdracht gemaakt in de [!DNL Experience Data Platform]map, maar tijdens de rapportage worden de records samengevoegd met de code `eventMergeID` en weergegeven als één gebeurtenis.

Als u gegevens over een bepaalde gebeurtenis naar externe providers verzendt, kunt u dezelfde gegevens ook `eventMergeID` met die gegevens opnemen. Als u de gegevens van derden later in de Adobe Experience Platform wilt importeren, `eventMergeID` worden deze gebruikt om alle gegevens samen te voegen die zijn verzameld als gevolg van de specifieke gebeurtenis die op uw webpagina heeft plaatsgevonden.

## Een `eventMergeID`

De `eventMergeID` waarde kan elke tekenreeks zijn die u kiest, maar houd er rekening mee dat alle gebeurtenissen die met dezelfde id worden verzonden als één gebeurtenis worden gerapporteerd. Wees daarom voorzichtig met het afdwingen van uniciteit wanneer gebeurtenissen niet moeten worden samengevoegd. Als u wilt dat de SDK `eventMergeID` namens u een unieke URL genereert (volgens de algemeen aanvaarde [UUID v4-specificatie](https://www.ietf.org/rfc/rfc4122.txt)), kunt u de `createEventMergeId` opdracht gebruiken om dit te doen.

Zoals met alle bevelen, is een belofte teruggekeerd omdat u het bevel zou kunnen uitvoeren alvorens SDK klaar is met laden. De belofte zal zo snel `eventMergeID` mogelijk met een unieke oplossing worden opgelost. U kunt op de belofte wachten om worden opgelost alvorens gegevens naar de server te verzenden als volgt:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
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
  alloy("sendEvent", {
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

Volg dit zelfde patroon als u toegang tot het `eventMergeID` om andere redenen (bijvoorbeeld, om het naar een derdeleverancier te verzenden) zou willen:

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
alloy("sendEvent", {
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
