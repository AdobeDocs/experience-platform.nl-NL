---
title: Gebeurtenisgegevens samenvoegen
seo-title: Adobe Experience Platform Web SDK-gebeurtenisgegevens samenvoegen
description: Leer hoe te om de gebeurtenisgegevens van SDK van het Web van het Experience Platform samen te voegen
seo-description: Leer hoe te om de gebeurtenisgegevens van SDK van het Web van het Experience Platform samen te voegen
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Gebeurtenisgegevens samenvoegen

>[!IMPORTANT]
>
>Deze functie is nog in ontwikkeling. Niet alle oplossingen kunnen gebeurtenisgegevens samenvoegen zoals op deze pagina wordt beschreven.

Soms zijn niet alle gegevens beschikbaar wanneer een gebeurtenis plaatsvindt. U zou de gegevens kunnen willen vangen u hebt zodat wordt het niet verloren als, bijvoorbeeld, de gebruiker browser sluit. Anderzijds kunt u ook gegevens opnemen die later beschikbaar komen.

In dergelijke gevallen kunt u gegevens samenvoegen met eerdere gebeurtenissen door `mergeId` als volgt een optie aan `event` opdrachten door te geven:

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
  },
  "mergeId": "ABC123"
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
  },
  "mergeId": "ABC123"
});
```

Door de zelfde waarde voor de `mergeId` optie tot beide gebeurtenisbevelen in dit voorbeeld over te gaan, worden de gegevens in het tweede gebeurtenisbevel uitgebreid tot gegevens eerder verzonden op het eerste gebeurtenisbevel. Er wordt een record voor elke gebeurtenisopdracht gemaakt in de [!DNL Experience Data Platform]map, maar tijdens de rapportage worden de records samengevoegd met de id voor het samenvoegen van gebeurtenissen en weergegeven als één gebeurtenis.

Als u gegevens over een bepaalde gebeurtenis naar externe providers verzendt, kunt u dezelfde gebeurtenis ook samenvoegen-id met die gegevens opnemen. Later, als u ervoor kiest om de gegevens van derden te importeren in Adobe Experience Platform, wordt de id voor het samenvoegen van gebeurtenissen gebruikt om alle gegevens samen te voegen die zijn verzameld als gevolg van de specifieke gebeurtenis die op uw webpagina heeft plaatsgevonden.

## Een samenvoegen-id voor een gebeurtenis genereren

De id voor het samenvoegen van gebeurtenissen kan elke tekenreeks zijn die u kiest, maar houd er rekening mee dat alle gebeurtenissen die met dezelfde id worden verzonden als één gebeurtenis worden gerapporteerd. Wees daarom voorzichtig met het afdwingen van eenduidigheid wanneer gebeurtenissen niet moeten worden samengevoegd. Als u wilt dat de SDK namens u een unieke gebeurtenis samenvoegt-id genereert (volgens de algemeen aanvaarde [UUID v4-specificatie](https://www.ietf.org/rfc/rfc4122.txt)), kunt u de `createEventMergeId` opdracht gebruiken om dit te doen.

Zoals met alle bevelen, is een belofte teruggekeerd omdat u het bevel zou kunnen uitvoeren alvorens SDK klaar is met laden. De belofte wordt zo snel mogelijk opgelost met een unieke samengevoegd-id voor de gebeurtenis. U kunt op de belofte wachten om worden opgelost alvorens gegevens naar de server te verzenden als volgt:

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
    },
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
    },
    "mergeId": results.eventMergeId
  });
});
```

Volg hetzelfde patroon als u om andere redenen toegang wilt tot de samenvoegings-id van de gebeurtenis (bijvoorbeeld om deze naar een externe provider te verzenden):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Opmerking over XDM-indeling

Binnen het gebeurtenisbevel, wordt identiteitskaart van de gebeurtenisfusie toegevoegd aan de `xdm` lading in uw naam op de correcte plaats.  De id voor het samenvoegen van gebeurtenissen kan desgewenst als onderdeel van de `xdm` optie worden verzonden, zoals:

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

Wanneer u de samenvoegen-id voor de gebeurtenis rechtstreeks aan het `xdm` object toevoegt, wordt de naam `eventMergeID` gebruikt in plaats van `mergeId`.
