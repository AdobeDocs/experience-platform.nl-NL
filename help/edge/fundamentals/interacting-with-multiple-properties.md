---
title: Interactie met meerdere eigenschappen
seo-title: Adobe Experience Platform Web SDK Interactie met meerdere eigenschappen
description: Leer hoe te met de veelvoudige eigenschappen van SDK van het Web van het Platform van de Ervaring in wisselwerking staan
seo-description: Leer hoe te met de veelvoudige eigenschappen van SDK van het Web van het Platform van de Ervaring in wisselwerking staan
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
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
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("event", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "configId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("event", {
  "data": {
    "key": "value"
  }
});
```

Zorg ervoor dat u de `configure` opdracht voor elke instantie uitvoert voordat u andere opdrachten voor dezelfde instantie uitvoert.

## Beperkingen

Om conflicten met cookies te voorkomen, kan slechts één exemplaar van de Adobe Experience Platform Web SDK op een pagina een bepaalde versie hebben `configId`.  Op dezelfde manier kan slechts één exemplaar van Adobe Experience Platform Web SDK een bepaalde versie hebben `orgId`.
