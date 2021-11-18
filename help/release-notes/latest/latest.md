---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
source-git-commit: aa8cafc9a40748eda3098b2af732a828d39204b2
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 17 november 2021**

## Nieuwe functies

Nieuwe functies in Adobe Experience Platform:

- [Real-time Customer Data Platform B2B Edition](#B2B)

## Updates voor bestaande functies

Updates voor bestaande functies in Adobe Experience Platform:

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Real-time Customer Data Platform B2B Edition {#B2B}

**Releasedatum: 12 november 2021**

Gebaseerd op Real-time Customer Data Platform (Real-Time CDP), is de Echte - tijdCDP B2B Uitgave speciaal-gebouwd voor marketers die in een zaken-aan-zaken de dienstmodel werken. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen te betrekken.

Er zijn verbeteringen aan een verscheidenheid van de mogelijkheden van Adobe Experience Platform die Real-time CDP B2B Uitgave van zijn B2C tegenhanger onderscheiden. Zij omvatten verbeteringen aan het Model van de Gegevens van de Ervaring (XDM) voor B2B gebruiksgevallen, verbeteringen aan identiteitsresolutie en profielsegmentatie, evenals een douane-gebouwde schakelaar en bestemming voor Marketo Engage. Met de Marketo-connector kunnen B2B-merken hun toonaangevende B2B-betrokkenheidsgegevens verbinden met gedragsinformatie om de leads te voeden en marketingactiviteiten op basis van account te verbeteren.

-[Nieuwe B2B- en B2P-edities](#editions)
-[Nieuwe Marketo-gegevensbron en -bestemmingsconnectors](#marketo)
-[Standaard B2B XDM](#XDM)

### Nieuwe B2B- en B2P-edities {#editions}

Nieuwe B2B- en B2P-edities die B2B-gegevens en -functionaliteit opleveren voor CDP-producten en CDP-producten in realtime en producten voor activering van Platforms, kunnen worden aangeschaft.

Voor meer informatie over Real-time CDP B2B Edition raadpleegt u de [overzicht](../../rtcdp/overview.md).

### Nieuwe Marketo-gegevensbron en -bestemmingsconnectors {#marketo}

De nieuwe gegevensbron en bestemmingsschakelaars van Marketo stromen Marketo gegevens in Platform en Platform publiek terug naar Marketo. Beschikbaar voor alle gebruikers van het Platform.

| Functie | Beschrijving |
|----------|-------------|
| Marketo Engage-bronaansluiting | De [Marketo Engage-bronaansluiting](../../sources/connectors/adobe-applications/marketo/marketo.md) biedt marketers de mogelijkheid om naadloos gegevens van een of meer Marketo-instanties in hun Adobe Experience Platform-exemplaar in te voeren en biedt een volledige oplossing voor het beheer van leads en B2B-marketers. |
| Marketo Engage-bestemming | De [Marketo-bestemming](../../destinations/catalog/adobe/marketo-engage.md) stelt marketers in staat om segmenten die in Adobe Experience Platform zijn gemaakt, naar Marketo te verplaatsen waar ze als statische lijsten worden weergegeven. |

### Standaard B2B XDM {#XDM}

De standaard B2B klassen XDM, gebiedsgroepen, en gegevenstypes zijn beschikbaar voor alle gebruikers van het Platform.

| Functie | Beschrijving |
|-----------|--------------|
| Standaard B2B XDM-klassen | Real-time Customer Data Platform B2B Edition biedt verschillende standaard XDM-kaarten die gegevens vastleggen over essentiële B2B-gegevensentiteiten, zoals accounts, mogelijkheden, campagnes en meer. |

Zie de [Schemas in Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) documentatie voor meer informatie over het vastleggen van B2B-gegevensentiteiten.

### Attribution AI {#attribution-ai}

Attribution AI wordt gebruikt om credits toe te wijzen aan aanraakpunten die leiden tot conversiegebeurtenissen. Dit kan door marketers worden gebruikt om het marketing effect van elk individueel marketing aanraakpunt over klantenreizen te kwantificeren.

| Functie | Beschrijving |
|-----------|---------------|
| Ondersteuning voor meerdere gegevenssets | Attribution AI kan nu gemakkelijk veelvoudige datasets direct in UI zonder de behoefte direct in kaart brengen en vastmaken elke dataset. Dit nieuwe tijdbesparende vermogen verstrekt krachtigere en nauwkeurige scores met rijkere gegevens van veelvoudige datasets. |
| Toewijzing van mediakanaal en campagneveld | Attribution AI ondersteunt nu de toewijzing van mediakanalen en campagnevelden. De kanaaltoewijzing van media tussen datasets verbetert de inzichten die uit Attribution AI worden afgeleid en helpt duidelijkere resultaten verstrekken die gemakkelijk te interpreteren zijn. |

Zie voor meer informatie over Attribution AI de [Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

De in Real-time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren. Dit wordt verwezenlijkt zonder het moeten de bedrijfsbehoeften aan een machine het leren probleem omzetten, een algoritme kiezen, opleiden, of opstellen.

**Bijgewerkte functies**

| Functie | Beschrijving |
|-----------|-------------|
| Ondersteuning voor meerdere gegevenssets | KlantAI kan nu gemakkelijk meerdere gegevenssets rechtstreeks in de gebruikersinterface opnemen zonder dat elke gegevensset moet worden toegewezen en gekoppeld. Dit nieuwe tijdbesparende vermogen verstrekt krachtigere en nauwkeurige scores met rijkere gegevens van veelvoudige datasets. |
| Aangepaste profielkenmerken | De AI van de Klant steunt nu het bepalen van de gebieden van de gegevensreeks van het douaneprofiel (met timestamps) in uw gegevens naast standaardgebeurtenisgebieden. Met deze optie kunt u aanvullende profielkenmerken toevoegen die u van belang acht. Hierdoor kan de kwaliteit van het model worden verbeterd en kunnen de resultaten nauwkeuriger worden weergegeven. |

Voor meer informatie over AI van de Klant, gelieve te zien [AI-documentatie van klant](../../intelligent-services/customer-ai/overview.md).
