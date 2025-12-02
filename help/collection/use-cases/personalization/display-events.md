---
title: Weergavegebeurtenissen beheren in de Web SDK
description: Verklaart welke vertoningsgebeurtenissen zijn en hoe u hen in het Web SDK kunt gebruiken.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Weergavegebeurtenissen beheren in de Web SDK

De gebeurtenissen van de vertoning worden gebruikt door SDK van het Web om uw verpersoonlijking of analysedienst mee te delen wanneer een specifieke verpersoonlijkingsinhoud op een pagina wordt getoond. Als u weergavegebeurtenissen verzendt, wordt de nauwkeurigheid van personalisatiemetriek verbeterd en krijgt u een accuraat overzicht van wat de gebruikers op de pagina zien.

>[!NOTE]
>
>Weergavegebeurtenissen worden niet automatisch verzonden wanneer de functie `applyPropositions` wordt aangeroepen.

## Weergavegebeurtenissen automatisch verzenden

Als u weergavegebeurtenissen verzendt, worden automatisch nauwkeurigere analytische gegevens verkregen, aangezien de gebeurtenis direct wordt verzonden nadat de personalisatie is geladen. Deze implementatie beschikt ook over een meer gestroomlijnde implementatiemethode.

Om vertoningsgebeurtenissen automatisch te verzenden nadat de gepersonaliseerde inhoud op pagina wordt teruggegeven, moet u de volgende parameters vormen:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` of niet opgegeven

Web SDK verzendt de weergavegebeurtenissen direct nadat een personalisatie is gerenderd als resultaat van een `sendEvent` -aanroep.

## Weergavegebeurtenissen verzenden in volgende sendEvent-aanroepen

Wanneer u weergavegebeurtenissen opneemt in volgende `sendEvent` -aanroepen, kunt u in vergelijking met het automatisch verzenden van weergavegebeurtenissen ook meer informatie over het laden van de pagina in de aanroep opnemen. Dit kan extra informatie zijn, die niet beschikbaar was bij het aanvragen van de gepersonaliseerde inhoud.

Bovendien minimaliseert het verzenden van weergavegebeurtenissen in `sendEvent` -aanroepen de fout met de stuiterende frequentie wanneer u Adobe Analytics gebruikt.

>[!IMPORTANT]
>
>Wanneer u handmatig gerenderde voorstellingen gebruikt, worden weergavegebeurtenissen alleen ondersteund via `sendEvent` -aanroepen. In dit geval kunt u weergavegebeurtenissen niet automatisch verzenden.

### Weergavegebeurtenissen verzenden voor automatisch gerenderde profielen

Om vertoningsgebeurtenissen voor automatisch teruggegeven voorstellingen te verzenden, moet u de volgende parameters in de `sendEvent` vraag vormen:

* `renderDecisions: true`
* `personalization.sendDisplayEvent: false` voor de bovenkant van de paginakit

Roep `sendEvent` met `personalization.includeRenderedPropositions: true` aan om de weergavegebeurtenissen te verzenden

### Weergavegebeurtenissen verzenden voor handmatig gerenderde profielen

Als u weergavegebeurtenissen wilt verzenden voor handmatig weergegeven voorstellingen, moet u deze opnemen in het `_experience.decisioning.propositions` XDM-veld, inclusief de velden `id` , `scope` en `scopeDetails` van de voorstellingen.

Stel bovendien het veld `include _experience.decisioning.propositionEventType.display` in op `1` .
