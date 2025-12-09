---
keywords: Experience Platform;data mirror;relationeel schema;change data capture;database sync;primary key;relaties
solution: Experience Platform
title: Data Mirror-overzicht
description: Leer hoe Data Mirror veranderingsingang op rijniveau van externe gegevensbestanden in Adobe Experience Platform gebruikend relationele schema's met gedwongen uniciteit, verhoudingen, en versioning toelaat.
badge: Beperkte beschikbaarheid
exl-id: bb92c77a-6c7a-47df-885a-794cf55811dd
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# Data Mirror-overzicht

>[!AVAILABILITY]
>
>Data Mirror en relationele schema&#39;s zijn beschikbaar aan Adobe Journey Optimizer **Geordende campagnes** vergunninghouders. Zij zijn ook beschikbaar als a **beperkte versie** voor de gebruikers van Customer Journey Analytics, afhankelijk van uw vergunning en eigenschapenactivering. Neem contact op met uw Adobe-vertegenwoordiger voor toegang.

Data Mirror is een capaciteit van Adobe Experience Platform die rij-vlakke veranderingsopname van externe gegevensbestanden in het gegevensmeer gebruikend relationele schema&#39;s toelaat. Het bewaart gegevensverhoudingen, dwingt uniciteit af, en steunt versioning zonder upstream extractie, transformatie, lading (ETL) processen te vereisen.

Met Data Mirror kunt u invoegen, bijwerken en verwijderen (muteerbare gegevens) van externe systemen zoals [!DNL Snowflake] , [!DNL Databricks] of [!DNL BigQuery] rechtstreeks in Experience Platform. Hierdoor kunt u de bestaande structuur en gegevensintegriteit van het databasemodel behouden wanneer u gegevens naar het platform overbrengt.

## Capaciteiten en voordelen

Data Mirror biedt de volgende essentiële mogelijkheden voor databasesynchronisatie:

* **Primaire zeer belangrijke handhaving**: Zorgt voor uniciteit binnen datasets en verhindert dubbele verslagen tijdens opname.
* **row-vlakke veranderingsopname**: Steunt korrelige gegevensveranderingen met inbegrip van upserts en schrapt met nauwkeurige controle.
* **verhoudingen van het Schema**: Laat buitenlandse en primaire zeer belangrijke verhoudingen tussen datasets door beschrijvers toe.
* **uit-van-orde gebeurtenis behandeling**: Verwerkt veranderingsgebeurtenissen gebruikend versie en timestamp beschrijvers, zelfs wanneer zij uit opeenvolging aankomen.
* **Directe pakhuis integratie**: Verbindt met gesteunde de pakhuizen van wolkengegevens voor dichtbij synchronisatie van de verandering in real time.

Gebruik Data Mirror om wijzigingen rechtstreeks van uw bronsystemen in te voeren, de schemacontegriteit af te dwingen en de gegevens beschikbaar te stellen voor analyses, reisorchestratie en compatibiliteitsworkflows. Data Mirror elimineert complexe stroomopwaartse processen ETL en versnelt implementatie door direct het weerspiegelen van bestaande gegevensbestandmodellen toe te laten.

Plan voor schrapping en gegevenshygiënevereisten wanneer het uitvoeren van relationele regelingen met Data Mirror. Alle toepassingen moeten in overweging nemen hoe schrappingen verwante datasets, nalevingswerkschema&#39;s, en stroomafwaartse processen vóór plaatsing beïnvloeden.

## Vereisten {#prerequisites}

Voordat u aan de slag gaat, moet u de volgende onderdelen van Experience Platform begrijpen en controleren of uw omgeving voldoet aan de technische en structurele vereisten:

* [&#x200B; creeer schema&#39;s in Experience Platform UI &#x200B;](../ui/resources/schemas.md) of [&#x200B; API &#x200B;](../api/schemas.md)
* [Cloubron-verbindingen configureren](../../sources/home.md#cloud-storage)
* [&#x200B; pas veranderingsgegevens toe vangen concepten &#x200B;](../../sources/tutorials/api/change-data-capture.md) (upserts, schrapt)
* Distinguish tussen [&#x200B; standaard &#x200B;](../schema/composition.md) en [&#x200B; relationele schema&#39;s &#x200B;](../schema/relational.md)
* [Structurele relaties definiëren met descriptors](../api/descriptors.md)

### Implementatievereisten

Uw Platform-exemplaar en brongegevens moeten voldoen aan specifieke vereisten voor een correcte werking van Data Mirror. Data Mirror vereist **relationele schema&#39;s**, die flexibele gegevensstructuren met gedwongen beperkingen zijn.

Omvat a **primaire sleutel en versiedescriptor** in alle schema&#39;s. Als u met een tijd-reeks schema werkt, wordt a **timestamp beschrijver** ook vereist.

Uw externe database moet ondersteuning bieden voor het vastleggen van wijzigingsgegevens of voor metagegevens die invoegen, bijwerken en verwijderen identificeren. De gegevens van Source moeten **unieke herkenningstekens** omvatten, of één enkel gebied of een samengestelde primaire sleutel en **versieinformatie** zodat kan het systeem updates in de correcte orde toepassen.

Om schrappingen te ontdekken, voeg een `_change_request_type` kolom toe die specificeert of elke verslag een upsert of een schrapping is.

## Data Mirror implementeren {#implementation-workflow}

In tegenstelling tot de standaardbenaderingen van de opname, behoudt Data Mirror de structuur van uw databasemodel binnen het Experience Platform-datumpomeer. Door deze consistentie in de gegevensstructuur is een externe voorbehandeling overbodig. Hieronder volgt een workflow voor Data Mirror-implementatie op hoog niveau. Kies de implementatiemethode op basis van de workflow en het bronsysteem van uw team.

### De schemastructuur definiëren

Creeer [&#x200B; relationele schema&#39;s &#x200B;](../schema/relational.md) met vereiste beschrijvers (meta-gegevens die schemagedrag en beperkingen bepalen). Kies een methode die in de workflow van uw team past, via de gebruikersinterface of rechtstreeks via de API.

* **benadering UI**: [&#x200B; creeer relationele schema&#39;s in de Redacteur van het Schema &#x200B;](../ui/resources/schemas.md#create-relational-schema)
* **API benadering**: [&#x200B; creeer schema&#39;s via de Registratie API van het Schema &#x200B;](../api/schemas.md#create-relational-schema)

### Relaties toewijzen en gegevensbeheer definiëren

Bepaal verbindingen tussen datasets gebruikend relatiebeschrijvers. Relaties beheren en de gegevenskwaliteit in verschillende gegevenssets behouden. Deze taken zorgen voor consistente verbindingen en ondersteunen de naleving van de gegevenshygiënevoorschriften.

* **relaties van het Schema**: [&#x200B; bepalen verband tussen datasets gebruikend beschrijvers &#x200B;](../api/descriptors.md)
* **hygiëne van het Verslag**: [&#x200B; beheert precisierecord schrapt voor datasets die op relationele schema&#39;s &#x200B;](../../hygiene/ui/record-delete.md#relational-record-delete) worden gebaseerd

### De bronverbinding configureren

Selecteer een innamemethode op basis van uw bronsysteem en gebruikscase. Elke optie ondersteunt verschillende niveaus van automatisering, transformatie en schaalbaarheid.

* [**Wolkenbronverbindingen configureren**](../../sources/home.md#cloud-storage)
* **SQL-opname**: Gebruik Data Distiller om in relationele datasets te schrijven
* [**uploadt het Dossier**](../ui/resources/schemas.md#upload-ddl-file): Upload manueel dossiers voor partij of eenmalig ingebed

### Inname van vastleggen van gegevens wijzigen inschakelen

Verbindingen voor het vastleggen van wijzigingsgegevens instellen met ondersteunde wolkengegevenspakhuizen. Breng veranderingen op rijniveau met behoud van uniciteit voor en pas updates in de correcte orde toe.

* **Gegevens van de Verandering vangen**: [&#x200B; laat veranderingsgegevens toe vangen in bronverbindingen &#x200B;](../../sources/tutorials/api/change-data-capture.md)

## Vaak voorkomende gebruiksscenario&#39;s {#use-cases}

Bekijk hieronder de veelvoorkomende gebruiksgevallen waarin Data Mirror nauwkeurige gegevenssynchronisatie en relatiebehoud ondersteunt. Elk scenario toont hoe Data Mirror gemeenschappelijke bedrijfsbehoeften over analyses, orchestratie, en naleving steunt.

### Relationele gegevensmodellering

Het gebruik [&#x200B; relationele schema&#39;s &#x200B;](../schema/relational.md) in Data Mirror om entiteiten, procestussenvoegsels, updates, en schrapt op het rijniveau te vertegenwoordigen, en de primaire en buitenlandse zeer belangrijke verhoudingen te handhaven die in uw gegevensbronnen bestaan. Deze benadering brengt de beginselen van relationele gegevensmodellering naar Experience Platform en zorgt voor structurele consistentie tussen gegevensreeksen.

### Synchronisatie van aardehuis naar meer

De gebeurtenisgegevens van de spiegel, de logboeken van de klanteninteractie, campagnegebeurtenissen, en hulpgegevens van gesteunde de pakhuizen van wolkengegevens in Experience Platform. Dit steunt campagnegeschiktheid, richtend precisie, en berichtopeenvolging. Journey Optimizer en Real-Time CDP B2B baseren zich op dit voor bijna-real-time orchestratielogica.

### Customer Journey Analytics-integratie

Synchroniseer tijdreeksgebeurtenissen zoals Web klikt, productmeningen, aankopen, en steuninteractie van systemen zoals vraagcentra of praatjelogboeken. Een volledige veranderingsgeschiedenis steunt nauwkeurige trendanalyse en gedragssegmentatie. Experience Platform Data Mirror for Customer Journey Analytics gebruikt dit om updates en verwijderingen van bronsystemen te weerspiegelen.

### B2B-relatiemodellen

Relaties zoals account-aan-contact, abonnement-aan-rekening, of contact-aan-regio hiërarchieën behouden. Deze steunen segmentatie, lood scoring, kansen volgen, en multichannel coördinatie. In tegenstelling tot standaardopname die relaties afvlakt, handhaaft Data Mirror deze native met behulp van beschrijvingen voor nauwkeuriger modellering.

### Abonnementsbeheer

Gebeurtenissen bijhouden zoals vernieuwingen, annuleringen, upgrades, downgrades en wijzigingen in het plan met de volledige versiegeschiedenis. Dit steunt behoudcampagnes, kinnevoorspelling, en levenscyclusgebaseerde segmentatie. De volledige geschiedenis laat gedragsinzichten en nauwkeurige het richten toe.

### Gegevenshygiëne

Met de gegevensvastlegging voor wijzigingen kunt u nauwkeurige verwijderingen op recordniveau mogelijk maken voor naleving (bijv. gereglementeerde industrieën) en werkstromen opschonen. Data Mirror past schrappingen correct toe terwijl het bewaren van verwante gegevens over verbonden datasets.

## Belangrijke overwegingen {#considerations}

Herzie deze zeer belangrijke overwegingen om uw implementatie te verzekeren richt zich op gesteund schemagedrag, insluitingsmethodes, en relatiepatronen. Een goede planning helpt integratieproblemen te voorkomen en zorgt voor een nauwkeurige modellering van gegevens.

### Gegevensverwijdering en hygiënevoorschriften

Alle toepassingen die relationele schema&#39;s en Data Mirror gebruiken moeten implicaties van de gegevensschrapping begrijpen. Relationele schema&#39;s laten nauwkeurige verslag-vlakke schrappingen toe die verwante gegevens over verbonden datasets kunnen beïnvloeden. Deze verwijderingsmogelijkheden zijn van invloed op gegevensintegriteit, compatibiliteit en gedrag van downstreamtoepassingen, ongeacht uw specifieke gebruiksscenario. Herzie [&#x200B; vereisten van de gegevenshygiëne voor datasets die op relationele schema&#39;s &#x200B;](../../hygiene/ui/record-delete.md#relational-record-delete) worden gebaseerd en plan voor schrappingsscenario&#39;s vóór implementatie.

### Selectie van schemagedrag

De relationele schema&#39;s gebrek aan **verslaggedrag**, dat entiteitstaat (klanten, rekeningen, enz.) vangt. Als u **tijd-reeksen gedrag** voor gebeurtenis het volgen nodig hebt, moet u het uitdrukkelijk vormen.

### Vergelijking van de inscriptiemethode

Gebruik deze vergelijkingstabel om de beste innamemethode voor uw gegevensbehoeften te kiezen, of u synchronisatie in real time, op SQL-Gebaseerde transformatie, of handmatige dossieruploads vereist.

| Inktmethode | Gebruiksscenario |
| ----------------------- | -------------------------------------------------------------- |
| **gegevens van de Verandering vangen** | Synchronisatie in realtime van ondersteunde wolkenpakhuizen |
| **Gegevens Distiller** | Workflows voor opname en transformatie op basis van SQL |
| **uploadt het Dossier** | Batch/handmatige opname wanneer bronintegratie niet beschikbaar is |

### Relatiebeperkingen

Data Mirror steunt **één-aan-één** en **vele-aan-één** verhoudingen gebruikend beschrijvers. **vele-aan-vele** verhoudingen vereisen extra modellering en niet direct gesteund.

## Volgende stappen

Na het bekijken van dit overzicht, zou u moeten kunnen bepalen als Data Mirror uw gebruiksgeval past en de vereisten voor implementatie begrijpen. Aan de slag:

1. **de architecten van Gegevens** zouden uw gegevensmodel moeten beoordelen om het primaire sleutels te verzekeren, versioning, en veranderingsvolgende mogelijkheden.
2. **Bedrijfs belanghebbenden** zouden uw vergunning relationele schemasteun en vereiste uitgaven van Experience Platform moeten bevestigen.
3. **de ontwerpers van het Schema** zouden uw schemastructuur moeten plannen om vereiste beschrijvers, gebiedsverhoudingen, en de behoeften van het gegevensbeheer te identificeren.
4. **de teams van de Implementatie** zouden een innamemethode moeten kiezen die op uw bronsystemen, vereisten in real time, en operationele werkschema&#39;s wordt gebaseerd.

Voor implementatiedetails, zie de [&#x200B; relationele schemadocumentatie &#x200B;](../schema/relational.md).
