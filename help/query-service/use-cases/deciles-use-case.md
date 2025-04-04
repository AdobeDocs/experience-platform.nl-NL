---
title: Het op decreet-gebaseerde Geval van het Gebruik van Datasets
description: Deze gids toont de stappen die worden vereist om de Dienst van de Vraag te gebruiken om op decile-Gebaseerde afgeleide datasets voor gebruik met uw gegevens van het Profiel tot stand te brengen.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---

# Gebruiksgeval voor op een regel gebaseerde afgeleide gegevenssets

De afgeleide datasets vergemakkelijken gecompliceerde gebruiksgevallen voor het analyseren van gegevens van het gegevensmeer die met andere stroomafwaartse diensten van Experience Platform kunnen worden gebruikt of in uw gegevens van het Profiel van de Klant in real time worden gepubliceerd.

Dit voorbeeld gebruikt geval toont aan hoe te om op decile-gebaseerde afgeleide datasets voor gebruik met uw gegevens van het Profiel van de Klant in real time te creëren. Gebruikend een scenario van de luchtvaartloyaliteit als voorbeeld, vertelt deze gids u hoe te om een dataset tot stand te brengen die categoriale deciles gebruikt om te segmenteren en publiek tot stand te brengen dat op gerangschikte attributen wordt gebaseerd.

De volgende belangrijke concepten worden geïllustreerd:

* Schema maken voor decile bucketing.
* Categorisch decile maken.
* Opstellen van complexe afgeleide gegevenssets.
* Berekening van tegels in een terugzoekperiode.
* Een voorbeeldvraag om samenvoeging, rangschikking, en het toevoegen van unieke identiteiten aan te tonen om voor publiek toe te staan dat op deze decile emmers wordt geproduceerd.

## Aan de slag

Deze gids vereist een werkend begrip van [ vraaguitvoering in de Dienst van de Vraag ](../best-practices/writing-queries.md) en de volgende componenten van Adobe Experience Platform:

* [ Real-Time overzicht van het Profiel van de Klant ](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [ Grondbeginselen van schemacompositie ](../../xdm/schema/composition.md): Een inleiding aan de schema&#39;s van het Model van Gegevens van de Ervaring (XDM) en de bouwstenen, beginselen, en beste praktijken voor het samenstellen van schema&#39;s.
* [ hoe te om een schema voor het Profiel van de Klant in real time ](../../profile/tutorials/add-profile-data.md) toe te laten: Dit leerprogramma schetst de stappen noodzakelijk om gegevens aan het Profiel van de Klant toe te voegen In real time.
* [ hoe te om een type van douanegegevens te bepalen ](../../xdm/api/data-types.md): De types van gegevens worden gebruikt als verwijzing-type gebieden in klassen of de groepen van het schemagebied en staan voor het verenigbare gebruik van een multi-gebiedstructuur toe die overal in het schema kan worden omvat.

## Doelstellingen

Het voorbeeld in dit document gebruikt deciles om afgeleide datasets te bouwen voor het rangschikken van gegevens van een schema van de luchtvaartloyaliteit. Met afgeleide datasets kunt u het nut van uw gegevens maximaliseren door een publiek te identificeren dat op de top &#39;n&#39; % voor een gekozen categorie wordt gebaseerd.

## Op decile gebaseerde afgeleide gegevenssets maken

Om de rangschikking van deciles te bepalen die op een bepaalde afmeting en overeenkomstige metrisch wordt gebaseerd, moet een schema worden ontworpen om voor het decile knippen toe te staan.

Deze gids gebruikt een dataset van de luchtvaartloyaliteit om aan te tonen hoe te om de Dienst van de Vraag te gebruiken om deciles te bouwen die op mijlen worden gebaseerd die over diverse terugkijkperiodes worden gevlogen.

## De Dienst van de Vraag van het gebruik om deciles te creëren

Gebruikend de Dienst van de Vraag, kunt u een dataset tot stand brengen die categorische deciles bevat, die dan kan worden gesegmenteerd om publiek tot stand te brengen dat op attributenrangschikking wordt gebaseerd. De concepten die in de volgende voorbeelden worden getoond kunnen worden toegepast om andere decile emmerdatasets tot stand te brengen, zolang een categorie wordt bepaald en metrisch beschikbaar is.

De gegevens van de voorbeeldluchtvaartloyaliteit gebruiken een [ XDM klasse ExperienceEvents ](../../xdm/classes/experienceevent.md). Elke gebeurtenis is een overzicht van een zakelijke transactie voor afgelegde kilometers, gecrediteerd of gedebiteerd, en de status van lidmaatschapsloyaliteit van &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; of &quot;Gold&quot;. Het primaire identiteitsveld is `membershipNumber` .

### Voorbeeldgegevenssets

De aanvankelijke dataset van de luchtvaartloyaliteit voor dit voorbeeld is &quot;Gegevens van de Loyalty van de Luchtlijn&quot;, en heeft het volgende schema. De primaire identiteit voor het schema is `_profilefoundationreportingstg.membershipNumber` .

![ een diagram van het schema van de Gegevens van de Loyalty van het Luchtnet.](../images/use-cases/airline-loyalty-data.png)

**gegevens van de Steekproef**

In de volgende tabel worden de voorbeeldgegevens weergegeven in het `_profilefoundationreportingstg` -object dat voor dit voorbeeld wordt gebruikt. Het verstrekt context voor het gebruik van deegemmers om complexe afgeleide datasets tot stand te brengen.

>[!NOTE]
>
>Kortom, de huurder-id `_profilefoundationreportingstg` is weggelaten van het begin van de naamruimte in de kolomtitels en de daaropvolgende vermeldingen in het hele document.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 01-01-2022 | STATUS_MILES | Nieuw lid | 5000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | SILVER |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nieuwe creditcard | 10000 | FLYER |

{style="table-layout:auto"}

## Decile-gegevenssets genereren

In de bovenstaande loyaliteitsgegevens van de luchtvaartmaatschappij bevat de `.mileage` -waarde het aantal mijl dat een lid per vlucht aflegt. Dit gegeven wordt gebruikt om deciles voor het aantal mijlen tot stand te brengen die over levenraadplegingen en een verscheidenheid van terugzoekperiodes worden gevlogen. Hiertoe wordt een dataset gemaakt die deciles bevat in een gegevenstype voor elke terugzoekperiode en een geschikte decile voor elke terugzoekperiode die onder `membershipNumber` is toegewezen.

Maak een &quot;Airline Loyalty Decile Schema&quot; om een decile dataset te maken met gebruik van Query Service.

![ A diagram van het &quot;Airline Loyalty Decile Schema&quot;.](../images/use-cases/airline-loyalty-decile-schema.png)

### Het schema inschakelen voor realtime-klantprofiel

Gegevens die in Experience Platform voor gebruik door het Profiel van de Klant in real time worden opgenomen moeten [ een Model van de Gegevens van de Ervaring (XDM) schema in overeenstemming zijn dat voor Profiel ](../../xdm/ui/resources/schemas.md) wordt toegelaten. Een schema kan alleen worden ingeschakeld voor Profiel als het de klasse XDM Individual Profile of XDM ExperienceEvent implementeert.

[ laat uw schema voor gebruik in het Profiel van de Klant in real time toe gebruikend de Registratie API van het Schema ](../../xdm/tutorials/create-schema-api.md) of het [ gebruikersinterface van de Redacteur van het Schema ](../../xdm/tutorials/create-schema-ui.md).  Gedetailleerde instructies over hoe te om een schema voor Profiel toe te laten zijn beschikbaar in hun respectieve documentatie.

Maak vervolgens een gegevenstype dat opnieuw moet worden gebruikt voor alle op decile betrekking hebbende veldgroepen. Het maken van de decile-veldgroep is een eenmalige stap per sandbox. Het kan ook voor alle op decile betrekking hebbende regelingen opnieuw worden gebruikt.

### Een naamruimte voor identiteit maken en markeren als primaire id {#identity-namespace}

Om het even welk schema dat voor gebruik met deciles wordt gecreeerd moet een primaire toegewezen identiteit hebben. U kunt [ een identiteitsgebied in de Schema&#39;s UI van Adobe Experience Platform ](../../xdm/ui/fields/identity.md#define-an-identity-field) bepalen, of door de [ Registratie API van het Schema ](../../xdm/api/descriptors.md#create).

De Dienst van de vraag staat u ook toe om een identiteit of een primaire identiteit voor de gebieden van de ad hoc schemadataset direct door SQL te plaatsen. Zie de documentatie bij [ plaatsend een secundaire identiteit en een primaire identiteit in ad hoc schemaidentiteiten ](../data-governance/ad-hoc-schema-identities.md) voor meer informatie.

### Creeer een vraag voor het berekenen van deciles over een raadplegingsperiode {#create-a-query}

In het volgende voorbeeld wordt de SQL-query getoond voor het berekenen van een decile-bewerking over een terugzoekperiode.

Een malplaatje kan of worden gemaakt gebruikend de Redacteur van de Vraag in UI, of door de [ Dienst API van de Vraag ](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### Query-revisie

Secties van de voorbeeldquery worden hieronder nader onderzocht.

#### Termijnen voor opzoeken

Het gegevenstype decile bevat een emmertje voor 1, 3, 6, 9, 12, en levenlookbacks. De vraag gebruikt de raadplegingsperiodes van 1, 3, en 6 maanden, zodat zal elke sectie sommige &quot;herhaalde&quot;vragen bevatten om tijdelijke lijsten voor elke raadplegingsperiode tot stand te brengen.

>[!NOTE]
>
>Als de brongegevens geen kolom hebben die kan worden gebruikt om een terugzoekperiode te bepalen, dan zullen alle decile klassenrankings onder `decileMonthAll` worden uitgevoerd.

#### Samenvoeging

Gebruik algemene tabelexpressies (CTE) om de kilometerstand samen te voegen voordat u decile-emmers maakt. Dit levert de totale mijl voor een specifieke terugkijkperiode. CTEs bestaat tijdelijk en is slechts bruikbaar binnen het werkingsgebied van de grotere vraag.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

Het blok wordt tweemaal herhaald in het malplaatje (`summed_miles_3` en `summed_miles_6`) met een verandering in de datumberekening om de gegevens voor de andere raadplegingsperiodes te produceren.

Het is belangrijk om van de identiteit, de afmeting, en metrische kolommen voor de vraag (`membershipNumber`, `loyaltyStatus` en `totalMiles` respectievelijk) nota te nemen.

#### Rangschikking

Met Deciles kunt u categoriale bucketing uitvoeren. Om het rangschikkingsaantal tot stand te brengen, wordt de functie `NTILE` gebruikt met een parameter van `10` binnen een VENSTER dat door het `loyaltyStatus` gebied wordt gegroepeerd. Dit resulteert in een rangorde van 1 tot 10. Plaats de `ORDER BY` clausule van `WINDOW` aan `DESC` om ervoor te zorgen dat een het rangschikken waarde van `1` aan **grootste** metrisch binnen de afmeting wordt gegeven.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### Kaartaggregatie

Met meerdere terugzoekperiodes moet u de decile emmermaps vooraf maken met de functies `MAP_FROM_ARRAYS` en `COLLECT_LIST` . In het voorbeeldfragment maakt `MAP_FROM_ARRAYS` een kaart met twee sleutels (`loyaltyStatus`) en waardenarrays (`decileBucket`). `COLLECT_LIST` retourneert een array met alle waarden in de opgegeven kolom.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>De samenvoeging van de kaart is niet nodig als het decile rangschikken slechts voor een levensperiode wordt vereist.

#### Unieke identiteiten

De lijst van unieke identiteiten (`membershipNumber`) wordt vereist om een unieke lijst van alle lidmaatschappen tot stand te brengen.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Als decile het rangschikken slechts voor een levensperiode wordt vereist, kan deze stap worden weggelaten en samenvoeging door `membershipNumber` kan in de definitieve stap worden gedaan.

#### Alle tijdelijke gegevens samenvoegen

De laatste stap bestaat uit het samenvoegen van alle tijdelijke gegevens in een formulier dat identiek is aan de structuur van de streepjes in de veldgroep.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

Als slechts levengegevens beschikbaar zijn, zou uw vraag als volgt verschijnen:

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

Een correlatie tussen het rangschikkende aantal en percentiel wordt gewaarborgd in de vraagresultaten wegens het gebruik van deciles. Elke rang is gelijk aan 10%, zodat het identificeren van een publiek dat op top 30% wordt gebaseerd slechts ranks 1, 2, en 3 hoeft te richten.

### De querysjabloon uitvoeren

Stel de vraag in werking om de decile dataset te bevolken. U kunt de vraag als malplaatje ook bewaren en het plannen om bij een kadentie te lopen. Als de query als een sjabloon wordt opgeslagen, kan deze ook worden bijgewerkt met het patroon voor maken en invoegen dat verwijst naar de opdracht `table_exists` . Meer informatie over hoe te om het `table_exists` bevel te gebruiken kan in de [ SQL syntaxisgids ](../sql/syntax.md#table-exists) worden gevonden.

## Volgende stappen

Het bovenstaande voorbeeld gebruikt benadrukt stappen om op decile-gebaseerde afgeleide datasets beschikbaar te maken in het Profiel van de Klant in real time. Dit staat voor de Dienst van de Segmentatie, of via een gebruikersinterface of RESTful API, toe om publiek te kunnen produceren dat op deze decile emmers wordt gebaseerd. Zie het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md) voor informatie over hoe te tot stand brengen, evalueren, en tot segmenten toegang hebben.
