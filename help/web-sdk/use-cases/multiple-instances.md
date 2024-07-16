---
title: Meerdere Web SDK-instanties gebruiken
description: Leer hoe te met de veelvoudige eigenschappen van SDK van het Web van het Experience Platform in wisselwerking te staan.
keywords: meerdere eigenschappen;configure;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Meerdere Web SDK-instanties gebruiken

Er zijn bepaalde gevallen waarin u mogelijk wilt werken met twee verschillende eigenschappen op dezelfde pagina. Deze gevallen zijn onder meer:

* Bedrijven die zijn aangeschaft en werken aan de integratie van hun websites
* Relaties tussen meerdere bedrijven voor het uitwisselen van gegevens
* Klanten die nieuwe oplossingen van de Adobe testen en hun bestaande implementatie niet willen verstoren

Met de SDK kunt u een aparte instantie voor elke eigenschap maken door een andere naam toe te voegen aan de array in de basiscode. In het volgende voorbeeld worden twee namen gegeven, `titanium` en `copper` .

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Hierdoor worden in het script twee instanties van de SDK gemaakt. De algemene functie voor interactie met de eerste instantie krijgt de naam `titanium` en de algemene functie voor interactie met de tweede instantie krijgt de naam `copper` .

Door twee afzonderlijke instanties te creëren, kan elk voor een verschillend bezit worden gevormd. Alle communicatie- of gegevenspersistentie die optreedt als gevolg van interactie met `titanium` blijft gescheiden van `copper` .

In het volgende voorbeeld kunt u met elke instantie opdrachten uitvoeren:

```javascript
titanium("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  "data": {
    "key": "value"
  }
});

copper("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Zorg ervoor dat u de opdracht `configure` voor elke instantie uitvoert voordat u andere opdrachten voor dezelfde instantie uitvoert.

>[!IMPORTANT]
>
>Om conflicten met cookies te voorkomen, moet elke Web SDK-instantie een eigen unieke `edgeConfigId` en eigen unieke `orgId` hebben.
