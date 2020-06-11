---
title: Interactie met meerdere eigenschappen
seo-title: Adobe Experience Platform Web SDK Interactie met meerdere eigenschappen
description: Leer hoe te met de veelvoudige eigenschappen van SDK van het Web van het Platform van de Ervaring in wisselwerking staan
seo-description: Leer hoe te met de veelvoudige eigenschappen van SDK van het Web van het Platform van de Ervaring in wisselwerking staan
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Interactie met meerdere eigenschappen

Er zijn bepaalde gevallen waarin u mogelijk wilt werken met twee verschillende eigenschappen op dezelfde pagina. Deze omvatten:

* Bedrijven die zijn aangeschaft en werken aan de integratie van hun websites
* Relaties tussen meerdere bedrijven voor het uitwisselen van gegevens
* Klanten die nieuwe Adobe-oplossingen testen en hun bestaande implementatie niet willen verstoren

Met de SDK kunt u een aparte instantie voor elke eigenschap maken door een andere naam toe te voegen aan de array in de basiscode. In het volgende voorbeeld hebben we twee namen opgegeven, `mycustomname1` en `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Hierdoor worden in het script twee instanties van de SDK gemaakt. De algemene functie voor interactie met de eerste instantie wordt genoemd `mycustomname1` en de algemene functie voor interactie met de tweede instantie wordt genoemd `mycustomname2`.

Door twee afzonderlijke instanties te creëren, kan elk voor een verschillend bezit worden gevormd. Elke communicatie of gegevenspersistentie die optreedt als gevolg van interactie met `mycustomname1` `mycustomname2` wordt geïsoleerd gehouden en omgekeerd.

In het volgende voorbeeld kunt u als volgt opdrachten uitvoeren met elk van de instanties:

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Zorg ervoor dat u de `configure` opdracht voor elke instantie uitvoert voordat u andere opdrachten voor dezelfde instantie uitvoert.

## Beperkingen

Om conflicten met cookies te voorkomen, kan slechts één instantie van Adobe Experience Platform Web SDK binnen een pagina een bepaalde versie hebben `edgeConfigId`.  Op dezelfde manier kan slechts één geval van het Web SDK van Adobe Experience Platform een bepaalde hebben `orgId`.
