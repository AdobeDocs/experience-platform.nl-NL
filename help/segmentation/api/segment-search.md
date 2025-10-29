---
title: Eindpunt van API voor segmentzoekopdracht
description: In de API van de Dienst van de Segmentatie van Adobe Experience Platform, wordt het Onderzoek van het Segment gebruikt om gebieden te zoeken die zich over diverse gegevensbronnen bevinden en hen in bijna real time terug te keren. Deze gids verstrekt informatie om u te helpen het Onderzoek van het Segment beter begrijpen en omvat steekproefAPI vraag voor het uitvoeren van basisacties gebruikend API.
role: Developer
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# Zoekeindpunt segment

Het Onderzoek van het segment wordt gebruikt om gebieden te zoeken die zich over diverse gegevensbronnen bevinden en hen in bijna real time terug te keren.

Deze gids verstrekt informatie om u te helpen het Onderzoek van het Segment beter begrijpen en omvat steekproefAPI vraag voor het uitvoeren van basisacties gebruikend API.

## Aan de slag

De eindpunten die in deze handleiding worden gebruikt, maken deel uit van de API van [!DNL Adobe Experience Platform Segmentation Service] . Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van vereiste kopballen en hoe te om voorbeeld API vraag te lezen.

Naast de vereiste kopballen die in de begonnen sectie worden geschetst, vereisen alle verzoeken aan het eindpunt van het Onderzoek van het Segment de volgende extra kopbal:

- x-ups-search-version: &quot;1.0&quot;

### Zoeken in meerdere naamruimten

Dit onderzoekseindpunt kan worden gebruikt om over diverse namespaces te zoeken, die een lijst van de resultaten van het onderzoeksaantal terugkeren. U kunt meerdere parameters gebruiken, gescheiden door ampersands (&amp;).

**API formaat**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| Parameters | Beschrijving |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Vereist)** Where {SCHEMA} vertegenwoordigt de schemaklasse die aan de onderzoeksvoorwerpen wordt geassocieerd. Momenteel wordt alleen `_xdm.context.segmentdefinition` ondersteund. |
| `s={SEARCH_TERM}` | *(Facultatief)* waar {SEARCH_TERM} een vraag vertegenwoordigt die aan de implementatie van Microsoft van [ het onderzoekssyntaxis van Lucene ](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax) in overeenstemming is. Als er geen zoekterm is opgegeven, worden alle records geretourneerd die aan `schema.name` zijn gekoppeld. Een meer gedetailleerde verklaring kan in [ bijlage ](#appendix) van dit document worden gevonden. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Reactie**

Een succesvolle reactie retourneert HTTP status 200 met de volgende informatie.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### Individuele entiteiten zoeken

Dit zoekeindpunt kan worden gebruikt om een lijst van alle volledige tekst geïndexeerde voorwerpen binnen gespecificeerde namespace terug te winnen. U kunt meerdere parameters gebruiken, gescheiden door ampersands (&amp;).

**API formaat**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameters | Beschrijving |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Vereist)** Where {SCHEMA} bevat de schemaklasse die aan de onderzoeksvoorwerpen wordt geassocieerd. Momenteel wordt alleen `_xdm.context.segmentdefinition` ondersteund. |
| `namespace={NAMESPACE}` | **(Vereist)** Where {NAMESPACE} bevat de naamruimte waarin u wilt zoeken. |
| `s={SEARCH_TERM}` | *(Facultatief)* waar {SEARCH_TERM} een vraag bevat die aan de implementatie van Microsoft van [ het onderzoekssyntaxis van Lucene ](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax) in overeenstemming is. Als er geen zoekterm is opgegeven, worden alle records geretourneerd die aan `schema.name` zijn gekoppeld. Een meer gedetailleerde verklaring kan in [ bijlage ](#appendix) van dit document worden gevonden. |
| `entityId={ENTITY_ID}` | *(Facultatief)* beperkt uw onderzoek tot binnen de aangewezen omslag, die met {ENTITY_ID} wordt gespecificeerd. |
| `limit={LIMIT}` | *(Optioneel)* Waar {LIMIT} staat voor het aantal zoekresultaten dat moet worden geretourneerd. De standaardwaarde is 50. |
| `page={PAGE}` | *(Optioneel)* Where {PAGE} staat voor het paginanummer dat wordt gebruikt voor pagineringsresultaten van de doorzochte query. Gelieve te merken op dat het paginaaantal bij **0** begint. |


**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met resultaten die overeenkomen met de zoekquery.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### Structuurgegevens ophalen over een zoekobject

Dit zoekeindpunt kan worden gebruikt om de structurele informatie over het gevraagde onderzoeksvoorwerp te krijgen.

**API formaat**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| Parameters | Beschrijving |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(Vereist)** Where {SCHEMA} bevat de schemaklasse die aan de onderzoeksvoorwerpen wordt geassocieerd. Momenteel wordt alleen `_xdm.context.segmentdefinition` ondersteund. |
| `namespace={NAMESPACE}` | **(Vereist)** Where {NAMESPACE} bevat de naamruimte waarin u wilt zoeken. |
| `entityId={ENTITY_ID}` | **(Vereist)** identiteitskaart van het onderzoeksvoorwerp u de structurele informatie over wilt krijgen, die met {ENTITY_ID} wordt gespecificeerd. |

**Verzoek**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met gedetailleerde structurele informatie over het gevraagde zoekobject.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## Volgende stappen

Na het lezen van deze handleiding hebt u nu een beter inzicht in hoe Segment Search werkt.

## Bijlage {#appendix}

In de volgende secties vindt u aanvullende informatie over de werking van zoektermen. Zoekopdrachten worden als volgt geschreven: `s={FieldName}:{SearchExpression}` . Als u bijvoorbeeld zoekt naar een segmentdefinitie met de naam AAM of [!DNL Platform] , gebruikt u de volgende zoekquery: `s=segmentName:AAM%20OR%20Platform` .

>[!NOTE]
>
>Voor beste praktijken, zou de onderzoeksuitdrukking HTML moeten worden gecodeerd, zoals het hierboven getoonde voorbeeld.

### Zoeken in velden {#search-fields}

De volgende tabel bevat een lijst met velden die kunnen worden doorzocht binnen de zoekqueryparameter.

| Veldnaam | Beschrijving |
| ---------- | ----------- |
| folderId | De map of mappen met de map-id van de opgegeven zoekopdracht. |
| folderLocation | De locatie of locaties met de maplocatie van de opgegeven zoekopdracht. |
| parentFolderId | De segmentdefinitie of map met de bovenliggende map-id van de opgegeven zoekopdracht. |
| segmentId | De segmentdefinitie die overeenkomt met de segment-id van de opgegeven zoekopdracht. |
| segmentName | De segmentdefinitie die overeenkomt met de segmentnaam van de opgegeven zoekopdracht. |
| segmentDescription | De segmentdefinitie die overeenkomt met de segmentbeschrijving van de opgegeven zoekopdracht. |

### Zoekopdracht {#search-expression}

De volgende lijst maakt een lijst een lijst van specifieke van hoe de onderzoeksvragen werken wanneer het gebruiken van het Onderzoek API van het Segment.

>[!NOTE]
>
>De volgende voorbeelden worden voor meer duidelijkheid weergegeven in een indeling die niet door HTML is gecodeerd. HTML codeert uw zoekopdracht voor beste werkwijzen.

| Voorbeeld van zoekopdracht | Beschrijving |
| ------------------------- | ----------- |
| foo | Zoeken naar een willekeurig woord. Dit resulteert in resultaten als het woord &quot;foo&quot; wordt gevonden in een van de doorzoekbare velden. |
| foo AND bar | Een Booleaanse zoekopdracht. Dit zal resultaten terugkeren als **zowel** de woorden &quot;foo&quot;en &quot;bar&quot;in om het even welke doorzoekbare gebieden worden gevonden. |
| foo OR bar | Een Booleaanse zoekopdracht. Dit zal resultaten terugkeren als **of** het woord &quot;foo&quot;of het woord &quot;bar&quot;in om het even welke doorzoekbare gebieden worden gevonden. |
| foo NOT bar | Een Booleaanse zoekopdracht. Dit resulteert in resultaten als het woord &quot;foo&quot; wordt gevonden maar het woord &quot;bar&quot; in geen van de doorzoekbare velden wordt gevonden. |
| naam: foo AND bar | Een Booleaanse zoekopdracht. Dit zal resultaten terugkeren als **zowel** de woorden &quot;foo&quot;en &quot;bar&quot;op het &quot;naam&quot;gebied worden gevonden. |
| run* | Een jokerteken zoeken. Als u een sterretje (*) gebruikt, komt dit overeen met 0 of meer tekens. Dit betekent dat het resultaat wordt geretourneerd als de inhoud van een doorzoekbaar veld een woord bevat dat begint met &#39;run&#39;. Dit resulteert bijvoorbeeld in resultaten als de woorden &quot;run&quot;, &quot;run&quot;, &quot;runner&quot; of &quot;runt&quot; worden weergegeven. |
| cam? | Een jokerteken zoeken. Een vraagteken (?) gebruiken komt overeen met slechts één teken. Dit betekent dat de resultaten worden geretourneerd als de inhoud van een doorzoekbaar veld begint met &#39;cam&#39; en een extra letter. Dit resulteert bijvoorbeeld in resultaten als de woorden &quot;kamp&quot; of &quot;cams&quot; worden weergegeven, maar retourneert geen resultaten als de woorden &quot;camera&quot; of &quot;campfire&quot; worden weergegeven. |
| &quot;blue umbrella&quot; | Een woordzoekopdracht. Dit levert resultaten op als de inhoud van een doorzoekbaar veld de volledige uitdrukking &quot;blauwe paraplu&quot; bevat. |
| blauw\~ | Een vage zoekopdracht. U kunt desgewenst een getal tussen 0 en 2 achter de tilde (~) plaatsen om de bewerkingsafstand op te geven. &quot;blue\~1&quot; zou bijvoorbeeld &quot;blue&quot;, &quot;blues&quot; of &quot;lijm&quot; zijn. Het vage onderzoek kan **slechts** worden toegepast op termijnen, niet uitdrukkingen. U kunt echter wel tildes toevoegen aan het einde van elk woord in een woordgroep. Dus &#39;camping\~ in\~ the\~ zomer\~&#39; komt overeen met &#39;kamping in de zomer&#39;. |
| &quot;hotel Airport&quot;\~5 | Een nabijheidszoekopdracht. Dit type zoekopdracht wordt gebruikt om termen te zoeken die in een document dicht bij elkaar liggen. Met de uitdrukking `"hotel airport"~5` vindt u bijvoorbeeld de termen &quot;hotel&quot; en &quot;luchthaven&quot; binnen 5 woorden van elkaar in een document. |
| `/a[0-9]+b$/` | Een zoekopdracht met een reguliere expressie. Dit type van onderzoek vindt een gelijke die op de inhoud tussen voorwaartse schuine strepen &quot;/&quot;wordt gebaseerd, zoals die in de klasse RegExp wordt gedocumenteerd. Als u bijvoorbeeld documenten met &quot;motel&quot; of &quot;hotel&quot; wilt zoeken, geeft u `/[mh]otel/` op. Zoekopdrachten met reguliere expressies worden vergeleken met afzonderlijke woorden. |

Voor meer gedetailleerde documentatie over de vraagsyntaxis, te lezen gelieve de [ documentatie van de de vraagsyntaxis van Lucene ](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
