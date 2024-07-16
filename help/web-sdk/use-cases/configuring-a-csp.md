---
title: Een CSP configureren
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Leer hoe te om CSP voor het Web SDK van het Experience Platform te vormen
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configureren;configuratie;SDK;edge;Web SDK;configure;context;web;apparaat;omgeving;web sdk-instellingen;content-beveiligingsbeleid;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Een CSP configureren

A [ het Beleid van de Veiligheid van de Inhoud ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) wordt gebruikt om de middelen te beperken browser wordt toegestaan te gebruiken. Het CSP kan ook de functionaliteit van manuscript en stijlmiddelen beperken. Adobe Experience Platform Web SDK vereist geen CSP, maar het toevoegen van één kan de aanvalsoppervlakte verminderen om tegen kwaadwillige aanvallen te verhinderen.

Het CSP moet weerspiegelen hoe [!DNL Platform Web SDK] wordt opgesteld en gevormd. In het volgende CDV wordt aangegeven welke wijzigingen nodig zijn om de SDK correct te laten functioneren. Afhankelijk van uw specifieke omgeving zijn waarschijnlijk aanvullende CSP-instellingen vereist.

## Voorbeeld van beveiligingsbeleid voor inhoud

De volgende voorbeelden tonen hoe te om CSP te vormen.

### Toegang tot het randdomein toestaan

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

In het bovenstaande voorbeeld moet `EDGE-DOMAIN` worden vervangen door het domein van de eerste partij. Het eerste partijdomein wordt gevormd voor [ edgeDomain ](../commands/configure/edgedomain.md) het plaatsen. Als er geen domein van de eerste partij is geconfigureerd, moet `EDGE-DOMAIN` worden vervangen door `*.adobedc.net` . Als de bezoekersmigratie gebruikend [ idMigrationEnabled ](../commands/configure/idmigrationenabled.md) wordt aangezet, moet de `connect-src` richtlijn ook `*.demdex.net` omvatten.

### NONCE gebruiken om inlinescript en stijlelementen toe te staan

[!DNL Platform Web SDK] kan pagina-inhoud wijzigen en moet worden goedgekeurd om inline script- en stijltags te maken. Om dit te verwezenlijken, adviseert de Adobe het gebruiken van één keer voor [ gebrek-src ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP richtlijn. Een nonce is een cryptografisch sterk willekeurig token dat door de server wordt gegenereerd en dat één keer per unieke paginaweergave wordt gegenereerd.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Bovendien moet CSP nonce als attribuut aan de [!DNL Platform Web SDK] [ markering van het basiscode ](../install/library.md) manuscript worden toegevoegd. [!DNL Platform Web SDK] gebruikt deze code vervolgens eenmaal wanneer u inline script- of stijltags aan de pagina toevoegt:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Als geen enkele keer wordt gebruikt, kunt u ook `unsafe-inline` aan de CSP-instructies `script-src` en `style-src` toevoegen:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>De Adobe **adviseert** niet het specificeren `unsafe-inline` omdat het voor om het even welk manuscript om op de pagina toestaat te lopen, die de voordelen van CSP beperkt.

## Een CSP configureren voor In-App Messaging {#in-app-messaging}

Wanneer u [ het Overseinen van het Web in-App ](../personalization/web-in-app-messaging.md) vormt, moet u de volgende richtlijn in uw CSP omvatten:

```
default-src  blob:;
```
