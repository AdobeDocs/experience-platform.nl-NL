---
title: IAB TCF 2.0 zonder Experience Platform Launch gebruiken
seo-title: De toestemming van IAB TCF 2.0 van de vestiging met de SDK van het Web van Adobe Experience Platform
description: Leer hoe u IAB TCF 2.0 instelt met de Adobe Experience Platform Web SDK
seo-description: Leer hoe u IAB TCF 2.0 instelt met de Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Het gebruiken van IAB TCF 2.0 met de uitbreiding van SDK van het Web van Adobe Experience Platform

Deze gids toont hoe te om het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0) met het Web SDK van Adobe Experience Platform te integreren zonder Experience Platform Launch te gebruiken. Voor een overzicht van het integreren met IAB TCF 2.0, lees het [overzicht](./overview.md). Voor een gids over hoe te met Experience Platform Launch te integreren, lees de [IAB TCF 2.0 gids voor Experience Platform Launch](./with-launch.md).

## Aan de slag

Deze gids gebruikt de `__tcfapi` interface voor de toegang tot van de toestemmingsinformatie. Het kan voor u gemakkelijker zijn om direct met uw leverancier van het wolkenbeheer (CMP) te integreren. De informatie in deze handleiding kan echter nog steeds nuttig zijn omdat de CMP&#39;s over het algemeen vergelijkbare functionaliteit bieden als de TCF API.

>[!NOTE]
>
>In deze voorbeelden wordt ervan uitgegaan dat de code op het moment dat deze wordt uitgevoerd, op de pagina `window.__tcfapi` is gedefinieerd. CMP&#39;s kunnen een haak vormen waar u deze functies kunt uitvoeren wanneer het `__tcfapi` object gereed is.

Om IAB TCF 2.0 met Experience Platform Launch en de uitbreiding van SDK van het Web te gebruiken AEP, moet u een beschikbaar schema XDM hebben. Als u geen van beide instellingen hebt ingesteld, begint u met het weergeven van deze pagina voordat u verdergaat.

Bovendien, vereist deze gids u een werkend inzicht in de SDK van het Web van Adobe Experience Platform te hebben. Lees voor een snelle vernieuwing het overzicht [van de SDK van het](../../home.md) Adobe Experience Platform-web en de documentatie met [veelgestelde vragen](../../web-sdk-faq.md) .

## Standaardtoestemming inschakelen

Als u alle onbekende gebruikers het zelfde wilt behandelen, kunt u de standaardtoestemming plaatsen aan `pending`. Deze wachttijden Ervaring Gebeurtenissen tot de toestemmingsvoorkeur wordt ontvangen.

Voor meer informatie over standaardtoestemming, verwijs naar de [standaardtoestemmingssectie](../../fundamentals/configuring-the-sdk.md#default-consent) in de de configuratiedocumentatie van SDK van het Web van het Platform.

### De standaardtoestemming instellen op basis van `gdprApplies`

Sommige CMP&#39;s kunnen bepalen of algemene gegevensbeschermingsverordening (General Data Protection Regulation — GDPR) op de klant van toepassing is. Als u toestemming voor klanten wilt veronderstellen waar GDPR niet van toepassing is, kunt u de `gdprApplies` vlag in de vraag TCF API gebruiken.

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

In dit voorbeeld wordt de `configure` opdracht aangeroepen nadat deze `tcData` is verkregen van de TCF API. Als `gdprApplies` waar is, wordt de standaardtoestemming geplaatst aan `pending`. Als `gdprApplies` false is, wordt de standaardtoestemming ingesteld op `in`. Ben zeker om de `alloyConfiguration` variabele met uw configuratie in te vullen.

>[!NOTE]
>
>Wanneer de standaardtoestemming wordt geplaatst aan `in`, kan het `setConsent` bevel nog worden gebruikt om uw voorkeur van de klantentoestemming te registreren.

## De gebeurtenis setConsent gebruiken

De IAB TCF 2.0 API verstrekt een gebeurtenis voor wanneer de toestemming door de klant wordt bijgewerkt. Dit gebeurt wanneer de klant eerst zijn voorkeuren instelt en wanneer de klant zijn voorkeuren bijwerkt.

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

Dit codeblok luistert naar de `useractioncomplete` gebeurtenis en stelt vervolgens de toestemming in, waarbij de toestemmingstekenreeks en de `gdprApplies` markering worden doorgegeven. Als u aangepaste identiteiten voor uw klanten hebt, moet u de `identityMap` variabele invullen. Raadpleeg de handleiding voor [ondersteunende toestemming](../../consent/supporting-consent.md) voor meer informatie over oproepen `setConsent`.

## Informatie over toestemming opnemen in sendEvent

In XDM-schema&#39;s kunt u informatie over voorkeuren voor toestemmingen opslaan van Experience Events. Er zijn twee manieren om deze informatie aan elke gebeurtenis toe te voegen.

Eerst, kunt u het relevante schema XDM op elke `sendEvent` vraag verstrekken. In het volgende voorbeeld wordt een manier getoond om dit te doen:

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

In dit voorbeeld wordt de informatie over de toestemming voor de TCF API opgehaald en wordt vervolgens een gebeurtenis verzonden met de informatie over de toestemming die aan het XDM-schema is toegevoegd. Zie de handleiding [voor het bijhouden van gebeurtenissen](../../fundamentals/tracking-events.md) om te begrijpen wat er in de `sendEvent` opdrachtopties moet staan.

De andere manier om de toestemmingsinformatie aan elk verzoek toe te voegen is met de `onBeforeEventSend` callback. Lees de sectie over het globaal [wijzigen van gebeurtenissen](../../fundamentals/tracking-events.md#modifying-events-globally) vanuit de documentatie voor het bijhouden van gebeurtenissen voor meer informatie over hoe u dit kunt doen.

## Volgende stappen

Nu u hebt geleerd hoe te om IAB TCF 2.0 met de uitbreiding van SDK van het Web van Adobe Experience Platform te gebruiken, kunt u ook verkiezen om met andere oplossingen van de Adobe zoals Adobe Analytics of het platform van de Gegevens van de Klant in real time te integreren. Zie het overzicht [van](./overview.md) IAB Transparency &amp; Consent Framework 2.0 voor meer informatie.
