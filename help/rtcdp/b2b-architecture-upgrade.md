---
title: Architectuurupgrades naar Real-Time CDP B2B edition
description: Lees dit document voor meer informatie over de uitgebreide architectuurupgrades naar Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/nl/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
hide: true
hidefromtoc: true
source-git-commit: 78444555178773a8305ba27aaaf7998fe279a71d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Architectuuropties naar Real-Time CDP B2B edition

>[!IMPORTANT]
>
>In dit document worden architectuurupgrades naar Real-Time CDP B2B en B2P Editions beschreven. **Geen actie wordt vereist van u** op dit punt. Raadpleeg dit document voor informatie over de gevolgen van de upgrades voor de bestaande functies van Adobe Experience Platform. Neem contact op met uw Adobe-accountteam als u vragen hebt.

Adobe heeft de Real-Time CDP B2B- en B2P-edities opnieuw ontworpen om de schaalbaarheid, prestaties en betrouwbaarheid te verbeteren, en ondersteunt ook meer geavanceerde B2B-gebruiksscenario&#39;s. Om ervoor te zorgen dat alle klanten van deze verbeteringen profiteren, zal Adobe alle bestaande B2B- en B2P-klanten upgraden naar de nieuwe architectuur.

Gebruik de verbeterde architectuur voor de volgende voordelen:

* **Schaalbaarheid van gegevensopname**: Verbeterde steun voor high-cardinality B2B verhoudingen, zoals rekeningen die met duizenden mensen worden verbonden.
* **Krachtige en betrouwbare publieksevaluatie**: Snellere en veerkrachtigere segmentatie voor complex B2B publiek.
* **entiteitresolutie**: Verbeterde identiteitsresolutie voor B2B entiteiten, verbeterde gegevenskwaliteit, en verminderde duplicatie om nauwkeurigere segmentatie en samenvoeging toe te laten.

## Nieuwe functies

Lees het volgende voor zeer belangrijke verhogingen inbegrepen in de architecturale verbetering.

### Momentopnamen van account voor publieksleden

Met de nieuwe B2B-architectuur worden de details van het publiekslidmaatschap nu opgenomen voor accountentiteiten in momentopnameleverporten. Met deze functie hebt u toegang tot de publieksstatus op accountniveau, tijdstempels en lidmaatschapsindicatoren.

Met deze upgrade kunt u nu:

* Schakel marketing- en operatieteams in om het lidmaatschap van het accountpubliek rechtstreeks te valideren.
* Benader de pariteit tussen uw profiel (persoon) en de modellen van de rekeningssegmentatie van de rekening, die verenigbare ervaring over entiteiten verzekeren.

Lees de documentatie over [ rekeningspubliek ](../segmentation/types/account-audiences.md) voor meer informatie.

### Aantallen van het publiek voor soorten publiek die B2B-entiteiten omvatten

Schattingen van de omvang van het publiek voor soorten publiek met B2B-entiteiten worden nu precies berekend. Deze schattingen zijn beschikbaar tijdens de voorvertoning en bieden nauwkeurigere en betrouwbaardere inzichten voor het publiek dat complexe B2B-relaties omvat.

Met deze upgrade kunt u nu:

* Gebruik inzichten van nauwkeurige schattingen van de omvang van het publiek om de planning en besluitvorming tijdens het maken van het publiek te verbeteren.
* Ontwerp op betrouwbare wijze complexe B2B-doelgroepen, met kennis van nauwkeurigere publieksschattingen.
* Verbeter een slimmere campagneplanning, nauwkeurigere gerichtheid, en betere middelentoewijzing.

Lees de documentatie over [ rekeningspubliek ](../segmentation/types/account-audiences.md) voor meer informatie.

### Volledige zoekopdracht naar gebeurtenissen op persoonniveau in accountpubliek

Accountpubliek kan nu de volledige geschiedenis van gebeurtenissen op persoonniveau benutten en deze gebeurtenissen overschrijden het vorige terugzoekvenster van 30 dagen.

Met deze upgrade kunt u nu:

* Uitgebreider publiek maken op basis van de volledige geschiedenis van verwante gebeurtenissen op persoonniveau.
* Verrijkere en nauwkeuriger publieksdefinities door gedragsgegevens op lange termijn te gebruiken.
* Hoogwaardige accounts identificeren op basis van diepere betrokkenheidspatronen in de loop der tijd.
* Ondersteuning van gebruiksgevallen die inzichten vereisen van historische handelingen, zoals lange verkoopcycli of vertraagde aankoopsignalen.

Lees de documentatie over [ rekeningspubliek ](../segmentation/types/account-audiences.md) voor meer informatie.

## Verbeteringen aan bestaande functies

De volgende functies zijn bijgewerkt als onderdeel van de B2B-architectuurupgrades.

### Updates voor publiek met meerdere entiteiten met B2B-kenmerken en Experience Events

Als onderdeel van de nieuwe architectuurupgrade kunnen de filters van de Gebeurtenis van de Ervaring niet meer binnen één enkele multi-entiteitspubliek worden gebruikt dat B2B attributen omvat.

Om de zelfde publiekslogica te bereiken, gebruik de segment-van-segment benadering:

1. Creeer een publiek van de Gebeurtenis van de Ervaring: bepaal afzonderlijk de gedragstoestand. Bijvoorbeeld: &quot;Personen die de prijspagina de afgelopen drie dagen hebben bezocht.&quot;
2. Creeer een multi-entiteitpubliek met B2B attributen: Verwijs het publiek van de Gebeurtenis van de Ervaring als deel van de criteria van dit publiek. Bijvoorbeeld: &quot;Mensen die a **&quot;Beslissingsmaker&quot;** van om het even welke kans zijn waar de rekening in de **&quot;Financiën&quot;** industrie en lid van het mensen publiek is die de het tarief pagina in de laatste drie dagen bezochten.

Zodra de verbetering volledig is, moet om het even welk nieuw multi-entiteitpubliek met B2B attributen en de Gebeurtenissen van de Ervaring worden gecreeerd gebruikend de segment-van-segmentbenadering. Daarnaast moet u het lidmaatschap van het publiek valideren om het verwachte gedrag te garanderen.

### Afwikkeling van entiteiten en tijdsprioriteit bij samenvoeging in B2B-publiek

Als onderdeel van de architectuurupgrade heeft Adobe een entiteitsresolutie voor accounts en mogelijkheden geïntroduceerd, die dagelijks wordt uitgevoerd. Dankzij deze verbetering kan Experience Platform meerdere records identificeren en consolideren die dezelfde real-world entiteit vertegenwoordigen. Hierdoor wordt de gegevensconsistentie verbeterd en wordt de publiekssegmentatie nauwkeuriger.

Met deze upgrade kunt u nu:

* Gebruik de API&#39;s van [!DNL Profile Access] om de meest recente samenvoegprofielen weer te geven zodra de taken voor de dagelijkse entiteitsresolutie zijn voltooid.
* Gebruik de verbeterde nauwkeurigheid en consistentie van uw account en opportuniteitsgegevens voor segmentatie, activering en analyse.

Lees [[!DNL Profile Access]  API ](../profile/api/entities.md) voor meer informatie.

### Ondersteuning van samenvoegingsbeleid in het B2B-publiek met meerdere entiteiten

Het publiek van meerdere entiteiten met B2B-attributen steunt nu één enkel fusiebeleid - het standaardfusiebeleid dat u vormt - in plaats van veelvoudige fusiebeleid.

Het publiek dat eerder op een niet-standaard fusiebeleid baseerde kan verschillende resultaten veroorzaken. Om de potentiële veranderingen in publiekssamenstelling te begrijpen, herzie en test om het even welk publiek dat op een niet-gebrek fusiebeleid baseert. Bovendien, de resultaten van de monitoractivering om het even welke verschuivingen in publiekssamenstelling wegens de verandering van het fusiebeleid te ontdekken.

Lees de [ handleiding van het de gebruikscase van de segmentatie voor Real-Time CDP B2B edition ](./segmentation/b2b.md) voor meer informatie.

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
* Opportunity
* Opportunity-Person relatie
* Campaign
* Campagnelid
* Marketinglijst
* Leden van de marketinglijst

Lees [[!DNL Profile Access]  API ](../profile/api/entities.md) voor meer informatie.

### Zoeken naar account- en opportuniteitsprofielen

U kunt account- en opportuniteitsschema&#39;s nu alleen ophalen als entiteiten met een zoekdimensie nadat ze het dagelijkse proces voor het oplossen van entiteiten hebben voltooid. Nieuw opgenomen records zijn pas beschikbaar voor profielverrijking of segmentdefinities als de volgende cyclus met entiteitresolutie is voltooid (meestal elke 24 uur).

U wordt aangeraden alle gebruiksgevallen te bekijken waarvoor realtime toegang tot account- en opportuniteitsgegevens vereist is. Bovendien, wordt u geadviseerd om voor een latentieperiode van 24 uur te plannen wanneer het ontwerpen van of het bijwerken van werkschema&#39;s die van raadpleging-gebaseerde segmentatie of verpersoonlijking met rekening en opportuniteitsentiteiten afhangen.

### Veroudering van publiek creëren via API voor B2B-entiteiten

Het creëren van een publiek met B2B-entiteiten via de API wordt afgekeurd. De lijst van betrokken B2B-entiteiten omvat:

* Account
* Opportunity
* Relatie account-persoon
* Opportunity-Person relatie
* Campaign
* Campagnelid
* Marketinglijst
* Lid van de marketinglijst

Lees de [ gids van het 0&rbrace; segment definities eindpunt API ](../segmentation/api/segment-definitions.md) voor meer informatie.

### Wijzigingen in het importeren van publiek van meerdere entiteiten in gereedschappen voor sandboxen

Met de architectuuractupgrades kunt u geen publiek met meerdere entiteiten meer importeren met B2B-kenmerken en Experience Events als deze werden geëxporteerd vóór de upgrade. Deze doelgroepen kunnen niet worden geïmporteerd en kunnen niet automatisch worden geconverteerd naar de nieuwe architectuur. Als u deze beperking wilt omzeilen, moet u deze doelgroepen opnieuw exporteren en deze vervolgens met behulp van sandboxgereedschappen importeren in de desbetreffende doelsandboxen.

Lees de [ zandbak tooling gids ](../sandboxes/ui/sandbox-tooling.md) voor meer informatie.