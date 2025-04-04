---
title: De IAB TCF 2.0-ondersteuning integreren met de Adobe Experience Platform Web SDK
description: Leer hoe u IAB TCF 2.0-ondersteuning voor uw website instelt zonder tags te gebruiken.
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# Integreer IAB TCF 2.0 steun met de SDK van het Web van Experience Platform

Deze handleiding laat zien hoe u het Interactieve Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0), kunt integreren met Adobe Experience Platform Web SDK zonder tags te gebruiken. Voor een overzicht van het integreren met IAB TCF 2.0, lees het [ overzicht ](./overview.md). Voor een gids op hoe te met markeringen te integreren, lees de [ gids IAB TCF 2.0 voor markeringen ](./with-tags.md).

## Aan de slag

In deze handleiding wordt de interface `__tcfapi` gebruikt voor toegang tot de informatie over de toestemming. Het kan voor u gemakkelijker zijn om direct met uw leverancier van het wolkenbeheer (CMP) te integreren. De informatie in deze handleiding kan echter nog steeds nuttig zijn omdat de CMP&#39;s over het algemeen vergelijkbare functionaliteit bieden als de TCF API.

>[!NOTE]
>
>In deze voorbeelden wordt ervan uitgegaan dat tegen de tijd dat de code wordt uitgevoerd, `window.__tcfapi` op de pagina is gedefinieerd. CMP&#39;s kunnen een haak bevatten waar u deze functies kunt uitvoeren wanneer het `__tcfapi` -object gereed is.

Als u IAB TCF 2.0 met tags en de Adobe Experience Platform Web SDK-extensie wilt gebruiken, moet u een XDM-schema beschikbaar hebben. Als u geen van beide instellingen hebt ingesteld, begint u met het weergeven van deze pagina voordat u verdergaat.

Bovendien is voor deze handleiding een goed begrip van Adobe Experience Platform Web SDK vereist. Voor een snelle verfrisser, te lezen gelieve het [ overzicht van SDK van het Web van Adobe Experience Platform ](../../home.md) en [ vaak gestelde vragen ](../../faq.md) documentatie.

## Standaardtoestemming inschakelen

Als u alle onbekende gebruikers gelijk wilt behandelen, kunt u [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) instellen op `pending` of `out` . Hiermee worden Experience Events in een wachtrij geplaatst of genegeerd totdat de voorkeuren voor toestemming zijn ontvangen.

### De standaardtoestemming instellen op `gdprApplies`

Sommige CMP&#39;s kunnen bepalen of algemene gegevensbeschermingsverordening (General Data Protection Regulation — GDPR) op de klant van toepassing is. Als u toestemming voor klanten wilt veronderstellen waar GDPR niet van toepassing is, kunt u de `gdprApplies` markering in de vraag TCF API gebruiken.

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

In dit voorbeeld wordt de opdracht `configure` aangeroepen nadat `tcData` is verkregen van de TCF API. Als `gdprApplies` true is, wordt de standaardtoestemming ingesteld op `pending` . Als `gdprApplies` false is, wordt de standaardtoestemming ingesteld op `in` . Vul de variabele `alloyConfiguration` met uw configuratie in.

>[!NOTE]
>
>Wanneer de standaardtoestemming is ingesteld op `in` , kan de opdracht `setConsent` nog steeds worden gebruikt om de voorkeuren voor uw toestemming van klanten vast te leggen.

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

Dit codeblok luistert naar de gebeurtenis `useractioncomplete` en stelt vervolgens de toestemming in, waarbij de toestemmingstekenreeks en de markering `gdprApplies` worden doorgegeven. Als u aangepaste id&#39;s voor uw klanten hebt, moet u de variabele `identityMap` invullen. Verwijs naar de gids op [ setConsent ](../../../web-sdk/commands/setconsent.md) voor meer informatie.

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

In dit voorbeeld wordt de informatie over de toestemming voor de TCF API opgehaald en wordt vervolgens een gebeurtenis verzonden met de informatie over de toestemming die aan het XDM-schema is toegevoegd.

De andere manier om de toestemmingsinformatie aan elk verzoek toe te voegen is met [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) callback.

## Volgende stappen

Nu u hebt geleerd hoe u IAB TCF 2.0 met de uitbreiding van Experience Platform Web SDK kunt gebruiken, kunt u ook verkiezen om met andere oplossingen van Adobe zoals Adobe Analytics of Adobe Real-Time Customer Data Platform te integreren. Zie het [ IAB overzicht van de Transparantie &amp; van de Toestemming Kader 2.0 ](./overview.md) voor meer informatie.
