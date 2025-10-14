---
title: Reacties sorteren en filteren in de Flow Service API
description: Deze zelfstudie behandelt de syntaxis voor sorteren en filteren met behulp van queryparameters in de Flow Service API, inclusief enkele geavanceerde gebruiksgevallen.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Reacties sorteren en filteren in de Flow Service API

Wanneer het uitvoeren van lijst (GET) verzoeken in de [&#x200B; Dienst API van de Stroom &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/), kunt u vraagparameters gebruiken om reacties te sorteren en te filtreren. Deze handleiding bevat een referentie voor het gebruik van deze parameters voor verschillende gebruiksgevallen.

## Sorteren

U kunt antwoorden sorteren met behulp van een `orderby` query-parameter. De volgende bronnen kunnen worden gesorteerd in de API:

* [&#x200B; Verbindingen &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [&#x200B; de verbindingen van Source &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [&#x200B; de verbindingen van het Doel &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [&#x200B; Stromen &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [&#x200B; Lopen &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Als u de parameter wilt gebruiken, moet u de waarde ervan instellen op de specifieke eigenschap waarop u wilt sorteren (bijvoorbeeld `?orderby=name` ). U kunt de waarde met een plusteken (`+`) voor het stijgen orde of minteken (`-`) voor het dalende orde toevoegen. Als er geen voorvoegsel voor de volgorde is opgegeven, wordt de lijst standaard in oplopende volgorde gesorteerd.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

U kunt een sorterende parameter met een het filtreren parameter ook combineren door &quot;en&quot;symbool (`&`) te gebruiken.

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filteren

U kunt reacties filteren door een parameter `property` te gebruiken met een expressie met sleutelwaarden. `?property=id==12345` retourneert bijvoorbeeld alleen bronnen waarvan de eigenschap `id` exact gelijk is aan `12345` .

Filteren kan algemeen worden toegepast op elke eigenschap in een entiteit, zolang het geldige pad naar die eigenschap bekend is.

>[!NOTE]
>
>Als een bezit binnen een seriepunt wordt genesteld, moet u vierkante haakjes (`[]`) aan de serie in de weg toevoegen. Zie de sectie op [&#x200B; het filtreren op serieeigenschappen &#x200B;](#arrays) voor voorbeelden.

**keer alle bronverbindingen terug waar de naam van de bronlijst `lead` is:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Terugkeer alle stromen voor specifieke segmentidentiteitskaart:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Filters combineren

Meerdere `property` -filters kunnen in een query worden opgenomen, op voorwaarde dat ze door &#39;en&#39;-tekens (`&`) worden gescheiden. Bij het combineren van filters wordt een AND-relatie verondersteld, wat betekent dat een entiteit aan alle filters moet voldoen om in de respons te worden opgenomen.

**Terugkeer alle toegelaten stromen voor segmentidentiteitskaart:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filteren op array-eigenschappen {#arrays}

U kunt filteren op basis van de eigenschappen van items binnen arrays door `[]` aan de naam van de array-eigenschap toe te voegen.

**stromen van de Terugkeer die met specifieke bronverbindingen worden geassocieerd:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**stromen van de Terugkeer die een transformatie hebben die een specifieke identiteitskaart van de selecteurswaarde bevatten:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**de bronverbindingen van de Terugkeer die een kolom met een specifieke `name` waarde hebben:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**kijkt omhoog stroom in werking stelt identiteitskaart voor een bestemming door op segmentidentiteitskaart te filtreren:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Elke filterquery kan worden toegevoegd met de parameter `count` query met de waarde `true` om het aantal resultaten te retourneren. De API-reactie bevat een eigenschap `count` waarvan de waarde het aantal totaal gefilterde items vertegenwoordigt. De daadwerkelijke gefilterde punten zijn niet teruggekeerd in deze vraag.

**keer de telling van toegelaten stromen in het systeem terug:**

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

Lees deze sectie voor sommige specifieke voorbeelden van hoe u het filtreren en het sorteren kunt gebruiken om informatie over bepaalde schakelaars terug te keren of u bij het zuiveren van kwesties te helpen. Als er nog meer gebruiksgevallen zijn die Adobe moet toevoegen, kunt u een aanvraag indienen met de tekst **[!UICONTROL Detailed feedback options]** op de pagina.

**Filter om verbindingen aan een bepaalde slechts bestemming terug te keren**

U kunt filters gebruiken om verbindingen naar slechts bepaalde bestemmingen terug te keren. Ga eerst als volgt naar het eindpunt van `connectionSpecs` :

```http
GET /connectionSpecs
```

Zoek vervolgens naar de gewenste `connectionSpec` door de parameter `name` te inspecteren. Zoek bijvoorbeeld naar Amazon Ads, of Pega, of SFTP, enzovoort in de parameter `name` . Het corresponderende `id` is de `connectionSpec` waarnaar u kunt zoeken in de volgende API-aanroep.

U kunt bijvoorbeeld uw doelen filteren om alleen bestaande verbindingen met Amazon S3-verbindingen te retourneren:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filter om dataflows aan bestemmingen slechts terug te keren**

Wanneer het vragen van het `/flows` eindpunt, in plaats van het terugkeren van alle bronnen en bestemmingsdataflows, kunt u een filter gebruiken om dataflows aan bestemmingen slechts terug te keren. Hiervoor gebruikt u `isDestinationFlow` als queryparameter, zoals:

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filter om dataflows aan een bepaalde bron of een bestemming slechts terug te keren**

U kunt dataflows filtreren om dataflows aan een bepaalde bestemming of van een bepaalde bron slechts terug te keren. U kunt bijvoorbeeld uw doelen filteren om alleen bestaande verbindingen met Amazon S3-verbindingen te retourneren:

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filter om alle looppas van een dataflow voor een specifieke tijd-periode** te krijgen

U kunt dataflow looppas van een dataflow filtreren om looppas in een bepaald tijdinterval slechts te bekijken, zoals hieronder:

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filter om ontbroken gegevens terug te keren slechts**

Voor het zuiveren doeleinden, kunt u alle ontbroken dataflow looppas voor een bepaalde bron of bestemmingsdataflow, zoals hieronder filtreren en zien:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Volgende stappen

In deze handleiding wordt beschreven hoe u de query-parameters `orderby` en `property` kunt gebruiken om reacties in de Flow Service API te sorteren en te filteren. Voor geleidelijke gidsen op hoe te om API voor gemeenschappelijke werkschema&#39;s in Experience Platform te gebruiken, zie de API leerprogramma&#39;s in de [&#x200B; bronnen &#x200B;](../../sources/home.md) en [&#x200B; documentatie van bestemmingen &#x200B;](../../destinations/home.md).
