---
title: Opmerkingen bij de release Adobe Target v2 Extension
description: De meest recente release bevat informatie over de Adobe Target v2-tagextensie in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 3f6526ec87189d6e629d4dcb8eb626367543b9e5
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Opmerkingen bij de release Adobe Target v2-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## v0.18.0 (1 juni 2022)

- Bijgewerkt voor ondersteuning `at.js` v2.9.0
- Ondersteuning voor Client Hints voor toegevoegde gebruikersagent.

## v0.17.1 (28 januari 2022)

- Bijgewerkt voor ondersteuning `at.js` v2.8.1
- Vast `pageLoad` niet toegewezen aan `target-global-mbox` in de hybride ODD-uitvoeringsmodus
- Probleem verholpen met details over analyses voor `mbox` verzoek
- Verbeterde dev-afhankelijkheden om beveiligingskwetsbaarheden te verhelpen

## v0.17.0 (7 januari 2022)

- Bijgewerkt voor ondersteuning `at.js` v2.8.0, dat nu het gebruik van functies en prestaties telemetriegegevens verzamelt.  Persoonlijke gegevens worden niet verzameld. Als u zich wilt afmelden voor deze functie, stelt u `telemetryEnabled` tot `false` in `targetGlobalSettings`.

## v0.16.0 (28 oktober 2021)

- Bijgewerkt voor ondersteuning `at.js` v2.7.0, nu beschikbaar voor downloaden vanaf Adobe Target.

## v0.15.1 (20 juli 2021)

- Probleem verholpen met een `stringify` functienaamsconflict, waardoor onjuiste UUID-waarden zijn gegenereerd voor `sessionId`, `requestId`, enzovoort.

## v0.15.0 (16 juli 2021)

- Veilige kenmerken aan cookies toevoegen wanneer `at.js` settings secureOnly is ingesteld op true
- Reactietokens zijn nu beschikbaar bij gebruik `triggerView()`
- Correctie van een fout met betrekking tot `CONTENT_RENDERING_NO_OFFERS` gebeurtenis. Nu wordt deze correct geactiveerd wanneer er geen inhoud is geretourneerd van Target
- A4T klik metrieke details correct zijn teruggekeerd wanneer het gebruiken van prefetch verzoeken
- UUID-generatie wordt niet langer gebruikt `Math.random()`, maar vertrouwt op `window.crypto`
- `sessionId` de vervaldatum van het koekje wordt correct uitgebreid op elke netwerkvraag
- SPA de initialisatie van het meningsgeheime voorgeheugen wordt nu correct behandeld en het houdt zich aan `viewsEnable` instellingen

## v0.14.2 (2 juni 2021)

- Een probleem verhelpen waarbij de uiteindelijke bundel twee elementen bevat `at.js` versies, één met On-Device Decisioning en één zonder.

## v0.14.1 (19 mei 2021)

- Herstel de regressie die met versie 0.14 versie werd geïntroduceerd waar de actie van het Doel van de Lading globale mbox vraag vuurde

## v0.14 (14 mei 2021)

- Nieuwe handeling Doel laden toegevoegd met [Apparaatbeslissingen](./overview.md#load-target-with-on-device-decisioning), die wordt geladen `at.js` 2.5 met beslissingsmogelijkheden op het apparaat
- Bijgewerkt `at.js` tot en met 2,5


## v0.13.7 (25 maart 2021)

- Probleem verholpen met `targetPageParams` worden opgenomen in mbox-aanvragen. `targetPageParams` alleen worden opgenomen in `pageLoad` verzoeken.
- Probleem verholpen met globale document- en vensterobjecten in de tagextensie door algemene objectafhankelijkheden te vervangen door directe verwijzingen ernaar.
- Bijgewerkt `at.js` tot en met 2.4.1.

## v0.13.6 (25 januari 2021)

- Hiermee wordt ondersteuning voor één profiel/platform-id toegevoegd aan de levering-API van de klant
- Oplossing voor een ongeldige inspuiting van stijltags
- Bijgewerkt om 2.4.0
- Opgeloste kwestie waar de ongedefinieerde params in slechte leveringsverzoeken kunnen resulteren

## v0.13.4 (25 november 2020)

- Probleem verholpen waarbij mbox-parameters niet werden weergegeven in de gebruikersinterface
- Branding bijwerken
- De `at.js` versie naar 2.3.3

## v0.13.3 (24 juli 2020)

- Oplossing voor een probleem dat ervoor zorgde dat koppelingen in de QA-modus niet werkten voor inactieve activiteiten
- Het probleem waarbij een extensie mislukte als een script of code wordt toegevoegd, is opgelost. `default` aan de `window` of `document`

## v0.13.2 (15 juni 2020)

- Probleem verholpen bij gebruik van CNAME en randoverschrijving, waarbij `at.js` 1.x zou tot het serverdomein verkeerd kunnen leiden, resulterend in het ontbreken van het verzoek van het Doel
- Probleem verholpen waarbij Target de aanroep van Analytics sendBeacon vertraagde bij het gebruik van de v2-tagextensie voor de tagextensie Target en Adobe Analytics.
- Verbeterde `deviceIdLifetime` instellen door deze te overschrijven via `targetGlobalSettings`

## v0.13.0 (25 maart 2020)

- Bijgewerkt `at.js` tot en met v2.3.
- Toegevoegde ondersteuning voor algemene doelbox in adobe.target.getOffer-API
- Probleem verholpen waarbij params en params voor het laden van pagina&#39;s niet correct werden verwerkt

## v0.12.0 (10 oktober 2019)

- Bijgewerkt `at.js` tot en met v2.2.
- Verbeterde prestaties voor integratie tussen Experience Cloud ID-bibliotheek (ECID) v4.4 en `at.js` 2.2
- Eerder deed de ECID-bibliotheek twee blokkerende oproepen voordat `at.js` kan ervaringen opdoen. Dit is verminderd tot één enkele vraag, die beduidend prestaties verbetert.

>[!NOTE]
>Voer een upgrade van de ECID-tagextensie uit naar v4.4.1 om te profiteren van deze prestatieverbetering.

## v0.11.1 (31 juli 2019)

- Bijgewerkte extensieversie voor gebruik `at.js` 2.1.1.
- Een correctie toegevoegd voor het verwerken van parameters

## v0.11.0 (3 juni 2019)

- Nieuwe tagextensie die wordt ondersteund `at.js` 2,1
