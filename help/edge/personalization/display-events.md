---
title: Weergavegebeurtenissen beheren in Web SDK
description: Dit artikel wat vertoningsgebeurtenissen zijn en hoe zij in Web SDK werken.
source-git-commit: 221a9348803e111a1842b3abf2e74f7408da5994
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Weergavegebeurtenissen beheren in Web SDK

De gebeurtenissen van de vertoning worden gebruikt door SDK van het Web om uw verpersoonlijking of analysedienst mee te delen wanneer een specifieke verpersoonlijkingsinhoud op een pagina wordt getoond.

Als u weergavegebeurtenissen verzendt, wordt de nauwkeurigheid van personalisatiemetriek verbeterd en krijgt u een accuraat overzicht van wat de gebruikers op de pagina zien.

Web SDK staat u toe om vertoningsgebeurtenissen op twee manieren te verzenden:

* [Automatisch](#send-automatically), onmiddellijk nadat de gepersonaliseerde inhoud op de pagina wordt weergegeven. Zie de documentatie over hoe u [persoonlijke inhoud renderen](rendering-personalization-content.md) voor meer informatie .
* [Handmatig](#send-sendEvent-calls), via `sendEvent` oproepen.

>[!NOTE]
>
>Weergavegebeurtenissen worden niet automatisch verzonden wanneer de `applyPropositions` functie.

## Weergavegebeurtenissen automatisch verzenden {#send-automatically}

Als u weergavegebeurtenissen verzendt, worden automatisch nauwkeurigere analytische gegevens verkregen, aangezien de gebeurtenis direct wordt verzonden nadat de personalisatie is geladen. Deze implementatie beschikt ook over een meer gestroomlijnde implementatiemethode.

Om vertoningsgebeurtenissen automatisch te verzenden nadat de gepersonaliseerde inhoud op pagina wordt teruggegeven, moet u de volgende parameters vormen:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` of niet opgegeven

Web SDK verzendt de vertoningsgebeurtenissen onmiddellijk nadat om het even welke verpersoonlijking als resultaat van een `sendEvent` vraag.

## Weergavegebeurtenissen verzenden in volgende sendEvent-aanroepen {#send-sendEvent-calls}

Vergeleken met [automatisch](#send-automatically) verzenden, weergavegebeurtenissen wanneer u deze opneemt in volgende `sendEvent` vraag u hebt ook de kans om meer informatie over de paginading in de vraag te omvatten. Dit kan extra informatie zijn, die niet beschikbaar was bij het aanvragen van de gepersonaliseerde inhoud.

Bovendien worden weergavegebeurtenissen verzonden in `sendEvent` De vraag minimaliseert stuit-tarief fouten wanneer het gebruiken van Adobe Analytics.

>[!IMPORTANT]
>
>Weergavegebeurtenissen worden alleen ondersteund via handmatig gerenderde voorstellingen `sendEvent` oproepen. In dit geval kunt u weergavegebeurtenissen niet automatisch verzenden.

### Weergavegebeurtenissen verzenden voor automatisch gerenderde profielen {#auto-rendered-propositions}

Om vertoningsgebeurtenissen voor automatisch teruggegeven voorstellingen te verzenden, moet u de volgende parameters in vormen `sendEvent` oproep:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` voor de bovenkant van de pagina treffend

Om de vertoningsgebeurtenissen te verzenden, roep `sendEvent` with `personalization.includePendingDisplayNotifications: true`

### Weergavegebeurtenissen verzenden voor handmatig gerenderde profielen {#manually-rendered-propositions}

Als u weergavegebeurtenissen wilt verzenden voor handmatig gerenderde voorstellingen, moet u deze opnemen in het dialoogvenster `_experience.decisioning.propositions` XDM-veld, inclusief de `id`, `scope`, en `scopeDetails` velden van de voorstellen.

Stel bovendien de `include _experience.decisioning.propositionEventType.display` veld naar `1`.