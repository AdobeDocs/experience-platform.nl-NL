---
title: Een CSP configureren
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Leer hoe te om CSP voor het Web SDK van het Experience Platform te vormen
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configureren;configuratie;SDK;edge;Web SDK;configure;context;web;apparaat;omgeving;web sdk-instellingen;content-beveiligingsbeleid;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Een CSP configureren

A [Beveiligingsbeleid voor inhoud](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) wordt gebruikt om de middelen te beperken browser wordt toegestaan te gebruiken. Het CSP kan ook de functionaliteit van manuscript en stijlmiddelen beperken. Adobe Experience Platform Web SDK vereist geen CSP, maar het toevoegen van één kan de aanvalsoppervlakte verminderen om tegen kwaadwillige aanvallen te verhinderen.

Het CDV moet weerspiegelen hoe [!DNL Platform Web SDK] wordt opgesteld en gevormd. In het volgende CDV wordt aangegeven welke wijzigingen nodig zijn om de SDK correct te laten functioneren. Afhankelijk van uw specifieke omgeving zijn waarschijnlijk aanvullende CSP-instellingen vereist.

## Voorbeeld van beveiligingsbeleid voor inhoud

De volgende voorbeelden tonen hoe te om CSP te vormen.

### Toegang tot het randdomein toestaan

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

In het bovenstaande voorbeeld: `EDGE-DOMAIN` moet worden vervangen door het domein van de eerste partij. Het eerste partijdomein wordt gevormd voor [edgeDomain](configuring-the-sdk.md#edge-domain) instellen. Als geen first-party domein is gevormd, `EDGE-DOMAIN` vervangen door `*.adobedc.net`. Als bezoekersmigratie is ingeschakeld met [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled)de `connect-src` richtlijn moet ook `*.demdex.net`.

### NONCE gebruiken om inlinescript en stijlelementen toe te staan

[!DNL Platform Web SDK] kan pagina-inhoud wijzigen en moet worden goedgekeurd om inline script- en stijltags te maken. Om dit te bereiken, adviseert Adobe het gebruiken van één keer voor de [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP-instructie. Een nonce is een cryptografisch sterk willekeurig token dat door de server wordt gegenereerd en dat één keer per unieke paginaweergave wordt gegenereerd.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Daarnaast moet het CDV eenmaal worden toegevoegd als kenmerk van het [!DNL Platform Web SDK] [basiscode](installing-the-sdk.md#adding-the-code) scripttag. [!DNL Platform Web SDK] gebruikt deze optie vervolgens eenmaal bij het toevoegen van inline script- of stijltags aan de pagina:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Als een nonce niet wordt gebruikt, kunt u het volgende toevoegen: `unsafe-inline` aan de `script-src` en `style-src` CSP-instructies:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe doet **niet** adviseren specificeren `unsafe-inline` omdat het voor om het even welk manuscript toestaat om op de pagina te lopen, die de voordelen van het CDV beperkt.
