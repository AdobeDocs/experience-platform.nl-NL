---
title: De TCF 2.0-ondersteuning van IAB integreren met de SDK van Adobe Experience Platform Web
description: Leer hoe u IAB TCF 2.0-ondersteuning voor uw website instelt zonder Adobe Experience Platform Launch te gebruiken.
seo-description: Meer informatie over het instellen van IAB TCF 2.0-toestemming met Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Integreer IAB TCF 2.0 steun met het Web SDK van het Platform

Deze gids toont hoe te om het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0) met het Web SDK van Adobe Experience Platform te integreren zonder Experience Platform Launch te gebruiken. Voor een overzicht van het integreren met IAB TCF 2.0, lees [overzicht](./overview.md). Voor een gids over hoe te met Experience Platform Launch te integreren, lees [IAB TCF 2.0 gids voor Experience Platform Launch](./with-launch.md).

## Aan de slag

Deze gids gebruikt de `__tcfapi` interface voor de toegang tot van de toestemmingsinformatie. Het kan voor u gemakkelijker zijn om direct met uw leverancier van het wolkenbeheer (CMP) te integreren. De informatie in deze handleiding kan echter nog steeds nuttig zijn omdat de CMP&#39;s over het algemeen vergelijkbare functionaliteit bieden als de TCF API.

>[!NOTE]
>
>In deze voorbeelden wordt ervan uitgegaan dat `window.__tcfapi` op het moment dat de code wordt uitgevoerd, op de pagina is gedefinieerd. CMPs kan een haak verstrekken waar u deze functies kon in werking stellen wanneer het `__tcfapi` voorwerp klaar is.

Om IAB TCF 2.0 met Experience Platform Launch en de uitbreiding van SDK van het Web van Adobe Experience Platform te gebruiken, moet u een beschikbaar schema XDM hebben. Als u geen van beide instellingen hebt ingesteld, begint u met het weergeven van deze pagina voordat u verdergaat.

Bovendien vereist deze handleiding dat u een goed begrip hebt van de SDK van Adobe Experience Platform Web. Lees voor een snelle vernieuwing de [Adobe Experience Platform Web SDK overview](../../home.md) en de [Veelgestelde vragen](../../web-sdk-faq.md) documentatie.

## Standaardtoestemming inschakelen

Als u alle onbekende gebruikers het zelfde wilt behandelen, kunt u de standaardtoestemming aan `pending` of `out` plaatsen. Hiermee worden Experience Events in een wachtrij geplaatst of genegeerd totdat de voorkeuren voor toestemming zijn ontvangen.

Voor meer informatie over standaardtoestemming, verwijs naar [standaardtoestemmingssectie](../../fundamentals/configuring-the-sdk.md#default-consent) in de de configuratiedocumentatie van SDK van het Web van het Platform.

### De standaardtoestemming instellen op `gdprApplies`

Sommige CMP&#39;s kunnen bepalen of algemene gegevensbeschermingsverordening (General Data Protection Regulation — GDPR) op de klant van toepassing is. Als u toestemming voor klanten wilt veronderstellen waar GDPR niet van toepassing is, kunt u de `gdprApplies` vlag in de TCF API vraag gebruiken.

In het volgende voorbeeld wordt een manier getoond om dit te doen:

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

In dit voorbeeld wordt de opdracht `configure` aangeroepen nadat de opdracht `tcData` is verkregen van de TCF API. Als `gdprApplies` waar is, wordt de standaardtoestemming geplaatst aan `pending`. Als `gdprApplies` onwaar is, wordt de standaardtoestemming geplaatst aan `in`. Ben zeker om de `alloyConfiguration` variabele met uw configuratie in te vullen.

>[!NOTE]
>
>Wanneer de standaardtoestemming wordt geplaatst aan `in`, kan `setConsent` bevel nog worden gebruikt om uw voorkeur van de klantentoestemming te registreren.

## De gebeurtenis setConsent gebruiken

IAB TCF 2.0 API verstrekt een gebeurtenis voor wanneer de toestemming door de klant wordt bijgewerkt. Dit gebeurt wanneer de klant eerst zijn voorkeuren instelt en wanneer de klant zijn voorkeuren bijwerkt.

In het volgende voorbeeld wordt een manier getoond om dit te doen:

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Dit codeblok luistert naar de gebeurtenis `useractioncomplete` en stelt vervolgens de toestemming in, waarbij de toestemmingstekenreeks en de markering `gdprApplies` worden doorgegeven. Als u aangepaste identiteiten voor uw klanten hebt, moet u de variabele `identityMap` invullen. Raadpleeg de handleiding bij [Ondersteunende toestemming](../../consent/supporting-consent.md) voor meer informatie over het aanroepen van `setConsent`.

## Informatie over toestemming opnemen in sendEvent

In XDM-schema&#39;s kunt u informatie over voorkeuren voor toestemmingen opslaan van Experience Events. Er zijn twee manieren om deze informatie aan elke gebeurtenis toe te voegen.

Eerst, kunt u het relevante XDM schema op elke `sendEvent` vraag verstrekken. In het volgende voorbeeld wordt een manier getoond om dit te doen:

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

In dit voorbeeld wordt de informatie over de toestemming voor de TCF API opgehaald en wordt vervolgens een gebeurtenis verzonden met de informatie over de toestemming die aan het XDM-schema is toegevoegd. Zie [het volgen gebeurtenissen](../../fundamentals/tracking-events.md) gids om te begrijpen wat in `sendEvent` bevelopties zou moeten zijn.

De andere manier om de toestemmingsinformatie aan elk verzoek toe te voegen is met `onBeforeEventSend` callback. Lees de sectie over [het wijzigen van gebeurtenissen globally](../../fundamentals/tracking-events.md#modifying-events-globally) van binnen de volgende gebeurtenisdocumentatie voor meer informatie over hoe te om dit te doen.

## Volgende stappen

Nu u hebt geleerd hoe te om IAB TCF 2.0 met de uitbreiding van SDK van het Web van het Platform te gebruiken, kunt u ook verkiezen om met andere Adobe oplossingen zoals Adobe Analytics of het platform van de Gegevens van de Klant in real time te integreren. Zie [IAB Transparency &amp; Consent Framework 2.0 overzicht](./overview.md) voor meer informatie.
