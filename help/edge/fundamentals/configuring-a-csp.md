---
title: Een CSP configureren
seo-title: Een CSP configureren voor Adobe Experience Platform Web SDK
description: Leer hoe te om CSP voor het Web SDK van het Experience Platform te vormen
seo-description: Leer hoe te om CSP voor het Web SDK van het Experience Platform te vormen
keywords: configureren;configuratie;SDK;edge;Web SDK;configure;context;web;apparaat;omgeving;web sdk-instellingen;content-beveiligingsbeleid;
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Een CSP configureren

Een [Inhoudsbeveiligingsbeleid](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) wordt gebruikt om de bronnen te beperken die een browser mag gebruiken. Het CSP kan ook de functionaliteit van manuscript en stijlmiddelen beperken. Adobe Experience Platform Web SDK vereist geen CSP, maar het toevoegen van één kan de aanvalsoppervlakte verminderen om tegen kwaadwillige aanvallen te verhinderen.

CSP moet weerspiegelen hoe [!DNL Platform Web SDK] wordt opgesteld en gevormd. In het volgende CDV wordt aangegeven welke wijzigingen nodig zijn om de SDK correct te laten functioneren. Afhankelijk van uw specifieke omgeving zijn waarschijnlijk aanvullende CSP-instellingen vereist.

## Voorbeeld van beveiligingsbeleid voor inhoud

De volgende voorbeelden tonen hoe te om CSP te vormen.

### Toegang tot het randdomein toestaan

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

In het bovenstaande voorbeeld moet `EDGE-DOMAIN` worden vervangen door het domein van de eerste partij. Het first-party domein wordt gevormd voor [edgeDomain](configuring-the-sdk.md#edge-domain) het plaatsen. Als geen first-party domein is gevormd, `EDGE-DOMAIN` zou met `*.adobedc.net` moeten worden vervangen. Als bezoekersmigratie is ingeschakeld met [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), moet de `connect-src`-instructie ook `*.demdex.net` bevatten.

### NONCE gebruiken om inlinescript en stijlelementen toe te staan

[!DNL Platform Web SDK] kan pagina-inhoud wijzigen en moet worden goedgekeurd om inline script- en stijltags te maken. Om dit te verwezenlijken, adviseert Adobe het gebruiken van één keer voor [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP richtlijn. Een nonce is een cryptografisch sterk willekeurig token dat door de server wordt gegenereerd en dat één keer per unieke paginaweergave wordt gegenereerd.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Daarnaast moet de CSP één keer worden toegevoegd als kenmerk aan de scripttag [!DNL Platform Web SDK] [basiscode](installing-the-sdk.md#adding-the-code). [!DNL Platform Web SDK] gebruikt deze optie vervolgens eenmaal bij het toevoegen van inline script- of stijltags aan de pagina:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Als een nonce niet wordt gebruikt, moet de andere optie `unsafe-inline` aan `script-src` en `style-src` CSP richtlijnen toevoegen:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe adviseert **not** specificerend `unsafe-inline` omdat het voor om het even welk manuscript toestaat om op de pagina te lopen, die de voordelen van CSP beperkt.
