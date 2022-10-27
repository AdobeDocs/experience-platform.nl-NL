---
keywords: Experience Platform;query-service;Query-service;geneste gegevensstructuren;geneste gegevens;
title: Werken met geneste gegevensstructuren in Query Service
description: Dit document biedt een werkvoorbeeld voor het verwerken en transformeren van geneste gegevensvelden met CTAS- en INSERT INTO-instructies.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Werken met geneste gegevensstructuren in Query Service

Adobe Experience Platform Query Service ondersteunt het gebruik van geneste gegevensvelden. De complexiteit van bedrijfsgegevensstructuren kan het transformeren of verwerken van deze gegevens ingewikkeld maken. Dit document verstrekt voorbeelden van om, datasets met complexe gegevenstypes met inbegrip van genestelde gegevensstructuren tot stand te brengen te verwerken of om te zetten.

De Dienst van de vraag verstrekt een [!DNL PostgreSQL] interface om SQL vragen op alle datasets in werking te stellen die door Experience Platform worden beheerd. Platform ondersteunt het gebruik van primitieve of complexe gegevenstypen in tabelkolommen, zoals struct, arrays, maps en diep geneste struct, arrays en maps. Datasets kunnen ook geneste structuren bevatten waarbij het gegevenstype van de kolom zo complex kan zijn als een array van geneste structuren, of een kaart met kaarten waarin de waarde van een sleutelwaardepaar een structuur met meerdere nestniveaus kan zijn.

## Aan de slag

Deze zelfstudie vereist het gebruik van een externe PSQL-client of het hulpmiddel Query Editor om query&#39;s te schrijven, te valideren en uit te voeren in de gebruikersinterface van het Experience Platform (UI). Volledige details over hoe te om vragen door UI in werking te stellen kunnen in worden gevonden [Handleiding voor de Query Editor](../ui/user-guide.md). Voor een gedetailleerde lijst waarop de derdeDesktopcliënten met de Dienst van de Vraag kunnen verbinden, zie [Overzicht van clientverbindingen](../clients/overview.md).

U zou ook een goed begrip van moeten hebben `INSERT INTO` en `CTAS` syntaxis. Specifieke informatie over het gebruik ervan is te vinden in het [`INSERT INTO`](../sql/syntax.md#insert-into) en [`CTAS`](../sql/syntax.md#create-table-as-select) van de [Referentiedocumentatie voor SQL-syntaxis](../sql/syntax.md).

## Een gegevensset maken

De dienst van de vraag verstrekt Create Lijst als Uitgezocht (`CTAS`) gebruiken om een tabel te maken op basis van de uitvoer van een `SELECT` -instructie, of zoals in dit geval, door een verwijzing naar een bestaand XDM-schema in Adobe Experience Platform te gebruiken. Hieronder wordt het XDM-schema weergegeven voor `Final_subscription` gemaakt voor dit voorbeeld.

![Een diagram van het final_subscription schema.](../images/best-practices/final-subscription-schema.png)

In het volgende voorbeeld ziet u hoe de SQL wordt gebruikt om de `final_subscription_test2` dataset. `final_subscription_test2` wordt gemaakt met de `Final_subscription` schema. Gegevens worden uit de bron geëxtraheerd met behulp van een `SELECT` component om enkele rijen te vullen.

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

In de oorspronkelijke gegevensset `final_subscription_test2`bevat, wordt het gegevenstype struct gebruikt voor het bevatten van `subscription` en `userid` Dit is uniek voor elke gebruiker. De `subscription` in dit veld worden de productabonnementen voor een gebruiker beschreven. Er kunnen meerdere abonnementen zijn, maar een tabel kan slechts de gegevens voor één abonnement per rij bevatten.

## Geneste gegevensvelden bijwerken met INVOEGEN IN

Na de `final_subscription_test2` dataset is gecreeerd, `INSERT INTO` wordt gebruikt om aanvullende gegevens aan de tabel toe te voegen. Bij het kopiëren van gegevens moeten de gegevenstypen in bron en doel overeenkomen. Het gegevenstype van de bron moet ook `CAST` naar het doelgegevenstype. De stijgende gegevens worden dan toegevoegd in de doeldataset gebruikend volgende SQL.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## Gegevens uit een geneste gegevensset verwerken

Om de lijst van actieve abonnementen van een gebruiker van een dataset te weten te komen, moet u een vraag schrijven die de elementen van een serie in veelvoudige rijen en kolommen scheidt. Hiervoor moet u eerst de vorm van het gegevensmodel begrijpen, aangezien de abonnementsgegevens binnen een array worden bewaard die in de dataset is genest.

De PSQL `\d` wordt gebruikt om niveau door niveau aan de vereiste abonnementsgegevens te navigeren. In de tabellen wordt de structuur van de `final_subscription_test2` dataset. Complexe gegevenstypen kunnen in één oogopslag worden herkend, omdat het geen standaardtekstwaarden zijn, zoals tekst, booleaanse waarden, tijdstempels, enz.

| Kolom | Type |
|--------|-------|
| `_lumaservices3` | final_subscription_test2_lumaservices3 |

De velden van de volgende kolom worden weergegeven met de `\d final_subscription_test2__lumaservices3` gebruiken.

| Kolom | Type |
|---------|-------|
| `userid` | text |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` is een array van struct-elementen. De velden worden weergegeven met de `\d _lumaservices3_subscription_e[]` gebruiken.

| Kolom | Type |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | text |
| `offer_id` | text |
| `subscription_id` | text |

Als u de geneste velden van het abonnement wilt opvragen, moet u eerst de elementen van het `subscription` in meerdere rijen te plaatsen en de resultaten te retourneren met de exploderfunctie. In het volgende SQL-voorbeeld wordt het actieve abonnement voor een gebruiker geretourneerd op `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Deze vereenvoudigde voorbeeldoplossing staat slechts voor één actief gebruikersabonnement toe. In werkelijkheid kunnen er veel actieve abonnementen zijn voor één gebruiker. In het volgende voorbeeld wordt de vorige query gewijzigd om meerdere gelijktijdige actieve abonnementen toe te staan.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

Ondanks de toenemende complexiteit van dit SQL-voorbeeld, `collect_list` voor actieve abonnementen garandeert niet dat de uitvoer in dezelfde volgorde zal zijn als de bron. Als u een lijst met actieve abonnementen voor een gebruiker wilt maken, moet u GROUP BY gebruiken of de volgorde wijzigen om de resultaten van de lijst samen te voegen.

## Volgende stappen

Door dit document te lezen, begrijpt u nu hoe te om datasets te verwerken of om te zetten die complexe gegevenstypes in de Dienst van de Vraag van Adobe Experience Platform gebruiken. Zie de [query-uitvoeringsrichtlijnen](./writing-queries.md) voor meer informatie over het runnen van SQL vragen over datasets binnen het meer van Gegevens.
