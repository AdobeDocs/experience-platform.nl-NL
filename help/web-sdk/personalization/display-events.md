---
title: Weergavegebeurtenissen beheren in Web SDK
description: Dit artikel verklaart welke vertoningsgebeurtenissen zijn en hoe u hen in Web SDK kunt gebruiken.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Weergavegebeurtenissen beheren in Web SDK

De gebeurtenissen van de vertoning worden gebruikt door SDK van het Web om uw verpersoonlijking of analysedienst mee te delen wanneer een specifieke verpersoonlijkingsinhoud op een pagina wordt getoond.

Als u weergavegebeurtenissen verzendt, wordt de nauwkeurigheid van personalisatiemetriek verbeterd en krijgt u een accuraat overzicht van wat de gebruikers op de pagina zien.

Web SDK staat u toe om vertoningsgebeurtenissen op twee manieren te verzenden:

* [ automatisch ](#send-automatically), onmiddellijk nadat de gepersonaliseerde inhoud op de pagina wordt teruggegeven. Zie de documentatie over hoe te [ gepersonaliseerde inhoud ](rendering-personalization-content.md) voor meer informatie teruggeven.
* [ manueel ](#send-sendEvent-calls), door verdere `sendEvent` vraag.

>[!NOTE]
>
>Weergavegebeurtenissen worden niet automatisch verzonden wanneer de functie `applyPropositions` wordt aangeroepen.

## Weergavegebeurtenissen automatisch verzenden {#send-automatically}

Als u weergavegebeurtenissen verzendt, worden automatisch nauwkeurigere analytische gegevens verkregen, aangezien de gebeurtenis direct wordt verzonden nadat de personalisatie is geladen. Deze implementatie beschikt ook over een meer gestroomlijnde implementatiemethode.

Om vertoningsgebeurtenissen automatisch te verzenden nadat de gepersonaliseerde inhoud op pagina wordt teruggegeven, moet u de volgende parameters vormen:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` of niet opgegeven

Web SDK verzendt de vertoningsgebeurtenissen onmiddellijk nadat om het even welke verpersoonlijking als resultaat van een `sendEvent` vraag wordt teruggegeven.

## Weergavegebeurtenissen verzenden in volgende sendEvent-aanroepen {#send-sendEvent-calls}

Vergeleken met [ ](#send-automatically) het automatisch verzenden van vertoningsgebeurtenissen, wanneer u hen in verdere `sendEvent` vraag omvat hebt u ook de kans om meer informatie over de paginading in de vraag te omvatten. Dit kan extra informatie zijn, die niet beschikbaar was bij het aanvragen van de gepersonaliseerde inhoud.

Bovendien minimaliseert het verzenden van weergavegebeurtenissen in `sendEvent` -aanroepen de fout met de stuiterende frequentie wanneer u Adobe Analytics gebruikt.

>[!IMPORTANT]
>
>Wanneer u handmatig gerenderde voorstellingen gebruikt, worden weergavegebeurtenissen alleen ondersteund via `sendEvent` -aanroepen. In dit geval kunt u weergavegebeurtenissen niet automatisch verzenden.

### Weergavegebeurtenissen verzenden voor automatisch gerenderde profielen {#auto-rendered-propositions}

Om vertoningsgebeurtenissen voor automatisch teruggegeven voorstellingen te verzenden, moet u de volgende parameters in de `sendEvent` vraag vormen:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` voor de bovenkant van de paginakit

Roep `sendEvent` met `personalization.includeRenderedPropositions: true` aan om de weergavegebeurtenissen te verzenden

### Weergavegebeurtenissen verzenden voor handmatig gerenderde profielen {#manually-rendered-propositions}

Als u weergavegebeurtenissen wilt verzenden voor handmatig weergegeven voorstellingen, moet u deze opnemen in het `_experience.decisioning.propositions` XDM-veld, inclusief de velden `id` , `scope` en `scopeDetails` van de voorstellingen.

Stel bovendien het veld `include _experience.decisioning.propositionEventType.display` in op `1` .
