---
title: Opmerkingen bij de release Adobe Target v2 Extension
description: De meest recente release bevat informatie over de Adobe Target v2-tagextensie in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Opmerkingen bij de release Adobe Target v2-extensie

## v0.20.3 (23 januari 2024)

- Bijgewerkt ter ondersteuning van `at.js` 2.11.4
- Het probleem waarbij er geen ongeldige geo-gegevens naar de API voor levering werden verzonden, is opgelost.

## v0.20.2 (29 november 2023)

- Bijgewerkt ter ondersteuning van `at.js` 2.11.3
- Oplossing voor een probleem dat ervoor zorgde dat er geen antwoordtokens werden verzonden bij &#39;at-content-rendering-failed&#39;-gebeurtenissen.

## v0.20.1 (3 november 2023)

- Bijgewerkt ter ondersteuning van `at.js` 2.11.2.
- Oplossing voor een bug die inconsistenties veroorzaakte in de reactietokens die op aangepaste gebeurtenissen werden verzonden.

## v0.20.0 (9 oktober 2023)

- Bijgewerkt ter ondersteuning van `at.js` 2.11.0.
- Toegevoegde ondersteuning voor het instellen van aangepaste Adobe Experience Platform-sandboxId en sandboxName in targetGlobalSettings, die wordt doorgegeven aan Delivery API voor aanroepen van getOffer/getOffers.
- Schaduw-DOM-correctie voor ketting van :eq() in kiezer.

## v0.19.3 (18 september 2023)

- Bijgewerkt ter ondersteuning van `at.js` v2.10.3.
- Probleem verholpen waarbij de aangepaste gebeurtenis &#39;at-content-rendering-Succesvol&#39; onjuist werd geactiveerd wanneer geen aanbiedingen worden weergegeven. De juiste gebeurtenis, at-content-rendering-no-aanbiedingen, wordt nu geactiveerd.
- Gebeurtenistoken en responseTokens zijn toegevoegd aan het foutobject voor de aangepaste gebeurtenis at-content-rendering-failed.

## v0.19.2 (14 februari 2023)

- Probleem verholpen waarbij de time-out kon worden ingesteld op een gegevenselement.

## v0.19.1 (3 februari 2023)

- Bijgewerkt voor ondersteuning van `at.js` v2.10.1
- Aangepaste Mbox-parameters van de client ondersteunen nu de puntnotatie correct
- Oproepen tot levering niet meer in VEC

## v0.19.0 (19 september 2022)

- Bijgewerkt voor ondersteuning van `at.js` v2.10.0
- Ondersteuning voor interdomeintracering toegevoegd.

## v0.18.0 (1 juni 2022)

- Bijgewerkt voor ondersteuning van `at.js` v2.9.0
- Ondersteuning voor Client Hints voor toegevoegde gebruikersagent.

## v0.17.1 (28 januari 2022)

- Bijgewerkt voor ondersteuning van `at.js` v2.8.1
- Fixed `pageLoad` wordt niet toegewezen aan `target-global-mbox` in ODD hybride uitvoeringsmodus
- Probleem verholpen met analytische details voor `mbox` aanvraag
- Verbeterde dev-afhankelijkheden om beveiligingskwetsbaarheden te verhelpen

## v0.17.0 (7 januari 2022)

- Bijgewerkt ter ondersteuning van `at.js` v2.8.0, die nu het gebruik van functies en telemetriegegevens voor prestaties verzamelt.  Persoonlijke gegevens worden niet verzameld. Als u deze functie wilt uitschakelen, stelt u `telemetryEnabled` in op `false` in `targetGlobalSettings` .

## v0.16.0 (28 oktober 2021)

- Bijgewerkt ter ondersteuning van `at.js` v2.7.0, nu beschikbaar voor downloaden vanaf Adobe Target.

## v0.15.2 (16 augustus 2021)

- Bijgewerkt ter ondersteuning van `at.js` 2.6.1.
- Initialiseer op apparaat beslissingen bij opstarten onafhankelijk van de gebeurtenis Pagina laden.
- De beslissing op het apparaat kan nu worden gebruikt tijdens het eerste bezoek nadat het artefact is gedownload.

## v0.15.1 (20 juli 2021)

- Probleem verholpen met een functienaamconflict `stringify` , dat ertoe leidde dat onjuiste UUID-waarden werden gegenereerd voor `sessionId` , `requestId` , enzovoort.

## v0.15.0 (16 juli 2021)

- Veilig kenmerk toevoegen aan cookies wanneer `at.js` settings secureOnly is ingesteld op true
- Responstokens zijn nu beschikbaar wanneer u `triggerView()` gebruikt
- Het probleem met `CONTENT_RENDERING_NO_OFFERS` -gebeurtenissen is opgelost. Nu wordt deze correct geactiveerd wanneer er geen inhoud is geretourneerd van Target
- A4T klik metrieke details correct zijn teruggekeerd wanneer het gebruiken van prefetch verzoeken
- Bij het genereren van UID wordt niet langer `Math.random()` gebruikt, maar wordt `window.crypto` gebruikt
- `sessionId` vervaldatum van cookie wordt correct verlengd bij elke netwerkaanroep
- De initialisatie van het cachegeheugen van de SPA-weergave wordt nu correct afgehandeld en voldoet aan `viewsEnable` -instellingen

## v0.14.2 (2 juni 2021)

- Los een fout op waar de definitieve bundel twee `at.js` versies bevat, één met Beslissing op Apparaat en één zonder.

## v0.14.1 (19 mei 2021)

- Herstel de regressie die met versie 0.14 versie werd geïntroduceerd waar de actie van het Doel van de Lading globale mbox vraag vuurde

## v0.14 (14 mei 2021)

- Toegevoegd een nieuw doel van de actielading met [ Beslissing op Apparaat ](./overview.md#load-target-with-on-device-decisioning), dat {2.5 met de mogelijkheden van het Beslissen op Apparaat laadt`at.js`
- Bijgewerkt `at.js` naar 2.5


## v0.13.7 (25 maart 2021)

- Probleem verholpen waarbij `targetPageParams` werd opgenomen in mbox-aanvragen. `targetPageParams` mag alleen worden opgenomen in `pageLoad` -aanvragen.
- Probleem verholpen met globale document- en vensterobjecten in de tagextensie door algemene objectafhankelijkheden te vervangen door directe verwijzingen ernaar.
- Bijgewerkt `at.js` naar 2.4.1.

## v0.13.6 (25 januari 2021)

- Hiermee wordt ondersteuning voor één profiel/platform-id toegevoegd aan de levering-API van de klant
- Oplossing voor een ongeldige inspuiting van stijltags
- Bijgewerkt om 2.4.0
- Opgeloste kwestie waar de ongedefinieerde params in slechte leveringsverzoeken kunnen resulteren

## v0.13.4 (25 november 2020)

- Probleem verholpen waarbij mbox-parameters niet werden weergegeven in de gebruikersinterface
- Branding bijwerken
- De versie van `at.js` is bijgewerkt naar versie 2.3.3

## v0.13.3 (24 juli 2020)

- Oplossing voor een probleem dat ervoor zorgde dat koppelingen in de QA-modus niet werkten voor inactieve activiteiten
- Het probleem waarbij de extensie mislukte wanneer een script of code de eigenschap `default` toevoegt aan de eigenschap `window` of `document` , is opgelost.

## v0.13.2 (15 juni 2020)

- Probleem verholpen bij het gebruik van CNAME en randoverschrijving, waarbij `at.js` 1.x het serverdomein mogelijk onjuist maakt, waardoor de aanvraag voor Doel mislukt is. Dit probleem is nu opgelost.
- Probleem verholpen waarbij Target de aanroep van Analytics sendBeacon vertraagde bij het gebruik van de v2-tagextensie voor de tagextensie Target en Adobe Analytics.
- De instelling `deviceIdLifetime` is verbeterd doordat deze kan worden overschreven via `targetGlobalSettings` .

## v0.13.0 (25 maart 2020)

- Bijgewerkt `at.js` naar v2.3.
- Toegevoegde ondersteuning voor algemene doelbox in adobe.target.getOffer-API
- Probleem verholpen waarbij params en params voor het laden van pagina&#39;s niet correct werden verwerkt

## v0.12.0 (10 oktober 2019)

- Bijgewerkt `at.js` naar v2.2.
- Verbeterde prestaties voor integratie tussen Experience Cloud ID library (ECID) v4.4 en `at.js` 2.2.
- Eerder deed de ECID-bibliotheek twee blokkerende aanroepen voordat `at.js` ervaringen kon opdoen. Dit is verminderd tot één enkele vraag, die beduidend prestaties verbetert.

>[!NOTE]
>Voer een upgrade van de ECID-tagextensie uit naar v4.4.1 om te profiteren van deze prestatieverbetering.

## v0.11.1 (31 juli 2019)

- Bijgewerkte extensieversie voor gebruik van `at.js` 2.1.1
- Een correctie toegevoegd voor het verwerken van parameters

## v0.11.0 (3 juni 2019)

- Nieuwe tagextensie ter ondersteuning van `at.js` 2.1
