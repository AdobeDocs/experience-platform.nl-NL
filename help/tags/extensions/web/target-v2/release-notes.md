---
title: Opmerkingen bij de release Adobe Target v2 Extension
description: De meest recente release bevat informatie over de Adobe Target v2-tagextensie in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 644be95d9f90e20622c4f8ad68252ac57c09a288
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# Opmerkingen bij de release Adobe Target v2 Extension

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## 7 januari 2022

### Adobe Target v2 Extension 0.17.0

- Bijgewerkt voor ondersteuning van at.js v2.8.0, die nu het gebruik van functies en telemetriegegevens voor prestaties verzamelt.  Persoonlijke gegevens worden niet verzameld. Als u zich wilt afmelden voor deze functie, stelt u `telemetryEnabled` tot `false` in `targetGlobalSettings`.

## 28 oktober 2021

### Adobe Target v2-extensie 0.16.0

- Bijgewerkt voor ondersteuning op 0.js v2.7.0, nu beschikbaar voor downloaden vanaf Adobe Target.

## 20 juli 2021

### Adobe Target v2-extensie 0.15.1

- Probleem verholpen met een `stringify` functienaamsconflict, waardoor onjuiste UUID-waarden zijn gegenereerd voor `sessionId`, `requestId`, enzovoort.

## 16 juli 2021

### Adobe Target v2-extensie 0.15.0

- Veilige kenmerken aan cookies toevoegen wanneer de SecureOnly-instellingen van at.js op true zijn ingesteld
- Reactietokens zijn nu beschikbaar bij gebruik `triggerView()`
- Correctie van een fout met betrekking tot `CONTENT_RENDERING_NO_OFFERS` gebeurtenis. Nu wordt deze correct geactiveerd wanneer er geen inhoud is geretourneerd van Target
- A4T klik metrieke details correct zijn teruggekeerd wanneer het gebruiken van prefetch verzoeken
- UUID-generatie wordt niet langer gebruikt `Math.random()`, maar vertrouwt op `window.crypto`
- `sessionId` de vervaldatum van het koekje wordt correct uitgebreid op elke netwerkvraag
- SPA de initialisatie van het meningsgeheime voorgeheugen wordt nu correct behandeld en het houdt zich aan `viewsEnable` instellingen

## 2 juni 2021

### Adobe Target v2-extensie 0.14.2

- Los een insect op waar de definitieve bundel twee at.js versies, één met Op Apparaat Beslissing en één zonder bevat.

## 19 mei 2021

### Adobe Target v2-extensie 0.14.1

- Herstel de regressie die met versie 0.14 versie werd geïntroduceerd waar de actie van het Doel van de Lading globale mbox vraag vuurde

## 14 mei 2021

### Adobe Target v2-extensie 0.14

- Nieuwe handeling Doel laden toegevoegd met [Apparaatbeslissingen](./overview.md#load-target-with-on-device-decisioning), die bij.js 2.5 met de mogelijkheden van de Beslissing van het Apparaat laadt
- Bijgewerkt om.js tot 2.5


## 25 maart 2021

### Adobe Target v2-extensie 0.13.7

- Probleem verholpen met `targetPageParams` worden opgenomen in mbox-aanvragen. `targetPageParams` alleen worden opgenomen in `pageLoad` verzoeken.
- Probleem verholpen met globale document- en vensterobjecten in de tagextensie door algemene objectafhankelijkheden te vervangen door directe verwijzingen ernaar.
- Bijgewerkt om 1.js tot 2.4.1.

## 25 januari 2021

### Adobe Target v2-extensie 0.13.6

- Hiermee wordt ondersteuning voor één profiel/platform-id toegevoegd aan de levering-API van de klant
- Oplossing voor een ongeldige inspuiting van stijltags
- Bijgewerkt om 2.4.0
- Opgeloste kwestie waar de ongedefinieerde params in slechte leveringsverzoeken kunnen resulteren

## 25 november 2020

### Adobe Target v2-extensie 0.13.4

- Probleem verholpen waarbij mbox-parameters niet werden weergegeven in de gebruikersinterface
- Branding bijwerken
- De versie at.js is bijgewerkt naar versie 2.3.3

## 24 juli 2020

### Adobe Target v2-extensie 0.13.3

- Oplossing voor een probleem dat ervoor zorgde dat koppelingen in de QA-modus niet werkten voor inactieve activiteiten
- Het probleem waarbij een extensie mislukte als een script of code wordt toegevoegd, is opgelost. `default` aan de `window` of `document`

## 15 juni 2020

### Adobe Target v2-extensie 0.13.2

- Probleem verholpen bij het gebruik van CNAME en randoverschrijving, waarbij at.js 1.x het serverdomein mogelijk onjuist zou maken, wat tot gevolg had dat de aanvraag van het Doel mislukte
- Probleem verholpen waarbij Target de aanroep van Analytics sendBeacon vertraagde bij het gebruik van de v2-tagextensie voor de tagextensie Target en Adobe Analytics.
- Verbeterde `deviceIdLifetime` instellen door deze te overschrijven via `targetGlobalSettings`

## 25 maart 2020

### Adobe Target v2-extensie 0.13.0

- Bijgewerkt van 0.js tot v2.3.
- Toegevoegde ondersteuning voor algemene doelbox in adobe.target.getOffer-API
- Probleem verholpen waarbij params en params voor het laden van pagina&#39;s niet correct werden verwerkt

## 10 oktober 2019

### Adobe Target v2-extensie 0.12.0

- Bijgewerkt van 0.js tot v2.2.
- Verbeterde prestaties voor integratie tussen Experience Cloud ID-bibliotheek (ECID) v4.4 en at.js 2.2.
- Eerder deed de ECID-bibliotheek twee blokkerende oproepen voordat at.js ervaringen kon ophalen. Dit is verminderd tot één enkele vraag, die beduidend prestaties verbetert.

>[!NOTE]
>Voer een upgrade van de ECID-tagextensie uit naar v4.4.1 om te profiteren van deze prestatieverbetering.

## 31 juli 2019

### Adobe Target v2-extensie 0.11.1

- Bijgewerkte extensie-versie voor gebruik van at.js 2.1.1
- Een correctie toegevoegd voor het verwerken van parameters

## 3 juni 2019

### Adobe Target v2-extensie 0.11.0

- Nieuwe tagextensie voor ondersteuning van at.js 2.1
