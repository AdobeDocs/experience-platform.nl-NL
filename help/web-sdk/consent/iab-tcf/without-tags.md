---
title: De TCF 2.0-ondersteuning van IAB integreren met de SDK van Adobe Experience Platform Web
description: Leer hoe u IAB TCF 2.0-ondersteuning voor uw website instelt zonder tags te gebruiken.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Integreer IAB TCF 2.0 steun met het Web SDK van het Platform

Deze gids toont hoe te om het Interactieve Kader van de Transparantie &amp; van de Toestemming van het Reclamebureau, versie 2.0 (IAB TCF 2.0) met SDK van het Web van Adobe Experience Platform te integreren zonder markeringen te gebruiken. Voor een overzicht van het integreren met IAB TCF 2.0, lees [overzicht](./overview.md). Voor een gids over hoe te met markeringen te integreren, lees [IAB TCF 2.0-gids voor tags](./with-tags.md).

## Aan de slag

Deze handleiding gebruikt de `__tcfapi` interface voor toegang tot de toestemmingsinformatie. Het kan voor u gemakkelijker zijn om direct met uw leverancier van het wolkenbeheer (CMP) te integreren. De informatie in deze handleiding kan echter nog steeds nuttig zijn omdat de CMP&#39;s over het algemeen vergelijkbare functionaliteit bieden als de TCF API.

>[!NOTE]
>
>In deze voorbeelden wordt ervan uitgegaan dat tegen de tijd dat de code wordt uitgevoerd: `window.__tcfapi` wordt gedefinieerd op de pagina. CMPs kan een haak verstrekken waar u deze functies kon in werking stellen wanneer `__tcfapi` -object gereed is.

Om IAB TCF 2.0 met markeringen en de uitbreiding van SDK van het Web van Adobe Experience Platform te gebruiken, moet u een beschikbaar schema XDM hebben. Als u geen van beide instellingen hebt ingesteld, begint u met het weergeven van deze pagina voordat u verdergaat.

Bovendien vereist deze handleiding dat u een goed begrip hebt van de SDK van Adobe Experience Platform Web. Lees voor een snelle vernieuwingsfunctie de [Overzicht van Adobe Experience Platform Web SDK](../../home.md) en de [Veelgestelde vragen](../../faq.md) documentatie.

## Standaardtoestemming inschakelen

Als u alle onbekende gebruikers gelijk wilt behandelen, kunt u instellen [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) tot `pending` of `out`. Hiermee worden Experience Events in een wachtrij geplaatst of genegeerd totdat de voorkeuren voor toestemming zijn ontvangen.

### De standaardtoestemming instellen op basis van `gdprApplies`

Sommige CMP&#39;s kunnen bepalen of algemene gegevensbeschermingsverordening (General Data Protection Regulation — GDPR) op de klant van toepassing is. Als u toestemming voor klanten wilt veronderstellen waar GDPR niet van toepassing is, kunt u `gdprApplies` markering in de TCF API vraag.

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

In dit voorbeeld wordt `configure` wordt de opdracht aangeroepen na de `tcData` wordt opgehaald uit de TCF API. Indien `gdprApplies` is waar (true), is de standaardtoestemming ingesteld op `pending`. Indien `gdprApplies` is false, de standaardtoestemming is ingesteld op `in`. Zorg ervoor dat u de `alloyConfiguration` variabele met uw configuratie.

>[!NOTE]
>
>Als de standaardtoestemming is ingesteld op `in`de `setConsent` nog steeds kunt u deze opdracht gebruiken om uw voorkeuren voor klantentoestemming vast te leggen.

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

Dit codeblok luistert naar de `useractioncomplete` en stelt vervolgens de toestemming in, waarbij de tekenreeks voor toestemming en de `gdprApplies` markering. Als u aangepaste id&#39;s voor uw klanten hebt, moet u de `identityMap` variabele. Raadpleeg de handleiding op [ondersteunende instemming](../../consent/supporting-consent.md) voor meer informatie over het roepen `setConsent`.

## Informatie over toestemming opnemen in sendEvent

In XDM-schema&#39;s kunt u informatie over voorkeuren voor toestemmingen opslaan van Experience Events. Er zijn twee manieren om deze informatie aan elke gebeurtenis toe te voegen.

Eerst kunt u het relevante XDM-schema op elke `sendEvent` vraag. In het volgende voorbeeld wordt een manier getoond om dit te doen:

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

In dit voorbeeld wordt de informatie over de toestemming voor de TCF API opgehaald en wordt vervolgens een gebeurtenis verzonden met de informatie over de toestemming die aan het XDM-schema is toegevoegd.

De andere manier om de toestemmingsinformatie aan elk verzoek toe te voegen is met de [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) callback.

## Volgende stappen

Nu u hebt geleerd hoe te om IAB TCF 2.0 met de uitbreiding van SDK van het Web van het Platform te gebruiken, kunt u ook verkiezen om met andere Adobe oplossingen zoals Adobe Analytics of Adobe Real-time Customer Data Platform te integreren. Zie de [IAB-overzicht van transparantie en instemming in framework 2.0](./overview.md) voor meer informatie .
