---
title: Architectuurupgrades naar Real-Time CDP B2B edition
description: Lees dit document voor meer informatie over de uitgebreide architectuurupgrades naar Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: da288d1a917df85b3c003bc6592fda7a6f1eafe7
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Architectuuropties naar Real-Time CDP B2B edition

>[!IMPORTANT]
>
>In dit document worden architectuurupgrades naar Real-Time CDP B2B en B2P Editions beschreven. Voor de upgrades zijn geen acties van de meeste klanten vereist. Er zijn echter soorten publiek die niet automatisch kunnen worden bijgewerkt. Adobe werkt rechtstreeks met u samen om deze scenario&#39;s aan te pakken. Raadpleeg dit document voor informatie over de gevolgen van de upgrades voor de bestaande functies van Adobe Experience Platform. Neem contact op met uw Adobe-accountteam als u vragen hebt.

Adobe heeft de Real-Time CDP B2B- en B2P-edities opnieuw ontworpen om de schaalbaarheid, prestaties en betrouwbaarheid te verbeteren, en ondersteunt ook meer geavanceerde B2B-gebruiksscenario&#39;s. Om ervoor te zorgen dat alle klanten van deze verbeteringen profiteren, zal Adobe alle bestaande B2B- en B2P-klanten upgraden naar de nieuwe architectuur.

Gebruik de verbeterde architectuur voor de volgende voordelen:

* **Schaalbaarheid van gegevensopname**: Verbeterde steun voor high-cardinality B2B verhoudingen, zoals rekeningen die met duizenden mensen worden verbonden.
* **Krachtige en betrouwbare publieksevaluatie**: Snellere en veerkrachtigere segmentatie voor complex B2B publiek.
* **entiteitresolutie**: Verbeterde identiteitsresolutie voor B2B entiteiten, verbeterde gegevenskwaliteit, en verminderde duplicatie om nauwkeurigere segmentatie en samenvoeging toe te laten.

## Nieuwe functies

Lees het volgende voor zeer belangrijke verhogingen inbegrepen in de architecturale verbetering.

### Account-momentopnamen voor doelgroeplidmaatschap

Met de nieuwe B2B-architectuur worden de details van het publiekslidmaatschap nu opgenomen voor accountentiteiten in momentopnameleverporten. Met deze functie hebt u toegang tot de publieksstatus op accountniveau, tijdstempels en lidmaatschapsindicatoren.

Met deze upgrade kunt u nu:

* Schakel marketing- en operatieteams in om het lidmaatschap van het accountpubliek rechtstreeks te valideren.
* Benader de pariteit tussen uw profiel (persoon) en de modellen van de rekeningssegmentatie van de rekening, die verenigbare ervaring over entiteiten verzekeren.

Lees de documentatie over [&#x200B; rekeningspubliek &#x200B;](../segmentation/types/account-audiences.md) voor meer informatie.

### Aantallen van het publiek voor soorten publiek die B2B-entiteiten omvatten

Schattingen van de omvang van het publiek voor soorten publiek met B2B-entiteiten worden nu precies berekend. Deze schattingen zijn beschikbaar tijdens de voorvertoning en bieden nauwkeurigere en betrouwbaardere inzichten voor het publiek dat complexe B2B-relaties omvat.

Met deze upgrade kunt u nu:

* Gebruik inzichten van nauwkeurige schattingen van de omvang van het publiek om de planning en besluitvorming tijdens het maken van het publiek te verbeteren.
* Ontwerp op betrouwbare wijze complexe B2B-doelgroepen, met kennis van nauwkeurigere publieksschattingen.
* Verbeter een slimmere campagneplanning, nauwkeurigere gerichtheid, en betere middelentoewijzing.

Lees de documentatie over [&#x200B; rekeningspubliek &#x200B;](../segmentation/types/account-audiences.md) voor meer informatie.

## Verbeteringen aan bestaande functies

De volgende functies zijn bijgewerkt als onderdeel van de B2B-architectuurupgrades.

### Updates voor publiek met meerdere entiteiten met B2B-kenmerken en Experience Events

Als onderdeel van de nieuwe architectuurupgrade kunnen de filters van de Gebeurtenis van de Ervaring niet meer binnen één enkele multi-entiteitspubliek worden gebruikt dat B2B attributen omvat.

Om de zelfde publiekslogica te bereiken, kunt u de segmentbouwer gebruiken om [&#x200B; publiek en verwijzingspubliek &#x200B;](../segmentation/ui/segment-builder.md#adding-audiences) toe te voegen

Bijvoorbeeld:

* Een Experience Event-publiek maken
   * De gedragsconditie afzonderlijk definiëren. Bijvoorbeeld: &quot;Personen die de prijspagina de afgelopen drie dagen hebben bezocht.&quot;
* Maak een publiek met meerdere entiteiten met B2B-kenmerken.
   * Van hieruit kunt u het publiek van de Gebeurtenis van de Ervaring als deel van de criteria van dit publiek van verwijzingen voorzien. Bijvoorbeeld: &quot;Mensen die a **&quot;Beslissingsmaker&quot;** van om het even welke kans zijn waar de rekening in de **&quot;Financiën&quot;** industrie en lid van het mensen publiek is die de het tarief pagina in de laatste drie dagen bezochten.

Zodra de verbetering volledig is, moet om het even welk nieuw multi-entiteitpubliek met attributen B2B en de Gebeurtenissen van de Ervaring worden gecreeerd gebruikend de [&#x200B; segment-van-segment &#x200B;](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types) benadering.

>[!TIP]
>
>A **segment van segmenten** is om het even welke segmentdefinitie die één of meerdere partij of randsegmenten bevat. **Nota**: als u een segment van segmenten gebruikt, zal de profielontzetting **om de 24 uur** gebeuren.

### Afwikkeling van entiteiten en tijdsprioriteit bij samenvoeging in B2B-publiek

Als onderdeel van de architectuurupgrade introduceert Adobe entiteitresolutie voor accounts en mogelijkheden. De afwikkeling van entiteiten is gebaseerd op deterministische ID-matching en op de meest recente gegevens. Entiteitsafwikkelingstaak wordt dagelijks uitgevoerd tijdens batchsegmentering, voordat het publiek met meerdere entiteiten met B2B-kenmerken wordt geëvalueerd.

>[!BEGINSHADEBOX]

#### Hoe werkt het oplossen van entiteiten?

* **vóór**: Als een aantal van het Systeem van de Nummering van Gegevens Universele (DUNS) als extra identiteit werd gebruikt en het aantal DUNS van de rekening werd bijgewerkt in een bronsysteem zoals CRM, wordt rekeningidentiteitskaart verbonden met zowel oude als nieuwe DUNS aantallen.
* **na**: Als het aantal DUNS als extra identiteit werd gebruikt en het aantal DUNS van de rekening in een bronsysteem als CRM werd bijgewerkt, wordt rekeningidentiteitskaart slechts verbonden met het nieuwe aantal DUNS, daardoor die nauwkeuriger op de huidige staat van rekening wijst.

>[!ENDSHADEBOX]

Met deze upgrade kunt u nu:

* Gebruik de API&#39;s van [!DNL Profile Access] om de meest recente samenvoegprofielen weer te geven zodra de taken voor de dagelijkse entiteitsresolutie zijn voltooid.
* Gebruik de verbeterde nauwkeurigheid en consistentie van uw account en opportuniteitsgegevens voor segmentatie, activering en analyse.

Lees [[!DNL Profile Access]  API &#x200B;](../profile/api/entities.md) voor meer informatie.

### Ondersteuning van samenvoegingsbeleid in het B2B-publiek met meerdere entiteiten

Het publiek van meerdere entiteiten met B2B-attributen steunt nu één enkel fusiebeleid - het standaardfusiebeleid dat u vormt - in plaats van veelvoudige fusiebeleid.

Lees de [&#x200B; handleiding van het de gebruikscase van de segmentatie voor Real-Time CDP B2B edition &#x200B;](./segmentation/b2b.md) voor meer informatie.

### Opzoeken en verwijderen van B2B-tekeneenheden in de API van [!DNL Profile Access]

De volgende opzoekfuncties voor B2B-entiteiten die de API [!DNL Profile Access] gebruiken, worden afgekeurd:

* Relatie account-persoon
* Opportunity-Person relatie
* Campaign
* Campagnelid
* Marketinglijst
* Leden van de marketinglijst

Verzoeken voor de volgende B2B-entiteiten die de API [!DNL Profile Access] gebruiken, worden afgekeurd:

* Account
* Relatie account-persoon
* Kans
* Opportunity-Person relatie
* Campaign
* Campagnelid
* Marketinglijst
* Leden van de marketinglijst

Lees [[!DNL Profile Access]  API &#x200B;](../profile/api/entities.md) voor meer informatie.

### Verplaatsing van API voor segmenttaak

Onder de nieuwe architectuur, &quot;creeer een eindpunt van de segmentbaan&quot;en de flexibele publieksevaluatie worden *not gesteund.

### Zoeken naar account- en opportuniteitsprofielen

U kunt account- en opportuniteitsschema&#39;s nu alleen ophalen als entiteiten met een zoekdimensie nadat ze het dagelijkse proces voor het oplossen van entiteiten hebben voltooid. Nieuw opgenomen records zijn pas beschikbaar voor profielverrijking of segmentdefinities als de volgende cyclus met entiteitresolutie is voltooid (meestal elke 24 uur).

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### Wijzigingen in het importeren van publiek van meerdere entiteiten in gereedschappen voor sandboxen

Met de architectuurupgrades kunt u geen publiek met meerdere entiteiten meer importeren met B2B-kenmerken en Experience Events als een pakket met deze soorten publiek vóór de upgrade is gepubliceerd. Deze doelgroepen kunnen niet worden geïmporteerd en kunnen niet automatisch worden geconverteerd naar de nieuwe architectuur. Als u deze beperking wilt omzeilen, moet u een nieuw pakket maken met het bijgewerkte publiek en deze met behulp van sandboxgereedschappen importeren in de respectievelijke doelsandboxen.

Ontwikkelingssandboxen worden opgewaardeerd naar de nieuwe architectuur. De soorten publiek die automatisch kunnen worden bijgewerkt, worden bijgewerkt; de soorten die niet kunnen worden uitgeschakeld. Uitgeschakelde doelgroepen moeten na de upgrade opnieuw worden gemaakt.

Lees de [&#x200B; zandbak tooling gids &#x200B;](../sandboxes/ui/sandbox-tooling.md) voor meer informatie.
