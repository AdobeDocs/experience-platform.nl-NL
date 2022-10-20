---
title: Query-versnelde rapportage-inzichten voor opslag
description: Leer hoe te om een rapporterend gegevensmodel van inzichten door de Dienst van de Vraag voor gebruik met versnelde opslaggegevens en user-defined dashboards te bouwen.
source-git-commit: 9c18432bbd9322aee1924c34cb10aadac440e726
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Vraag versnelde opslag die inzichten rapporteert

De vraag versnelde opslag staat u toe om de tijd en de verwerkingscapaciteit te verminderen die wordt vereist om kritieke inzichten van uw gegevens te bereiken. Doorgaans worden gegevens regelmatig verwerkt (bijvoorbeeld op uurbasis of dagelijks), waar geaggregeerde weergaven worden gemaakt en gerapporteerd. De analyse van deze verslagen, die op basis van geaggregeerde gegevens zijn opgesteld, leidt tot inzichten die tot doel hebben de bedrijfsresultaten te verbeteren. De opslag met query-versnelling biedt een cacheservice, gelijktijdige uitvoering, een interactieve ervaring en een stateless API. Er wordt echter aangenomen dat de gegevens vooraf worden verwerkt en geoptimaliseerd voor geaggregeerd opvragen en niet voor onbewerkte opvragen van gegevens.

Met de opslag met query-versnelling kunt u een aangepast gegevensmodel maken en/of uitbreiden op bestaande Real-time Customer Data Platform-gegevensmodellen. Vervolgens kunt u naar keuze uw rapportinzichten gebruiken of insluiten in een rapportage-/visualisatieframework van uw keuze. Het CDP gegevensmodel in real time van Adobe Experience Platform verstrekt inzichten op profielen, segmenten, en bestemmingen en laat in real time CDP inzicht dashboards toe. Dit document begeleidt u door het proces om uw rapporteringsgegevensmodel van inzicht te creëren en ook hoe te om CDP gegevensmodellen in real time uit te breiden zoals nodig.

## Vereisten

In deze zelfstudie worden door de gebruiker gedefinieerde dashboards gebruikt om gegevens van uw aangepaste gegevensmodel in de gebruikersinterface van het Platform te visualiseren. Zie de [door de gebruiker gedefinieerde dashboarddocumentatie](../../dashboards/user-defined-dashboards.md) voor meer informatie over deze functie.

## Aan de slag

Distiller SKU van Gegevens wordt vereist om een model van douanegegevens voor uw rapporteringsinzichten te bouwen en de CDP gegevensmodellen in real time uit te breiden die verrijkte gegevens van het Platform houden. Zie de [verpakking](../packages.md), [guardrails](../guardrails.md#query-accelerated-store), en [licenties](../data-distiller/licence-usage.md) documentatie die betrekking heeft op de gegevens Distiller SKU. Als u geen gegevens Distiller SKU hebt, kunt u voor meer informatie contact opnemen met een medewerker van de klantenservice van de Adobe.

## Een gegevensmodel voor het rapporteren van inzichten maken

In deze zelfstudie wordt een voorbeeld gebruikt van het bouwen van een gegevensmodel voor inzicht van het publiek. Als u een of meer adverteerderplatforms gebruikt om uw publiek te bereiken, kunt u de API van de adverteerder gebruiken om een geschatte gelijke telling van uw publiek te krijgen.

Aan het begin hebt u een eerste gegevensmodel uit uw bronnen (mogelijk via de API van uw adverteerderplatform). Als u een geaggregeerde weergave van uw onbewerkte gegevens wilt maken, maakt u een model voor rapportinzichten, zoals hieronder in de afbeelding wordt beschreven. Dit staat voor één dataset toe om de hogere en lagere grenzen van de publieksgelijke te krijgen.

![Een entiteitrelationeel diagram (ERD) van het gebruikersmodel voor inzicht van het publiek.](../images/query-accelerated-store/audience-insight-user-model.png)

In dit voorbeeld wordt `externalaudiencereach` table/dataset is gebaseerd op identiteitskaart en volgt de lagere en hogere grenzen voor gelijke telling. De `externalaudiencemapping` De afmetinglijst/dataset brengt externe identiteitskaart aan een bestemming en een segment op Platform in kaart.

## Een model maken voor het rapporteren van inzichten met Data Distiller

Maak vervolgens een rapportagemodel (`audienceinsight` in dit voorbeeld) en gebruik de SQL-opdracht `ACCOUNT=acp_query_batch and TYPE=QSACCEL` om ervoor te zorgen dat deze wordt gemaakt in de versnelde opslag. Dan gebruik de Dienst van de Vraag om een `audienceinsight.audiencemodel` schema voor het `audienceinsight` database.

>[!NOTE]
>
>De gegevens Distiller SKU wordt vereist voor `ACCOUNT=acp_query_batch` gebruiken. Zonder dit, wordt een regelmatig gegevensmodel gecreeerd op het gegevens meer.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## Tabellen, relaties en gegevens vullen

Nu hebt u uw `audienceinsight` rapportagemodel, het `externalaudiencereach` en `externalaudiencemapping` tabellen en leggen onderlinge relaties vast. Gebruik vervolgens de `ALTER TABLE` gebruiken om een beperking voor vreemde sleutels tussen de tabellen toe te voegen en een relatie te definiëren. In het volgende SQL-voorbeeld wordt getoond hoe u dit doet.

```sql
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencereach
WITH ( DISTRIBUTION = REPLICATE ) AS
  SELECT cast(null as int) approximate_count_upper_bound,
         cast(null as string) deliverystatusdescription,
         cast(null as timestamp)  timeupdated ,
         cast(null as int) operationstatuscode ,
         cast(null as string) operationstatusdescription,
         cast(null as int) approximate_count_lower_bound,
         cast(null as timestamp)timecreated ,
         cast(null as timestamp)timecontentupdated ,
         cast(null as int) deliverystatuscode ,
         cast(null as int)  ext_custom_audience_id
   WHERE false;
 
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencemapping
WITH ( DISTRIBUTION = REPLICATE ) AS
SELECT cast(null as int) segment_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

Na de succesvolle uitvoering van beide `ALTER TABLE` bevelen, wordt het verband tussen het feit en afmetinglijsten gevormd.

Wanneer de instructies zijn uitgevoerd, gebruikt u de opdracht `SHOW datagroups;` bevel om een lijst van de beschikbare datasets op de versnelde opslag van terug te keren `audienceinsight.audiencemodel`. De tabellarische resultaten moeten overeenkomen met het onderstaande voorbeeld.

>[!IMPORTANT]
>
>Slechts zijn de gegevens in de versnelde opslag toegankelijk van het stateless API eindpunt van de Dienst van de Vraag `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## Vraag het rapporterende gegevensmodel van het inzicht

De Dienst van de Vraag van het gebruik om te vragen `audiencemodel.externalaudiencereach` dimensietabel. Een voorbeeldvraag kan hieronder worden gezien.

```sql
SELECT a.ext_custom_audience_id,
       a.approximate_count_upper_bound
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.externalaudiencemapping AS b
                    ON ( ( a.ext_custom_audience_id ) =
                         ( b.ext_custom_audience_id ) )
GROUP  BY a.ext_custom_audience_id,
          a.approximate_count_upper_bound
LIMIT  5000 ;
```

De tabellarische resultaten bevatten een telling en een id.

```console
ext_custom_audience_id | approximate_count_upper_bound
------------------------+-------------------------------
 23850912218170554      |                          1000
 23850808585120554      |                       1012000
 23850808585220554      |                        100000
 23850814978560554      |                          1000
 23850808585180554      |                        421000
 23850814978510554      |                       3001000
 23850814978530554      |                        300000
 23850912218160554      |                        105000
 23850808584990554      |                          1000
 23850809520110554      |                          1000
(10 rows)
```

## Breid uw gegevensmodel met het Real-time CDP gegevensmodel van inzichten uit

U kunt het publieksmodel uitbreiden met extra details om een rijkere dimensietabel te maken. U kunt bijvoorbeeld de segmentnaam en de doelnaam toewijzen aan de externe publieksidentificatie. Om dit te doen, gebruik de Dienst van de Vraag om een nieuwe dataset tot stand te brengen of te verfrissen en het toe te voegen aan het publieksmodel dat segmenten en bestemmingen met een externe identiteit combineert. In het onderstaande diagram wordt het concept van deze extensie van het gegevensmodel geïllustreerd.

![Een ERD diagram dat het Real-time CDP inzicht gegevensmodel en het Vraag versnelde opslagmodel verbindt.](../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## Tabellen met dimensies maken om uw model met rapportageinzichten uit te breiden

De Dienst van de Vraag van het gebruik om zeer belangrijke beschrijvende attributen van de verrijkte Echte CDP afmetingsdatasets aan toe te voegen `audienceinsight` gegevensmodel en vestigen een verband tussen uw feitenlijst en de nieuwe afmetingslijst. SQL toont hieronder aan hoe te om bestaande afmetinglijsten in uw rapporterend gegevensmodel van inzichten te integreren.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         segment_name,
         destination_status,
         a.destination_id,
         a.segment_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_segments AS b
                      ON ( ( a.segment_id ) = ( b.segment_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

Gebruik de `SHOW datagroups;` bevel om de verwezenlijking van de extra `external_seg_dest_map` dimensietabel.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## Vraag uw uitgebreide versnelde opslagrapportering van inzichten gegevensmodel

Nu `audienceinsight` het gegevensmodel is uitgebreid en is klaar om te worden opgevraagd . In het volgende SQL ziet u de lijst met toegewezen doelen en segmenten.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.segment_name,
       b.destination_status,
       b.destination_id,
       b.segment_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

De vraag keert alle datasets op de vraag versnelde opslag terug:

```console
ext_custom_audience_id | destination_name |       segment_name        | destination_status | destination_id | segment_id 
------------------------+------------------+---------------------------+--------------------+----------------+-------------
 23850808595110554      | FCA_Test2        | United States             | enabled            |     -605911558 | -1357046572
 23850799115800554      | FCA_Test2        | Born in 1980s             | enabled            |     -605911558 | -1224554872
 23850799115790554      | FCA_Test2        | Born in 1970s             | enabled            |     -605911558 |  1899603869
 23850798177620554      | FCA_Test1        | Billionaires              | enabled            |      321720439 |  1401872665
 23850814978560554      | FCA_Test3        | Canada - Saskatchewan     | enabled            |     1182494936 | -1917996562
 23850808585180554      | FCA_Test3        | United States             | enabled            |     1182494936 | -1357046572
 23850814978530554      | FCA_Test3        | Canada - British Columbia | enabled            |     1182494936 |  -652840507
 23850808585120554      | FCA_Test3        | Canada - Quebec           | enabled            |     1182494936 |  -519557860
 23850809520110554      | FCA_Test3        | Born in 1960s             | enabled            |     1182494936 |   237824266
 23850808585220554      | FCA_Test3        | Western Canada            | enabled            |     1182494936 |  1075937528
 23850808584990554      | FCA_Test3        | Canada - Ontario          | enabled            |     1182494936 |  1593438041
 23850814978510554      | FCA_Test3        | Canada - Alberta          | enabled            |     1182494936 |  1862946783
 23850912218170554      | FCA_Test4        | Canada - Alberta          | enabled            |     1549248886 |  1862946783
 23850912218160554      | FCA_Test4        | Born in 1970s             | enabled            |     1549248886 |  1899603869
```

## Visualiseer uw gegevens met door de gebruiker gedefinieerde dashboards

Nu u uw model van douanegegevens hebt gecreeerd, bent u bereid om uw gegevens met douanevragen en user-defined dashboards te visualiseren.

De volgende SQL verstrekt een uitsplitsing van de gelijke telling door publiek in een bestemming en een uitsplitsing van elke bestemming van publiek door segment.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.segment_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.segment_name
ORDER BY b.destination_name
LIMIT  5000
```

De afbeelding hieronder geeft een voorbeeld van de mogelijke aangepaste visualisaties aan de hand van het gegevensmodel voor het rapporteren van inzichten.

![Een gelijke telling door bestemming en segmentwidget die van het nieuwe rapporteringsinzichten gegevensmodel wordt gecreeerd.](../images/query-accelerated-store/user-defined-dashboard-widget.png)

Het aangepaste gegevensmodel vindt u in de lijst met beschikbare gegevensmodellen in de door de gebruiker gedefinieerde dashboardwerkruimte. Zie de [door de gebruiker gedefinieerde dashboardhulplijn](../../dashboards/user-defined-dashboards.md) voor begeleiding op hoe te om uw model van douanegegevens te gebruiken.
