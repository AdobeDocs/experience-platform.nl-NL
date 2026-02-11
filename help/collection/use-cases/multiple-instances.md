---
title: Meerdere Web SDK-instanties gebruiken
description: Leer hoe u communiceert met meerdere Experience Platform Web SDK-eigenschappen.
keywords: meerdere eigenschappen
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Meerdere Web SDK-instanties gebruiken

Er zijn bepaalde gevallen waarin u mogelijk wilt werken met twee verschillende eigenschappen op dezelfde pagina. Mogelijke scenario&#39;s zijn:

* Bedrijven die zijn aangeschaft en werken aan de integratie van hun websites
* Relaties tussen meerdere bedrijven voor het uitwisselen van gegevens
* Klanten die nieuwe Adobe-oplossingen testen en hun bestaande implementatie niet willen verstoren

SDK staat u toe om een afzonderlijke instantie voor elk bezit tot stand te brengen door een andere naam aan de serie in de [&#x200B; basiscode &#x200B;](../js/install/base-code.md) toe te voegen. In het volgende voorbeeld worden twee namen gegeven, `titanium` en `copper` .

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

Hierdoor maakt het script twee algemene functies ( `titanium` en `copper` in het bovenstaande voorbeeld) die twee SDK-instanties worden wanneer de bibliotheek wordt geïnitialiseerd. Elke instantie behoudt zijn eigen configuratie en status. Opdrachten die `titanium` gebruiken, blijven gescheiden van `copper` .

>[!TIP]
>
>Als het gebruiken van de basiscode met markeringen, zorg ervoor dat alle instantienamen die u plaatst alle [&#x200B; instantienamen van SDK &#x200B;](/help/tags/extensions/client/web-sdk/configure/general.md) aanpassen wanneer het vormen van de markeringsuitbreiding.

In het volgende voorbeeld van het naampatroon `titanium` en `copper` als Web SDK-instanties kunt u onafhankelijk opdrachten uitvoeren:

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

Zorg ervoor dat u de opdracht [`configure`](../js/commands/configure/overview.md) voor elke instantie uitvoert voordat u andere opdrachten voor dezelfde instantie uitvoert.

>[!IMPORTANT]
>
>Om conflicten met cookies te voorkomen, moet elke Web SDK-instantie zijn eigen unieke `datastreamId` en eigen unieke `orgId` hebben.
