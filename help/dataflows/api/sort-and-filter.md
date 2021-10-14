---
title: Reacties sorteren en filteren in de Flow Service API
description: Deze zelfstudie behandelt de syntaxis voor sorteren en filteren met behulp van queryparameters in de Flow Service API, inclusief enkele geavanceerde gebruiksgevallen.
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Reacties sorteren en filteren in de Flow Service API

Wanneer het uitvoeren van lijst (GET) verzoeken in [de Dienst API van de Stroom](https://www.adobe.io/experience-platform-apis/references/flow-service/), kunt u vraagparameters gebruiken om reacties te sorteren en te filtreren. Deze handleiding bevat een referentie voor het gebruik van deze parameters voor verschillende gebruiksgevallen.

## Sorteren

U kunt reacties sorteren door een `orderby` vraagparam te gebruiken. De volgende bronnen kunnen worden gesorteerd in de API:

* [Verbindingen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Bronverbindingen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Doelverbindingen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Stromen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Runs](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Als u de parameter wilt gebruiken, moet u de waarde ervan instellen op de specifieke eigenschap waarop u wilt sorteren (bijvoorbeeld `?orderby=name`). U kunt de waarde met een plusteken (`+`) voor het stijgen orde of minteken (`-`) voor het dalende orde toevoegen. Als er geen voorvoegsel voor de volgorde is opgegeven, wordt de lijst standaard in oplopende volgorde gesorteerd.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

U kunt een sorterende parameter met een het filtreren parameter ook combineren door een &quot;en&quot;symbool (`&`) te gebruiken.

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filteren

U kunt reacties filteren door een `property` parameter met een zeer belangrijke uitdrukking te gebruiken. `?property=id==12345` retourneert bijvoorbeeld alleen bronnen waarvan de eigenschap `id` exact `12345` is.

Filteren kan algemeen worden toegepast op elke eigenschap in een entiteit, zolang het geldige pad naar die eigenschap bekend is.

>[!NOTE]
>
>Als een eigenschap is genest binnen een arrayitem, moet u vierkante haakjes (`[]`) toevoegen aan de array in het pad. Zie de sectie over [filteren op array-eigenschappen](#arrays) voor voorbeelden.

**Retourneer alle bronverbindingen waarbij de naam van de brontabel  `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Retourneer alle stromen voor een specifieke segment-id:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Filters combineren

De veelvoudige `property` filters kunnen in een vraag worden omvat op voorwaarde dat zij door &quot;en&quot;karakters (`&`) worden gescheiden. Bij het combineren van filters wordt een AND-relatie verondersteld, wat betekent dat een entiteit aan alle filters moet voldoen om in de respons te worden opgenomen.

**Retourneer alle ingeschakelde stromen voor een segment-id:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filteren op array-eigenschappen {#arrays}

U kunt filteren op basis van de eigenschappen van items binnen arrays door `[]` toe te voegen aan de naam van de array-eigenschap.

**De stromen van de terugkeer die met specifieke bronverbindingen worden geassocieerd:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Retourstromen met een transformatie die een specifieke id voor de selecteerwaarde bevat:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**De bronverbindingen van de terugkeer die een kolom met een specifieke  `name` waarde hebben:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Zoek omhoog identiteitskaart van de stroomlooppas voor een bestemming door op segmentidentiteitskaart te filtreren:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Om het even welke het filtreren vraag kan met `count` vraagparameter met een waarde van `true` worden toegevoegd om de telling van de resultaten terug te keren. De API reactie bevat een `count` bezit de waarvan waarde telling van totaal gefilterde punten vertegenwoordigt. De daadwerkelijke gefilterde punten zijn niet teruggekeerd in deze vraag.

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

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

**`run`**

| Eigenschap | Voorbeeld |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

Deze gids behandelde hoe te om `orderby` en `property` vraagparameters te gebruiken om reacties in de Dienst API van de Stroom te sorteren en te filtreren. Voor geleidelijke gidsen over hoe te om API voor gemeenschappelijke werkschema&#39;s in Platform te gebruiken, zie de API leerprogramma&#39;s in de [bronnen](../../sources/home.md) en [bestemmingen](../../destinations/home.md) documentatie.
