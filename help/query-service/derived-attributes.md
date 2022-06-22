---
title: Afgeleide kenmerken
description: Met afgeleide kenmerken kunt u kenmerken op een reguliere cadence berekenen en optioneel deze afgeleide kenmerken in realtime klantprofiel publiceren als profielkenmerken. Dit document biedt een overzicht van hoe u de Query-service kunt gebruiken om afgeleide kenmerken te maken voor gebruik met uw profielgegevens.
source-git-commit: 72e157e0a6310ebf2f55205b03b60600a56e3cf6
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---

# Afgeleide kenmerken

Met afgeleide kenmerken kunt u kenmerken op een reguliere cadence berekenen en optioneel deze afgeleide kenmerken in realtime klantprofiel publiceren als profielkenmerken.

Afgeleide kenmerken, zoals kenmerken die zijn gemaakt met decile-gegevens, zijn nodig voor verschillende gebruiksgevallen waarin profielgegevens worden geanalyseerd. Met behulp van decile-gegevens kunt u soorten publiek maken op basis van hun percentiel of rangschikking van een bepaald kenmerk. Mogelijke gebruiksgevallen zijn bijvoorbeeld:

* De laagste 10% van de abonnees identificeren op basis van viewer per kanaal. Op die manier kunnen marketeers zich richten op een bepaald publiek en een nieuw abonneepakket verkopen.
* Een publiek identificeren dat zich in de top 10% van de vliegers bevindt op basis van hun totale afgelegde kilometers en de &quot;Flyer&quot;-status hebben. Dit publiek zou kunnen worden gebruikt om selectief de verkoop van een nieuw creditcardaanbod te richten.

## Aan de slag

Dit overzicht vereist een goed begrip van [API-aanroepen van Platform](../landing/api-guide.md) en de volgende onderdelen van Adobe Experience Platform:

* [Overzicht van het realtime klantprofiel](../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Basisbeginselen van de schemacompositie](../xdm/schema/composition.md): Een inleiding aan de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s.
* [Hoe te om een schema voor het Profiel van de Klant in real time toe te laten](../profile/tutorials/add-profile-data.md): In deze zelfstudie worden de stappen beschreven die nodig zijn om gegevens toe te voegen aan het realtime profiel van de klant.

## SQL-ondersteuning voor afgeleide kenmerken

Om de rangschikking van tegels te bepalen die op een bepaalde afmeting (categorie) en een overeenkomstige metrisch (opbrengst, punten, kijkerduur, enz.) wordt gebaseerd, moet een schema worden ontworpen om voor het decile opsluiten toe te staan. Dit schema kan als deel van het grotere schema van het Profiel worden gebruikt.

### Een naamruimte voor de identiteit maken voor het profielschema {#identity-namespace}

Identiteitsnaamruimten zijn een component van [Identiteitsservice](../identity-service/home.md) die dienen als indicatoren van de context waarop een identiteit betrekking heeft. Een volledig gekwalificeerde identiteit omvat een waarde van identiteitskaart en een namespace. Wanneer de aanpassing en het samenvoegen van verslaggegevens over profielfragmenten, zowel de identiteitswaarde als namespace moeten aanpassen.

Gegevensbestanden die zijn gemaakt met betrekking tot identiteit kunnen worden gegroepeerd als een gegevensgroep en helpen de levenscyclus van de gegevens te handhaven. U kunt aangepaste naamruimten maken met de opdracht [Identiteitsservice-API](../identity-service/api/create-custom-namespace.md) of via de gebruikersinterface. Zie de [aangepaste documentatie voor naamruimten beheren](../identity-service/namespaces.md#manage-namespaces) voor begeleiding op hoe te om dit door UI te doen.

De primaire identiteitsbeschrijver kan of aan een gebied in Schemas UI worden toegewezen of kan worden gecreeerd gebruikend de Registratie API van het Schema. Zie de documentatie voor instructies over hoe u kunt [Een identiteitsveld definiëren in de gebruikersinterface van Adobe Experience Platform](../xdm/ui/fields/identity.md#define-an-identity-field)of via de [Schema-register-API](../xdm/api/descriptors.md#create).

De Dienst van de vraag staat u ook toe om een identiteit of een primaire identiteit voor de gebieden van de ad hoc schemadataset direct door SQL te plaatsen. Zie de documentatie op [het plaatsen van een secundaire identiteit en primaire identiteit in ad hoc schemaidentiteiten](./data-governance/ad-hoc-schema-identities.md) voor meer informatie .

## Afgeleide kenmerken maken

De voorbeeldvraag die in dit document wordt verstrekt concentreert zich op deciles om grote gegevensreeksen te categoriseren en de gegevens van hoogste te rangschikken aan laagste waarden (of vice versa), en filter die op tijdspanne wordt gebaseerd.

### Deciles {#deciles}

Een decile is een methode om een reeks gerangschikte gegevens op te splitsen in tien gelijke delen. Wanneer de gegevens in deciles worden verdeeld, wordt een decile rang toegewezen aan elke rij in de gegevensreeks. Hierdoor kunnen de gegevens in aflopende of oplopende volgorde worden gesorteerd.

Bij een lagere rangschikking worden de gegevens gerangschikt op een schaal van 1 tot 10, waarbij elk opeenvolgend getal overeenkomt met een verhoging van 10 procentpunten.

Decile emmers vertegenwoordigen het aantal gerangschikte groepen en worden gebruikt om een ranking aan een dimensie (categorie) in de dataset toe te wijzen. Het emmertje kan een aantal of een uitdrukking zijn die tot een positieve geheelwaarde voor elke verdeling evalueert. De emmers mogen geen null-waarde hebben.

De kwartjes worden gebruikt om de verdeling door vier en percentielen door 100 te verdelen.

### Het schema voor het decile-emmertje maken {#create-schema}

Het schema dat voor de decile emmers wordt gecreeerd heeft drie integrale delen: een gegevenstype, een veldgroep voor het gegevenstype (per brondataset) en een primair identiteitsveld.

>[!NOTE]
>
>Er moet een naamruimte voor de identiteit worden gemaakt voordat het schema kan worden gemaakt. Zie de [naamruimte identity](#identity-namespace) voor meer informatie.

Adobe biedt verschillende standaard (&quot;core&quot;) XDM-klassen, waaronder XDM Individual Profile en XDM ExperienceEvent. Naast deze kernklassen kunt u ook uw eigen aangepaste klassen maken om specifieke gebruiksgevallen voor uw organisatie te beschrijven. Zie de hulplijnen over hoe u [schema&#39;s maken en bewerken in de gebruikersinterface](../xdm/ui/resources/schemas.md#create) of door [schema&#39;s eindpunt in de Registratie API van het Schema](../xdm/api/schemas.md#create) voor meer informatie .

Gegevens die in Experience Platform voor gebruik door het Profiel van de Klant in real time worden opgenomen moeten aan een schema van de Gegevens van de Ervaring (XDM) in overeenstemming zijn dat voor Profiel wordt toegelaten. Een schema kan alleen worden ingeschakeld voor Profiel als het de klasse XDM Individual Profile of XDM ExperienceEvent implementeert.

U kunt [laat een schema voor gebruik in het Profiel van de Klant in real time toe gebruikend de Registratie API van het Schema](../xdm/tutorials/create-schema-api.md) of de [Gebruikersinterface Schema-editor](../xdm/tutorials/create-schema-ui.md).  Gedetailleerde instructies over hoe te om een schema voor Profiel toe te laten zijn beschikbaar in hun respectieve documentatie.

### Een gegevenstype maken {#create-data-type}

De gegevenstypes worden gebruikt als verwijzing-type gebieden in klassen of de groepen van het schemagebied en staan voor het verenigbare gebruik van een multi-gebiedstructuur toe die overal in het schema kan worden omvat. Het maken van het gegevenstype is een eenmalige stap per sandbox, aangezien deze stap opnieuw kan worden gebruikt voor alle aan decile gerelateerde veldgroepen.

Zie de documentatie voor instructies over hoe u kunt [een aangepast gegevenstype definiëren](../xdm/api/data-types.md) met de [Schema-register-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### De groep met decile-velden maken {#create-field-group}

Het maken van de veldgroep is een eenmalige stap per sandbox. Het kan ook voor alle op decile betrekking hebbende regelingen opnieuw worden gebruikt.

Zie de documentatie voor instructies over hoe u kunt [veldgroepen maken via de gebruikersinterface](../xdm/ui/resources/field-groups.md#create)

## De Dienst van de Vraag van het gebruik om deciles tot stand te brengen

De Dienst van de vraag verstrekt een ideale manier om een dataset tot stand te brengen die categorische deciles bevat. Dit kan dan samen met de Dienst van de Segmentatie worden gebruikt om publiek tot stand te brengen dat op attributenrangschikking wordt gebaseerd.

De concepten die in de volgende voorbeelden worden getoond kunnen worden toegepast om tot andere decile emmerdatasets te leiden, zolang een categorie (afmeting) wordt bepaald en metrisch beschikbaar is. De voorbeelden zijn gebaseerd op gegevens voor een loyaliteitsregeling voor luchtvaartmaatschappijen. De gegevens van de luchtvaartloyaliteit gebruiken de klasse van de Gebeurtenissen van de Ervaring waar elke gebeurtenis een verslag van een bedrijfstransactie voor is **kilometerstand**, gecrediteerd of gedebiteerd, en het lidmaatschap **loyaliteitsstatus** &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot; of &quot;Gold&quot;. Het primaire identiteitsveld is `membershipNumber`.

### Een querysjabloon maken {#create-a-query-template}

Het malplaatje kan of gebruikend de Redacteur van de Vraag in UI, of door worden gemaakt [Query Service-API](./api/query-templates.md#create-a-query-template).

Secties van de hieronder weergegeven querysjabloon worden gedetailleerder onderzocht.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### Terugkijkperioden

Het gegevenstype decile bevat een emmertje voor 1, 3, 6, 9, 12, en levenblik-rug. De vraag gebruikt de terugblik-achterperiodes van 1, 3, en 6 maanden, zodat zal elke sectie sommige &quot;herhaalde&quot;vragen bevatten om tijdelijke lijsten voor elke terugblik periode tot stand te brengen.

>[!NOTE]
>
>Als de brongegevens geen kolom hebben die kan worden gebruikt om een terugblik-achterperiode te bepalen, dan zullen alle decile klassenrankings onder worden uitgevoerd `decileMonthAll`.

#### Samenvoeging

Gebruik algemene tabelexpressies (CTE) om de kilometerstand samen te voegen voordat u decile-emmers maakt. Dit levert de totale mijl voor een specifieke terugblik periode. CTEs bestaat tijdelijk en is slechts bruikbaar binnen het werkingsgebied van de grotere vraag.

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

Het blok wordt tweemaal herhaald in de sjabloon (`summed_miles_3` en `summed_miles_6`) met een wijziging in de datumberekening om de gegevens voor de andere terugkijkperioden te genereren.

Gelieve te nota van de identiteit, de afmeting, en metrische kolommen voor de vraag (`membershipNumber`, `loyaltyStatus` en `totalMiles` respectievelijk).

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

Met veelvoudige terugblik periodes, moet u de decile emmer kaarten vooraf creëren gebruikend `MAP_FROM_ARRAYS` en `COLLECT_LIST` functies. In het voorbeeldfragment: `MAP_FROM_ARRAYS` maakt een kaart met twee toetsen (`loyaltyStatus`) en waarden (`decileBucket`). `COLLECT_LIST` retourneert een array met alle waarden in de opgegeven kolom.

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

### De querysjabloon uitvoeren

Zoekopdrachten kunnen [uitgevoerd via de gebruikersinterface](./ui/user-guide.md#executing-queries) of de [Query Service-API](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

Een correlatie tussen het rangschikkende aantal en percentiel wordt gewaarborgd in de vraagresultaten wegens het gebruik van deciles. Elke rang is gelijk aan 10%, zodat het identificeren van een publiek dat op top 30% wordt gebaseerd slechts ranks 1, 2, en 3 hoeft te richten.

## Volgende stappen

De Dienst van de segmentatie verstrekt een gebruikersinterface en RESTful API die u toestaat om publiek te produceren dat op deze decile emmers wordt gebaseerd. Zie de [Overzicht van segmentatieservice](../segmentation/home.md) voor informatie over om, segmenten tot stand te brengen te evalueren en toegang te hebben.

Voor gedetailleerde informatie over om segmenten in de Bouwer van het Segment tot stand te brengen en te gebruiken (de implementatie UI van de Dienst van de Segmentatie), zie [Handleiding Segment Builder](../segmentation/ui/overview.md).

Raadpleeg de zelfstudie voor informatie over het samenstellen van segmentdefinities met behulp van de API [publiekssegmenten maken met behulp van de API](../segmentation/tutorials/create-a-segment.md).
