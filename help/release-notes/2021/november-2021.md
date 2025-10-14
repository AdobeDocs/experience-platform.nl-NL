---
title: Aanvullende informatie voor Adobe Experience Platform, november 2021
description: Aanvullende informatie voor Adobe Experience platform, november 2021.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 14%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 17 november 2021**

## Nieuwe functies

Nieuwe functies in Adobe Experience Platform:

- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [(Beta) Activeer publiekssegmenten naar batchbestemmingen via de API voor ad-hocactivering](#ad-hoc-activation)

## Updates voor bestaande functies

Updates voor bestaande functies in Adobe Experience Platform:

- [Attributie-AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Real-Time Customer Data Platform B2B Edition {#B2B}

**Releasedatum: zaterdag 12 november 2021**

Real-Time CDP B2B edition is gebaseerd op Real-Time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.

Er zijn verbeteringen aangebracht in verschillende Adobe Experience Platform-mogelijkheden die Real-Time CDP B2B edition onderscheiden van zijn B2C-tegenhanger. Zij omvatten verbeteringen aan het Model van de Gegevens van de Ervaring (XDM) voor B2B gebruiksgevallen, verbeteringen aan identiteitsresolutie en profielsegmentatie, evenals een douane-gebouwde schakelaar en bestemming voor Marketo Engage. Met de Marketo-connector kunnen B2B-merken hun toonaangevende B2B-betrokkenheidsgegevens verbinden met gedragsinformatie om de leads te voeden en marketingactiviteiten op basis van account te verbeteren.

-[&#x200B; Nieuwe B2B en B2P uitgaven &#x200B;](#editions)
- [&#x200B; Nieuwe Marketo gegevensbron en bestemmingsschakelaars &#x200B;](#marketo)
-[&#x200B; Standaard B2B XDM &#x200B;](#XDM)

### Nieuwe B2B- en B2P-edities {#editions}

Nieuwe B2B- en B2P-edities die B2B-gegevens en -functionaliteit leveren aan zowel Real-Time CDP- als Experience Platform-activeringsproducten zijn verkrijgbaar.

Meer over Real-Time CDP B2B edition leren zie het [&#x200B; overzicht &#x200B;](../../rtcdp/overview.md).

### Nieuwe Marketo-gegevensbron en -bestemmingsconnectors {#marketo}

De nieuwe Marketo gegevensbron en bestemmingsschakelaars stromen Marketo gegevens naar Experience Platform en Experience Platform publiek terug naar Marketo. Beschikbaar voor alle Experience Platform-gebruikers.

| Functie | Beschrijving |
|----------|-------------|
| Marketo Engage-bronaansluiting | De [&#x200B; bron van Marketo Engage schakelaar &#x200B;](../../sources/connectors/adobe-applications/marketo/marketo.md) staat marketers toe om gegevens van één of meerdere instanties van Marketo in hun instantie van Adobe Experience Platform foutloos in te voeren en verstrekt een volledige oplossing voor loodbeheer en B2B marketers. |
| Marketo Engage-bestemming | De [&#x200B; bestemming van Marketo &#x200B;](../../destinations/catalog/adobe/marketo-engage.md) laat marketers toe om segmenten te duwen die in Adobe Experience Platform aan Marketo worden gecreeerd waar zij als statische lijsten zullen verschijnen. |

### Standaard B2B XDM {#XDM}

Standaard B2B XDM-klassen, veldgroepen en gegevenstypen zijn beschikbaar voor alle Experience Platform-gebruikers.

| Functie | Beschrijving |
|-----------|--------------|
| Standaard B2B XDM-klassen | Real-Time Customer Data Platform B2B edition biedt verschillende standaard XDM-codes die gegevens vastleggen over essentiële B2B-gegevensentiteiten, zoals accounts, mogelijkheden, campagnes en meer. |

Zie de [&#x200B; Schema&#39;s in Real-Time Customer Data Platform B2B edition &#x200B;](../../rtcdp/schemas/b2b.md) documentatie om meer te leren over het vangen van B2B gegevensentiteiten.

### (Beta) Activeer publiekssegmenten naar batchbestemmingen via de API voor ad-hocactivering {#ad-hoc-activation}

Met de API voor ad-hocactivering kunnen marketers publiekssegmenten programmatisch op een snelle en efficiënte manier naar doelen activeren voor situaties waarin onmiddellijke activering vereist is. Ad-hoc publieksactivering wordt slechts gesteund door [&#x200B; op dossier-gebaseerde bestemmingen &#x200B;](../../destinations/destination-types.md#file-based) en is momenteel in bèta. Voor meer informatie, zie de [&#x200B; ad-hoc documentatie van de activering API &#x200B;](../../destinations/api/ad-hoc-activation-api.md).

### Attributie-AI {#attribution-ai}

Attribution AI wordt gebruikt om credits toe te wijzen aan touchpoints die leiden tot conversiegebeurtenissen. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

| Functie | Beschrijving |
|-----------|---------------|
| Ondersteuning voor meerdere gegevenssets | Kenmerken AI kan nu gemakkelijk veelvoudige datasets direct in UI zonder de behoefte direct in kaart brengen en vastmaken elke dataset. Dit nieuwe tijdbesparende vermogen verstrekt krachtigere en nauwkeurige scores met rijkere gegevens van veelvoudige datasets. |
| Toewijzing van mediakanaal en campagneveld | Kenmerk AI ondersteunt nu het toewijzen van mediakanaal- en campagnevelden. De kanaaltoewijzing van media tussen datasets verbetert de inzichten die uit Attributie AI worden afgeleid en helpt duidelijkere resultaten verstrekken die gemakkelijk te interpreteren zijn. |

Voor meer informatie over Attributie AI, zie gelieve de [&#x200B; documentatie van AI van de Attributie &#x200B;](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

De in Real-Time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren. Dit wordt bereikt zonder de bedrijfsbehoeften te hoeven omzetten in een machine learning-probleem, een algoritme te kiezen, te trainen of te implementeren.

**Bijgewerkte functies**

| Functie | Beschrijving |
|-----------|-------------|
| Ondersteuning voor meerdere gegevenssets | KlantAI kan nu gemakkelijk meerdere gegevenssets rechtstreeks in de gebruikersinterface opnemen zonder dat elke gegevensset moet worden toegewezen en gekoppeld. Dit nieuwe tijdbesparende vermogen verstrekt krachtigere en nauwkeurige scores met rijkere gegevens van veelvoudige datasets. |
| Aangepaste profielkenmerken | De AI van de Klant steunt nu het bepalen van de gebieden van de gegevensreeks van het douaneprofiel (met timestamps) in uw gegevens naast standaardgebeurtenisgebieden. Met deze optie kunt u aanvullende profielkenmerken toevoegen die u van belang acht. Hierdoor kan de kwaliteit van het model worden verbeterd en kunnen de resultaten nauwkeuriger worden weergegeven. |

Voor meer informatie over Klant AI, te zien gelieve de [&#x200B; documentatie van AI van de Klant &#x200B;](../../intelligent-services/customer-ai/overview.md).
