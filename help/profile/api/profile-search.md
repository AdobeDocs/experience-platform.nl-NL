---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# Profielzoekopdracht

Het onderzoek van het profiel wordt gebruikt om configureerbare gebieden te zoeken en te indexeren die over diverse gegevensbronnen worden bevat en hen in bijna real time terug te keren.

Deze handleiding bevat informatie waarmee u het zoeken naar profielen beter kunt begrijpen en voorbeeld-API-aanroepen voor het uitvoeren van basishandelingen met de API.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van Real-time API van het Profiel van de Klant. Lees voordat u verdergaat de handleiding voor ontwikkelaars van [realtime klantprofiel](getting-started.md).

Met name bevat de sectie [Aan de](getting-started.md) slag van de handleiding voor ontwikkelaars van profielen koppelingen naar verwante onderwerpen, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar API&#39;s van het Experience Platform met succes uit te voeren.

### Zoekresultaten ophalen

Het onderzoekseindpunt kan worden gebruikt om onderzoeksresultaten te krijgen die op de waarden van de vereiste `schema.name` parameter en extra facultatieve vraagparameters worden gebaseerd. U kunt meerdere parameters gebruiken, gescheiden door ampersands (&amp;).

**API-indeling**

```http
GET /search?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
|---|---|
| `schema.name` | **Vereist.** De naam van de schemaklasse die de inhoud bevat die moet worden gezocht, in punt-aantekening formaat wordt geschreven. Momenteel wordt alleen `schema.name=_xdm.context.segmentdefinition` ondersteund. |
| `limit` | Het aantal zoekresultaten dat moet worden geretourneerd. De standaardwaarde is 50. |
| `page` | Het paginanummer dat wordt gebruikt voor pagineringsresultaten van de doorzochte query. |
| `s` | Een query die voldoet aan de Microsoft-implementatie van de zoeksyntaxis [van](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Als er geen zoekterm is opgegeven, worden alle records die aan deze zoekterm zijn gekoppeld, `schema.name` geretourneerd. Een meer gedetailleerde uitleg vindt u in de sectie met [zoekparameters](#search-parameters) van dit document. |
| `namespace` | Identificeert de daadwerkelijke gegevens om op de schemaklasse te zoeken die in de `schema.name` parameter wordt gespecificeerd. |
| `organization.type` | Hiermee bepaalt u de inhoud van de reactie. De indeling van de geretourneerde inhoud is afhankelijk van de waarden die worden gebruikt in `schema.name`. De geldige waarden zijn `_xdm.context.segmentdefinition`bijvoorbeeld `hierarchy` of `hierarchyinfo`. |
| `organization.id` | **Vereist als`organization.type`is opgegeven.** Geeft de hiërarchie van de opgegeven organisatie wanneer deze wordt gebruikt met `organization.type` de hiërarchie. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een array met objecten die voldoen aan uw zoekcriteria. In dit voorbeeld wordt een lijst met segmentdefinities geretourneerd omdat de `schema.name` parameter `_xdm.context.segmentdefinition`is.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### Leveringsverzoeken maken

U kunt leveringsverzoeken tot stand brengen om het onderzoek van het Profiel op schema&#39;s toe te laten door een POST- verzoek aan het `/search/provisioning/component/init` eindpunt te maken.

**Verzoek**

>[!CAUTION]
>Dit POST-verzoek bevat geen payload en vereist daarom geen Content-Type-header. Bovendien is er geen Sandbox-header omdat alle gegevens naar een algemene sandbox worden verzonden.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 201 (Gemaakt) en het volgende bericht:

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### Configuratieverzoeken verwerken

Het configuratieeindpunt kan aan opstelling worden gebruikt de juiste indexen, indexeerders, en gegevensbronverbindingen voor een nieuwe IMS Organisatie. Twee eigenschappen worden vereist om configuratieverzoeken te behandelen: `databaseName` en `containerName`.

`databaseName` vertegenwoordigt de naam van het gegevensbestand van het Profiel voor de organisatie die zal worden gevormd.

`containerName` vertegenwoordigt de naam van de container die door een gegevensschakelaar wordt bevolkt, die is wat tijdens configuratie wordt gelezen. Er zijn twee waarden voor `containerName`, één of beide kunnen in het POST-verzoek worden gebruikt:
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### Een configuratieverzoek maken

Met de volgende API-aanroep worden de vereiste gegevensbron, index en index gegenereerd op basis van de parameters die in de payload van de aanvraag worden opgegeven.

**API-indeling**

```http
POST /search/configure
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) en een plaintext-bericht.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### Een configuratieverzoek verwijderen

Met de volgende API-aanroep worden overeenkomende indexitems verwijderd en worden de indexen en de gegevensbron verwijderd op basis van de parameters die in de aanvraaglading zijn opgegeven.

>[!NOTE]
>De index zelf wordt niet verwijderd, omdat het een gedeelde bron is.

**API-indeling**

```http
DELETE /search/configure
```

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 202 (geaccepteerd) en een plaintext-bericht.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## Volgende stappen

Na het lezen van deze gids hebt u nu een beter inzicht in hoe het zoeken van het Profiel van de Klant in real time werkt. Lees het overzicht [van het profiel van de](../home.md)real-time klant voor meer informatie over het profielvan de real-time klant. Lees het [segmentatieoverzicht](../../segmentation/home.md)voor meer informatie over segmentatie.

## Aanhangsel {#appendix}

### Zoekparameters {#search-parameters}

In de volgende tabel worden de details weergegeven van de werking van de zoekparameter wanneer de zoek-API wordt gebruikt.

| Zoekopdracht | Beschrijving |
|------------ | -----------|
| foo | Zoeken naar een willekeurig woord. Dit resulteert in resultaten als het woord &quot;foo&quot; wordt gevonden in een van de doorzoekbare velden. |
| foo AND bar | Een Booleaanse zoekopdracht. Dit resulteert in resultaten als **zowel** de woorden &quot;foo&quot; als &quot;bar&quot; in een van de doorzoekbare velden worden gevonden. |
| foo OR bar | Een Booleaanse zoekopdracht. Dit resulteert in resultaten als **** of het woord &quot;foo&quot; of het woord &quot;bar&quot; in om het even welke doorzoekbare gebieden worden gevonden. |
| foo NOT bar | Een Booleaanse zoekopdracht. Dit resulteert in resultaten als het woord &quot;foo&quot; wordt gevonden maar het woord &quot;bar&quot; in geen van de doorzoekbare velden wordt gevonden. |
| naam: foo AND bar | Een Booleaanse zoekopdracht. Dit resulteert in resultaten als **zowel** de woorden &quot;foo&quot; als &quot;bar&quot; in het veld &quot;name&quot; worden gevonden. |
| run* | Een zoekopdracht met jokertekens. Als u een sterretje (*) gebruikt, komt dit overeen met 0 of meer tekens. Dit betekent dat het resultaat wordt geretourneerd als de inhoud van een doorzoekbaar veld een woord bevat dat begint met &#39;run&#39;. Dit resulteert bijvoorbeeld in resultaten als de woorden &quot;run&quot;, &quot;run&quot;, &quot;runner&quot; of &quot;runt&quot; worden weergegeven. |
| cam? | Een zoekopdracht met jokertekens. Een vraagteken (?) gebruiken komt overeen met slechts één teken. Dit betekent dat de resultaten worden geretourneerd als de inhoud van een doorzoekbaar veld begint met &#39;cam&#39; en een extra letter. Dit resulteert bijvoorbeeld in resultaten als de woorden &quot;kamp&quot; of &quot;cams&quot; worden weergegeven, maar retourneert geen resultaten als de woorden &quot;camera&quot; of &quot;campfire&quot; worden weergegeven. |
| &quot;blue umbrella&quot; | Een woordzoekopdracht. Dit levert resultaten op als de inhoud van een doorzoekbaar veld de volledige uitdrukking &quot;blauwe paraplu&quot; bevat. |
| blauw\~ | Een vage zoekopdracht. U kunt desgewenst een getal tussen 0 en 2 achter de tilde (~) plaatsen om de bewerkingsafstand op te geven. &quot;blue\~1&quot; wordt bijvoorbeeld &quot;blauw&quot;, &quot;blauw&quot; of &quot;lijm&quot; geretourneerd. Vage zoekopdrachten kunnen **alleen** op termen worden toegepast, niet op woordgroepen. U kunt echter wel tildes toevoegen aan het einde van elk woord in een woordgroep. Dus &#39;camping\~ in\~ the\~ zomer\~&#39; komt overeen met &#39;kamping in de zomer&#39;. |
| &quot;hotel Airport&quot;\~5 | Een nabijheidszoekopdracht. Dit type zoekopdracht wordt gebruikt om termen te zoeken die in een document dicht bij elkaar liggen. De woorden &quot;hotel&quot; en &quot;luchthaven&quot; `"hotel airport"~5` zullen bijvoorbeeld binnen vijf woorden in een document voorkomen. |
| `/a[0-9]+b$/` | Een zoekopdracht met een reguliere expressie. Dit type van onderzoek vindt een gelijke die op de inhoud tussen voorwaartse schuine strepen &quot;/&quot;wordt gebaseerd, zoals die in de klasse RegExp wordt gedocumenteerd. Als u bijvoorbeeld documenten wilt zoeken die &#39;motel&#39; of &#39;hotel&#39; bevatten, geeft u op `/[mh]otel/`. Zoekopdrachten met reguliere expressies worden vergeleken met afzonderlijke woorden. |

Voor meer gedetailleerde documentatie over de vraagsyntaxis, te lezen gelieve de documentatie [van de de vraagsyntaxis van](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene.
