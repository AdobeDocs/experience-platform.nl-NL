---
title: 'Hoofdlettergebruik van op decile gebaseerde afgeleide kenmerken '
description: Deze gids toont de stappen die worden vereist om de Dienst van de Vraag te gebruiken om op decile-Gebaseerde afgeleide attributen voor gebruik met uw gegevens van het Profiel tot stand te brengen.
source-git-commit: 61e0895484b8005e2109056d51557f609fecaf97
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 1%

---

# Gebruiksscenario voor op decile gebaseerde afgeleide kenmerken

De afgeleide attributen vergemakkelijken gecompliceerde gebruiksgevallen voor het analyseren van gegevens van het gegevensmeer die met andere stroomafwaartse diensten van het Platform kunnen worden gebruikt of in uw gegevens van het Profiel van de Klant in real time worden gepubliceerd.

In dit voorbeeldgebruik wordt getoond hoe u op decile gebaseerde afgeleide kenmerken kunt maken voor gebruik met uw gegevens van het profiel van de klant in real time. Gebruikend een scenario van de luchtvaartloyaliteit als voorbeeld, vertelt deze gids u hoe te om een dataset tot stand te brengen die categoriale deciles gebruikt om te segmenteren en publiek tot stand te brengen dat op gerangschikte attributen wordt gebaseerd.

De volgende belangrijke concepten worden geïllustreerd:

* Schema maken voor decile bucketing.
* Categorisch decile maken.
* Creatie van complexe afgeleide kenmerken.
* Berekening van tegels in een terugzoekperiode.
* Een voorbeeldvraag om samenvoeging, rangschikking, en het toevoegen van unieke identiteiten aan te tonen om voor publiek toe te staan dat op deze decile emmers wordt geproduceerd.

## Aan de slag

Deze handleiding vereist een goed begrip van [query-uitvoering in Query-service](../best-practices/writing-queries.md) en de volgende onderdelen van Adobe Experience Platform:

* [Overzicht van het realtime klantprofiel](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Basisbeginselen van de schemacompositie](../../xdm/schema/composition.md): Een inleiding aan de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s.
* [Hoe te om een schema voor het Profiel van de Klant in real time toe te laten](../../profile/tutorials/add-profile-data.md): In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan het realtime profiel van de klant.
* [Een aangepast gegevenstype definiëren](../../xdm/api/data-types.md): De gegevenstypes worden gebruikt als verwijzing-type gebieden in klassen of de groepen van het schemagebied en staan voor het verenigbare gebruik van een multi-gebiedstructuur toe die overal in het schema kan worden omvat.

## Doelstellingen

Het voorbeeld in dit document gebruikt deciles om afgeleide attributen te bouwen voor het rangschikken van gegevens van een schema van de luchtvaartloyaliteit. Met afgeleide kenmerken kunt u het nut van uw gegevens maximaliseren door een publiek te identificeren op basis van de hoogste &#39;n&#39; % voor een gekozen categorie.

## Op decile gebaseerde afgeleide kenmerken maken

Om de rangschikking van deciles te bepalen die op een bepaalde afmeting en overeenkomstige metrisch wordt gebaseerd, moet een schema worden ontworpen om voor het decile knippen toe te staan.

Deze gids gebruikt een dataset van de luchtvaartloyaliteit om aan te tonen hoe te om de Dienst van de Vraag te gebruiken om deciles te bouwen die op mijlen worden gebaseerd die over diverse terugkijkperiodes worden gevlogen.

## De Dienst van de Vraag van het gebruik om deciles tot stand te brengen

Gebruikend de Dienst van de Vraag, kunt u een dataset tot stand brengen die categorische deciles bevat, die dan kan worden gesegmenteerd om publiek tot stand te brengen dat op attributenrangschikking wordt gebaseerd. De concepten die in de volgende voorbeelden worden getoond kunnen worden toegepast om andere decile emmerdatasets tot stand te brengen, zolang een categorie wordt bepaald en metrisch beschikbaar is.

In het voorbeeld worden de gegevens van de luchtvaartmaatschappijen gebruikt voor [XDM ExperienceEvents, klasse](../../xdm/classes/experienceevent.md). Elke gebeurtenis is een overzicht van een zakelijke transactie voor afgelegde kilometers, gecrediteerd of gedebiteerd, en de status van lidmaatschapsloyaliteit van &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; of &quot;Gold&quot;. Het primaire identiteitsveld is `membershipNumber`.

### Voorbeeldgegevenssets

De aanvankelijke dataset van de luchtvaartloyaliteit voor dit voorbeeld is &quot;Gegevens van de Loyalty van de Luchtlijn&quot;, en heeft het volgende schema. Merk op dat de primaire identiteit voor het schema is `_profilefoundationreportingstg.membershipNumber`.

![Een diagram van het gegevensschema voor de luchtkwaliteit.](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**Voorbeeldgegevens**

In de volgende tabel worden de voorbeeldgegevens in het dialoogvenster `_profilefoundationreportingstg` object dat voor dit voorbeeld wordt gebruikt. Het verstrekt context voor het gebruik van decile emmers om complexe afgeleide attributen tot stand te brengen.

>[!NOTE]
>
>Voor de beknoptheid, de inhouds-id `_profilefoundationreportingstg` is weggelaten vanaf het begin van de naamruimte in de kolomtitels en latere vermeldingen in het hele document.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 01-01-2022 | STATUS_MILES | Nieuw lid | 5000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | SILVER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5000 | SILVER |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Nieuwe creditcard | 10000 | FLYER |

{style=&quot;table-layout:auto&quot;}

## Decile-gegevenssets genereren

In de bovenstaande gegevens over de loyaliteit van de luchtvaartmaatschappij `.mileage` waarde bevat het aantal mijl dat een lid per vlucht aflegt. Dit gegeven wordt gebruikt om deciles voor het aantal mijlen tot stand te brengen die over levenraadplegingen en een verscheidenheid van terugzoekperiodes worden gevlogen. Voor dit doel wordt een dataset gecreeerd die deciles in een type van kaartgegevens voor elke raadplegingsperiode bevat en aangewezen decile voor elke raadplegingsperiode die onder wordt toegewezen `membershipNumber`.

Creeer een &quot;Airline Loyalty Decile Schema&quot;om een decile dataset tot stand te brengen gebruikend de Dienst van de Vraag.

![Een diagram van het &quot;Airline Loyalty Decile Schema&quot;.](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### Het schema inschakelen voor Real-time klantprofiel

Gegevens die in Experience Platform worden opgenomen voor gebruik door Real-time Klantprofiel moeten in overeenstemming zijn met [een XDM-schema (Experience Data Model) dat is ingeschakeld voor Profiel](../../xdm/ui/resources/schemas.md). Een schema kan alleen worden ingeschakeld voor Profiel als het de klasse XDM Individual Profile of XDM ExperienceEvent implementeert.

[Laat uw schema voor gebruik in het Profiel van de Klant in real time toe gebruikend de Registratie API van het Schema](../../xdm/tutorials/create-schema-api.md) of de [Gebruikersinterface Schema-editor](../../xdm/tutorials/create-schema-ui.md).  Gedetailleerde instructies over hoe te om een schema voor Profiel toe te laten zijn beschikbaar in hun respectieve documentatie.

Maak vervolgens een gegevenstype dat opnieuw moet worden gebruikt voor alle op decile betrekking hebbende veldgroepen. Het maken van de decile-veldgroep is een eenmalige stap per sandbox. Het kan ook voor alle op decile betrekking hebbende regelingen opnieuw worden gebruikt.

### Een naamruimte voor identiteit maken en markeren als primaire id {#identity-namespace}

Om het even welk schema dat voor gebruik met deciles wordt gecreeerd moet een primaire toegewezen identiteit hebben. U kunt [een identiteitsveld definiëren in de gebruikersinterface van Adobe Experience Platform-schema&#39;s](../../xdm/ui/fields/identity.md#define-an-identity-field)of via de [Schema-register-API](../../xdm/api/descriptors.md#create).

De Dienst van de vraag staat u ook toe om een identiteit of een primaire identiteit voor de gebieden van de ad hoc schemadataset direct door SQL te plaatsen. Zie de documentatie op [het plaatsen van een secundaire identiteit en primaire identiteit in ad hoc schemaidentiteiten](../data-governance/ad-hoc-schema-identities.md) voor meer informatie .

### Creeer een vraag voor het berekenen van deciles over een raadplegingsperiode {#create-a-query}

In het volgende voorbeeld wordt de SQL-query getoond voor het berekenen van een decile-bewerking over een terugzoekperiode.

Een malplaatje kan of gebruikend de Redacteur van de Vraag in UI, of door worden gemaakt [Query Service-API](../api/query-templates.md#create-a-query-template).

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

#### Termijnen

Het gegevenstype decile bevat een emmertje voor 1, 3, 6, 9, 12, en levenlookbacks. De vraag gebruikt de raadplegingsperiodes van 1, 3, en 6 maanden, zodat zal elke sectie sommige &quot;herhaalde&quot;vragen bevatten om tijdelijke lijsten voor elke raadplegingsperiode tot stand te brengen.

>[!NOTE]
>
>Als de brongegevens geen kolom hebben die kan worden gebruikt om een raadplegingsperiode te bepalen, dan zullen alle decile klassenrankings onder worden uitgevoerd `decileMonthAll`.

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

Het blok wordt tweemaal herhaald in de sjabloon (`summed_miles_3` en `summed_miles_6`) met een wijziging in de datumberekening om de gegevens voor de andere terugzoekperioden te genereren.

Het is belangrijk om van de identiteit, de afmeting, en metrische kolommen voor de vraag nota te nemen (`membershipNumber`, `loyaltyStatus` en `totalMiles` respectievelijk).

#### Rangorde

Met Deciles kunt u categoriale bucketing uitvoeren. Als u het rangschikkingsnummer wilt maken, `NTILE` functie wordt gebruikt met een parameter van `10` binnen een VENSTER gegroepeerd door de `loyaltyStatus` veld. Dit resulteert in een rangorde van 1 tot 10. Stel de `ORDER BY` bepaling van de `WINDOW` tot `DESC` om ervoor te zorgen dat een `1` wordt gegeven aan de **grootste** metrisch binnen de afmeting.

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

Met veelvoudige raadplegingsperiodes, moet u de decile emmer kaarten vooraf creëren gebruikend `MAP_FROM_ARRAYS` en `COLLECT_LIST` functies. In het voorbeeldfragment: `MAP_FROM_ARRAYS` maakt een kaart met twee toetsen (`loyaltyStatus`) en waarden (`decileBucket`). `COLLECT_LIST` retourneert een array met alle waarden in de opgegeven kolom.

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

De lijst met unieke identiteiten (`membershipNumber`) is vereist om een unieke lijst met alle lidmaatschappen te maken.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Als decile het rangschikken slechts voor een levensperiode wordt vereist, kan deze stap worden weggelaten en samenvoeging door `membershipNumber` kan worden uitgevoerd in de laatste stap.

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

Stel de vraag in werking om de decile dataset te bevolken. U kunt de vraag als malplaatje ook bewaren en het plannen om bij een kadentie te lopen. Als de query als een sjabloon wordt opgeslagen, kan deze ook worden bijgewerkt met het patroon voor maken en invoegen dat verwijst naar het `table_exists` gebruiken. Meer informatie over het gebruik van de `table_exists`kunt u vinden in het dialoogvenster [SQL-syntaxishandleiding](../sql/syntax.md#table-exists).

## Volgende stappen

Het bovenstaande voorbeeld van het gebruik markeert de stappen waarmee u decile-kenmerken beschikbaar kunt maken in het realtime profiel van de klant. Dit staat voor de Dienst van de Segmentatie, of via een gebruikersinterface of RESTful API, toe om publiek te kunnen produceren dat op deze decile emmers wordt gebaseerd. Zie de [Overzicht van segmentatieservice](../../segmentation/home.md) voor informatie over om, segmenten tot stand te brengen te evalueren en toegang te hebben.

