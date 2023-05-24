---
title: Interactie met meerdere eigenschappen in de Adobe Experience Platform Web SDK
description: Leer hoe te met de veelvoudige eigenschappen van SDK van het Web van het Experience Platform in wisselwerking te staan.
keywords: meerdere eigenschappen;configure;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Interactie met meerdere eigenschappen

Er zijn bepaalde gevallen waarin u mogelijk wilt werken met twee verschillende eigenschappen op dezelfde pagina. Deze gevallen omvatten:

* Bedrijven die zijn aangeschaft en werken aan de integratie van hun websites
* Relaties tussen meerdere bedrijven voor het uitwisselen van gegevens
* Klanten die nieuwe Adobe-oplossingen testen en hun bestaande implementatie niet willen verstoren

Met de SDK kunt u een aparte instantie voor elke eigenschap maken door een andere naam toe te voegen aan de array in de basiscode. In het volgende voorbeeld worden twee namen weergegeven: `mycustomname1` en `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Hierdoor worden in het script twee instanties van de SDK gemaakt. De algemene functie voor interactie met de eerste instantie wordt `mycustomname1` en de algemene functie voor interactie met de tweede instantie wordt genoemd `mycustomname2`.

Door twee afzonderlijke instanties te creëren, kan elk voor een verschillend bezit worden gevormd. Elke communicatie- of gegevenspersistentie die optreedt als gevolg van interactie met `mycustomname1` wordt geïsoleerd gehouden van `mycustomname2`.

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

Zorg ervoor dat u de opdracht `configure` voor elke instantie voordat andere opdrachten op dezelfde instantie worden uitgevoerd.

## Beperkingen

Om conflicten met cookies te voorkomen, doet u slechts één exemplaar van Adobe Experience Platform [!DNL Web SDK] binnen een pagina kan een bepaalde `edgeConfigId`. En slechts één exemplaar van Adobe Experience Platform [!DNL Web SDK] kan een bepaalde `orgId`.
