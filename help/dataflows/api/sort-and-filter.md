---
title: Reacties sorteren en filteren in de Flow Service API
description: Deze zelfstudie behandelt de syntaxis voor sorteren en filteren met behulp van queryparameters in de Flow Service API, inclusief enkele geavanceerde gebruiksgevallen.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: c7ff379b260edeef03f8b47f932ce9040eef3be2
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---

# Reacties sorteren en filteren in de Flow Service API

Bij het uitvoeren van aanbiedingen (GET) in het dialoogvenster [Flow Service-API](https://www.adobe.io/experience-platform-apis/references/flow-service/)kunt u queryparameters gebruiken om reacties te sorteren en te filteren. Deze handleiding bevat een referentie voor het gebruik van deze parameters voor verschillende gebruiksgevallen.

## Sorteren

U kunt reacties sorteren met een `orderby` query-param. De volgende bronnen kunnen worden gesorteerd in de API:

* [Verbindingen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Bronverbindingen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Doelverbindingen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Stromen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Runs](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Als u de parameter wilt gebruiken, moet u de waarde ervan instellen op de specifieke eigenschap waarop u wilt sorteren (bijvoorbeeld `?orderby=name`). U kunt de waarde vooraf toevoegen met een plusteken (`+`) voor oplopende of minteken (`-`) voor aflopende volgorde. Als er geen voorvoegsel voor de volgorde is opgegeven, wordt de lijst standaard in oplopende volgorde gesorteerd.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

U kunt een sorteerparameter ook combineren met een filterparameter door een &quot;en&quot;-symbool (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filteren

U kunt reacties filteren met een `property` parameter met een expressie van een sleutelwaarde. Bijvoorbeeld: `?property=id==12345` alleen bronnen retourneert waarvan `id` eigenschap is exact gelijk aan `12345`.

Filteren kan algemeen worden toegepast op elke eigenschap in een entiteit, zolang het geldige pad naar die eigenschap bekend is.

>[!NOTE]
>
>Als een eigenschap binnen een arrayitem is genest, moet u vierkante haakjes toevoegen (`[]`) aan de array in het pad. Zie de sectie over [filteren op array-eigenschappen](#arrays) voor voorbeelden.

**Hiermee worden alle bronverbindingen geretourneerd waar de naam van de brontabel is `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Retourneer alle stromen voor een specifieke segment-id:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Filters combineren

Meerdere `property` filters kunnen in een query worden opgenomen op voorwaarde dat ze door &#39;en&#39;-tekens worden gescheiden (`&`). Bij het combineren van filters wordt een AND-relatie verondersteld, wat betekent dat een entiteit aan alle filters moet voldoen om in de respons te worden opgenomen.

**Retourneer alle ingeschakelde stromen voor een segment-id:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filteren op array-eigenschappen {#arrays}

U kunt filteren op basis van de eigenschappen van items binnen arrays door het toevoegen `[]` naar de naam van de array-eigenschap.

**De stromen van de terugkeer die met specifieke bronverbindingen worden geassocieerd:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Retourstromen met een transformatie die een specifieke id voor de selecteerwaarde bevat:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Bronverbindingen van de terugkeer die een kolom met specifieke hebben `name` waarde:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Zoek omhoog identiteitskaart van de stroomlooppas voor een bestemming door op segmentidentiteitskaart te filtreren:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Elke filterquery kan worden toegevoegd `count` queryparameter met een waarde van `true` om het aantal resultaten te retourneren. De API-reactie bevat een `count` eigenschap waarvan de waarde het aantal totaal gefilterde items vertegenwoordigt. De daadwerkelijke gefilterde punten zijn niet teruggekeerd in deze vraag.

**Retourneer het aantal ingeschakelde stromen in het systeem:**

```http
GET /flows?property=state==enabled&count=true
```

De reactie op de bovenstaande query ziet er als volgt uit:

```json
{
  "count": 95
}
```

### Filterbare eigenschappen per bron

Afhankelijk van de entiteit van de Dienst van de Stroom u terugwint, kunnen de verschillende eigenschappen voor het filtreren worden gebruikt. De lijsten hieronder onderverdelen onderaan de wortel-vlakke gebieden voor elk middel die algemeen in het filtreren gebruiksgevallen worden gebruikt.

**`connectionSpec`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style="table-layout:auto"}

**`flowSpec`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`flow`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style="table-layout:auto"}

**`run`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## Gebruiksscenario’s {#use-cases}

Lees deze sectie voor sommige specifieke voorbeelden van hoe u het filtreren en het sorteren kunt gebruiken om informatie over bepaalde schakelaars terug te keren of u bij het zuiveren van kwesties te helpen. Als er nog meer gebruiksgevallen zijn die u door de Adobe wilt toevoegen, kunt u de **[!UICONTROL Detailed feedback options]** op de pagina om een aanvraag in te dienen.

**Filter om verbindingen naar een bepaald doel te retourneren**

U kunt filters gebruiken om verbindingen naar slechts bepaalde bestemmingen terug te keren. Eerst zoekt u de `connectionSpecs` eindpunt zoals hieronder:

```http
GET /connectionSpecs
```

Zoek vervolgens naar de gewenste `connectionSpec` door de `name` parameter. Zoek bijvoorbeeld naar Amazon Ads, of Pega, of SFTP, enzovoort in de `name` parameter. De overeenkomstige `id` is de `connectionSpec` die u kunt zoeken door in de volgende API vraag te zoeken.

U kunt bijvoorbeeld uw doelen filteren om alleen bestaande verbindingen met Amazon S3-verbindingen te retourneren:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filter om gegevensstromen te retourneren naar alleen doelen**

Bij het opvragen van `/flows` eindpunt, in plaats van het terugkeren van alle bronnen en bestemmingsdataflows, kunt u een filter gebruiken om dataflows aan bestemmingen slechts terug te keren. Om dit te doen, gebruik `isDestinationFlow` als queryparameter, zoals:

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filter om gegevens alleen naar een bepaalde bron of bestemming te retourneren**

U kunt dataflows filtreren om dataflows aan een bepaalde bestemming of van een bepaalde bron slechts terug te keren. U kunt bijvoorbeeld uw doelen filteren om alleen bestaande verbindingen met Amazon S3-verbindingen te retourneren:

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filter om alle runtime van een gegevensstroom voor een specifieke periode te krijgen**

U kunt dataflow looppas van een dataflow filtreren om looppas in een bepaald tijdinterval slechts te bekijken, zoals hieronder:

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filter om alleen mislukte gegevensstromen te retourneren**

Voor het zuiveren doeleinden, kunt u alle ontbroken dataflow looppas voor een bepaalde bron of bestemmingsdataflow, zoals hieronder filtreren en zien:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Volgende stappen

In deze handleiding wordt beschreven hoe u de `orderby` en `property` De parameters van de vraag aan soort en filterreacties in de Dienst API van de Stroom. Zie de API-zelfstudies in het dialoogvenster [bronnen](../../sources/home.md) en [bestemmingen](../../destinations/home.md) documentatie.
