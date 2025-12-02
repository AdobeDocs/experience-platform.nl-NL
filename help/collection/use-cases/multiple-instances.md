---
title: Meerdere Web SDK-instanties gebruiken
description: Leer hoe u communiceert met meerdere Experience Platform Web SDK-eigenschappen.
keywords: meerdere eigenschappen
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 2c60ebdebd706ed7b5beb2438ae83665b6b6e47a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Meerdere Web SDK-instanties gebruiken

Er zijn bepaalde gevallen waarin u mogelijk wilt werken met twee verschillende eigenschappen op dezelfde pagina. Deze gevallen zijn onder meer:

* Bedrijven die zijn aangeschaft en werken aan de integratie van hun websites
* Relaties tussen meerdere bedrijven voor het uitwisselen van gegevens
* Klanten die nieuwe Adobe-oplossingen testen en hun bestaande implementatie niet willen verstoren

Met de SDK kunt u voor elke eigenschap een aparte instantie maken door een andere naam toe te voegen aan de array in de basiscode. In het volgende voorbeeld worden twee namen gegeven, `titanium` en `copper` .

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Hierdoor worden in het script twee exemplaren van de SDK gemaakt. De algemene functie voor interactie met de eerste instantie krijgt de naam `titanium` en de algemene functie voor interactie met de tweede instantie krijgt de naam `copper` .

Door twee afzonderlijke instanties te creëren, kan elk voor een verschillend bezit worden gevormd. Alle communicatie- of gegevenspersistentie die optreedt als gevolg van interactie met `titanium` blijft gescheiden van `copper` .

In het volgende voorbeeld kunt u met elke instantie opdrachten uitvoeren:

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

Zorg ervoor dat u de opdracht `configure` voor elke instantie uitvoert voordat u andere opdrachten voor dezelfde instantie uitvoert.

>[!IMPORTANT]
>
>Om conflicten met cookies te voorkomen, moet elke Web SDK-instantie zijn eigen unieke `datastreamId` en eigen unieke `orgId` hebben.
