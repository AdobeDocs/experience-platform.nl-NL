---
title: Opmerkingen bij de release Adobe Target v2 Extension
description: De meest recente release bevat informatie over de Adobe Target v2-tagextensie in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# Opmerkingen bij de release Adobe Target v2 Extension

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## 20 juli 2021

### Adobe Target v2-extensie 0.15.1

- Probleem verholpen met een functienaamconflict `stringify`, dat ertoe leidde dat onjuiste UUID-waarden werden gegenereerd voor `sessionId`, `requestId` enzovoort.

## 16 juli 2021

### Adobe Target v2-extensie 0.15.0

- Veilige kenmerken aan cookies toevoegen wanneer de SecureOnly-instellingen van at.js op true zijn ingesteld
- Reactietokens zijn nu beschikbaar wanneer u `triggerView()` gebruikt
- Oplossing voor een fout met betrekking tot de gebeurtenis `CONTENT_RENDERING_NO_OFFERS`. Nu wordt deze correct geactiveerd wanneer er geen inhoud is geretourneerd van Target
- A4T klik metrieke details correct zijn teruggekeerd wanneer het gebruiken van prefetch verzoeken
- UUID-generatie gebruikt `Math.random()` niet meer, maar is afhankelijk van `window.crypto`
- `sessionId` de vervaldatum van het koekje wordt correct uitgebreid op elke netwerkvraag
- SPA de initialisatie van het weergavecache wordt nu correct afgehandeld en voldoet aan de `viewsEnable`-instellingen

## 2 juni 2021

### Adobe Target v2-extensie 0.14.2

- Los een insect op waar de definitieve bundel twee at.js versies, één met Op Apparaat Beslissing en één zonder bevat.

## 19 mei 2021

### Adobe Target v2-extensie 0.14.1

- Herstel de regressie die met versie 0.14 versie werd geïntroduceerd waar de actie van het Doel van de Lading globale mbox vraag vuurde

## 14 mei 2021

### Adobe Target v2-extensie 0.14

- Een nieuwe handeling Load Target with [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning) toegevoegd, die wordt geladen op 0,js 2.5 met mogelijkheden voor het bepalen van het apparaat
- Bijgewerkt om.js tot 2.5


## 25 maart 2021

### Adobe Target v2-extensie 0.13.7

- Probleem verholpen waarbij `targetPageParams` was opgenomen in mbox-aanvragen. `targetPageParams` uitsluitend in  `pageLoad` verzoeken worden opgenomen.
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
- Het probleem waarbij de extensie mislukte als een script of code `default`-eigenschap toevoegt aan `window` of `document` is opgelost.

## 15 juni 2020

### Adobe Target v2-extensie 0.13.2

- Probleem verholpen bij het gebruik van CNAME en randoverschrijving, waarbij at.js 1.x het serverdomein mogelijk onjuist zou maken, wat tot gevolg had dat de aanvraag van het Doel mislukte
- Probleem verholpen waarbij Target de aanroep van Analytics sendBeacon vertraagde bij het gebruik van de v2-tagextensie voor de tagextensie Target en Adobe Analytics.
- De instelling `deviceIdLifetime` is verbeterd doordat deze via `targetGlobalSettings` kan worden overschreven

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
