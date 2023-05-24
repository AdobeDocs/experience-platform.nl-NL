---
title: Opmerkingen bij de release van Adobe Experience Platform november 2021
description: De release van november 2021 bevat notities voor Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 9%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 17 november 2021**

## Nieuwe functies

Nieuwe functies in Adobe Experience Platform:

- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [(bèta) Activeer publiekssegmenten naar batchbestemmingen via de API voor ad-hocactivering](#ad-hoc-activation)

## Updates voor bestaande functies

Updates voor bestaande functies in Adobe Experience Platform:

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Real-Time Customer Data Platform B2B Edition {#B2B}

**Releasedatum: 12 november 2021**

Real-Time CDP B2B Edition is gebaseerd op Real-time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen te betrekken.

Er zijn verbeteringen aangebracht in verschillende Adobe Experience Platform-mogelijkheden die Real-Time CDP B2B Edition onderscheiden van de B2C-tegenhanger. Zij omvatten verbeteringen aan het Model van de Gegevens van de Ervaring (XDM) voor B2B gebruiksgevallen, verbeteringen aan identiteitsresolutie en profielsegmentatie, evenals een douane-gebouwde schakelaar en bestemming voor Marketo Engage. Met de Marketo-connector kunnen B2B-merken hun toonaangevende B2B-betrokkenheidsgegevens verbinden met gedragsinformatie om de leads te voeden en marketingactiviteiten op basis van account te verbeteren.

-[Nieuwe B2B- en B2P-edities](#editions)
-[Nieuwe Marketo-gegevensbron en -bestemmingsconnectors](#marketo)
-[Standaard B2B XDM](#XDM)

### Nieuwe B2B- en B2P-edities {#editions}

Nieuwe B2B- en B2P-edities die B2B-gegevens en -functionaliteit leveren aan zowel Real-Time CDP- als Platform Activation-producten zijn verkrijgbaar.

Voor meer informatie over de Real-Time CDP B2B Edition raadpleegt u de [overzicht](../../rtcdp/overview.md).

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

### (bèta) Activeer publiekssegmenten naar batchbestemmingen via de API voor ad-hocactivering {#ad-hoc-activation}

Met de API voor ad-hocactivering kunnen marketers publiekssegmenten programmatisch op een snelle en efficiënte manier naar doelen activeren voor situaties waarin onmiddellijke activering vereist is. Activering van ad-hocgroepen wordt alleen ondersteund door [batchbestandsgebaseerde doelen](../../destinations/destination-types.md#file-based) en is momenteel in bèta. Zie voor meer informatie de [API-documentatie voor ad-hocactivering](../../destinations/api/ad-hoc-activation-api.md).

### Attribution AI {#attribution-ai}

Attribution AI wordt gebruikt om credits toe te wijzen aan touchpoints die leiden tot conversiegebeurtenissen. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

| Functie | Beschrijving |
|-----------|---------------|
| Ondersteuning voor meerdere gegevenssets | Attribution AI kan nu gemakkelijk veelvoudige datasets direct in UI zonder de behoefte direct in kaart brengen en vastmaken elke dataset. Dit nieuwe tijdbesparende vermogen verstrekt krachtigere en nauwkeurige scores met rijkere gegevens van veelvoudige datasets. |
| Toewijzing van mediakanaal en campagneveld | Attribution AI ondersteunt nu de toewijzing van mediakanalen en campagnevelden. De kanaaltoewijzing van media tussen datasets verbetert de inzichten die uit Attribution AI worden afgeleid en helpt duidelijkere resultaten verstrekken die gemakkelijk te interpreteren zijn. |

Zie voor meer informatie over Attribution AI de [Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

De in Real-time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren. Dit wordt bereikt zonder de bedrijfsbehoeften te hoeven omzetten in een machine learning-probleem, een algoritme te kiezen, te trainen of te implementeren.

**Bijgewerkte functies**

| Functie | Beschrijving |
|-----------|-------------|
| Ondersteuning voor meerdere gegevenssets | KlantAI kan nu gemakkelijk meerdere gegevenssets rechtstreeks in de gebruikersinterface opnemen zonder dat elke gegevensset moet worden toegewezen en gekoppeld. Dit nieuwe tijdbesparende vermogen verstrekt krachtigere en nauwkeurige scores met rijkere gegevens van veelvoudige datasets. |
| Aangepaste profielkenmerken | De AI van de Klant steunt nu het bepalen van de gebieden van de gegevensreeks van het douaneprofiel (met timestamps) in uw gegevens naast standaardgebeurtenisgebieden. Met deze optie kunt u aanvullende profielkenmerken toevoegen die u van belang acht. Hierdoor kan de kwaliteit van het model worden verbeterd en kunnen de resultaten nauwkeuriger worden weergegeven. |

Voor meer informatie over AI van de Klant, gelieve te zien [AI-documentatie van klant](../../intelligent-services/customer-ai/overview.md).
