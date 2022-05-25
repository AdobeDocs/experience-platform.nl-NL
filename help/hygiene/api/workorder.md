---
title: Eindpunt van API voor werkorder
description: Het /workorder eindpunt in de Hygiene API van Gegevens staat u toe om schrappingstaken voor consumentenidentiteiten programmatically te beheren.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Werkordereindpunt

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die Adobe Shield voor gezondheidszorg hebben aangeschaft.

De `/workorder` Het eindpunt in de Hygiene API van Gegevens staat u toe om schrappingstaken voor consumentenidentiteiten in Adobe Experience Platform programmatically te beheren.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Controleer voordat je doorgaat de [overzicht](./overview.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Identiteiten verwijderen {#delete-identities}

U kunt één of meerdere consumentenidentiteiten van één enkele dataset of alle datasets schrappen door een verzoek van de POST aan de `/workorder` eindpunt.

**API-indeling**

```http
POST /workorder
```

**Verzoek**

Afhankelijk van de waarde van de `datasetId` verstrekt in de verzoeklading, zal de API vraag consumentenidentiteiten van alle datasets of één enkele dataset schrappen die u specificeert. Het volgende verzoek schrapt drie consumentenidentiteiten van een specifieke dataset.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `action` | De uit te voeren actie. De waarde moet worden ingesteld op `delete_identity` wanneer u identiteiten verwijdert. |
| `datasetId` | Als u uit één enkele dataset schrapt, moet deze waarde identiteitskaart van de dataset in kwestie zijn. Als u uit alle datasets schrapt, plaats de waarde aan `ALL`.<br><br>Als u één enkele dataset specificeert, moet het bijbehorende schema van de Gegevens van de Ervaring van de dataset van het Model (XDM) een primaire bepaalde identiteit hebben. |
| `identities` | Een array met de identiteiten van ten minste één gebruiker van wie u de gegevens wilt verwijderen. Elke identiteit bestaat uit een [naamruimte identity](../../identity-service/namespaces.md) en een waarde:<ul><li>`namespace`: Bevat één tekenreekseigenschap, `code`, die staat voor de naamruimte identity. </li><li>`id`: De identiteitswaarde.</ul>Indien `datasetId` geeft één gegevensset aan, elke entiteit onder `identities` moet dezelfde naamruimte gebruiken als de primaire identiteit van het schema.<br><br>Indien `datasetId` is ingesteld op `ALL`de `identities` array is niet beperkt tot één naamruimte omdat elke dataset anders kan zijn. Uw verzoeken blijven echter beperkt tot de naamruimten die beschikbaar zijn voor uw organisatie, zoals gerapporteerd door [Identiteitsservice](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert de details van de identiteitsschrapping terug.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de verwijderingsvolgorde. Dit kan worden gebruikt om de status van de schrapping later omhoog te kijken. |
| `orgId` | De id van uw organisatie. |
| `batchId` | De id van de batch waaraan deze verwijderingsvolgorde is gekoppeld, wordt gebruikt voor foutopsporingsdoeleinden. De veelvoudige schrappingsorden worden gebundeld in een partij die door stroomafwaartse diensten moet worden verwerkt. |
| `bundleOrdinal` | De volgorde waarin deze verwijderingsopdracht werd ontvangen toen deze in een batch voor downstreamverwerking werd gebundeld. Wordt gebruikt voor foutopsporingsdoeleinden. |
| `payloadByteSize` | De grootte, in bytes, van de lijst van identiteiten die in de verzoeklading werden verstrekt die tot deze schrappingsorde leidde. |
| `operationCount` | Het aantal identiteiten waarop deze schrappingsorde van toepassing is. |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `responseMessage` | De meest recente reactie die door het systeem is geretourneerd. Als er tijdens de verwerking een fout optreedt, is deze waarde een JSON-tekenreeks met gedetailleerde foutinformatie om u te helpen begrijpen wat er mogelijk fout is gegaan. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |

{style=&quot;table-layout:auto&quot;}

## De status van alle verwijderingen van identiteiten weergeven {#list}

U kunt de status van alle verwijderingen van identiteiten weergeven door een GET-aanvraag in te dienen.

**API-indeling**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMS}` | Een lijst van facultatieve vraagparameters voor de lijstvraag, met veelvoudige parameters die door worden gescheiden `&` tekens. Accepteerde vraagparams zijn als volgt:<ul><li>`data` - Een Booleaanse waarde die, wanneer ingesteld op `true`bevat alle aanvullende verzoek- en reactiegegevens die voor de verwijderingsvolgorde zijn ontvangen. Standaardwaarden: `false`.</li><li>`start` - Een tijdstempel voor het begin van de tijdlijn om te zoeken naar verwijderingsopdrachten.</li><li>`end` - Een tijdstempel voor het einde van de tijdlijn om te zoeken naar verwijderingsopdrachten.</li><li>`page` - De specifieke reactiepagina die moet worden geretourneerd.</li><li>`limit` - Het aantal records dat per pagina moet worden weergegeven.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de details van alle verwijderingsbewerkingen, inclusief de huidige status. De voorbeeldreactie hieronder is afgebroken voor de ruimte.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `results` | Bevat de lijst met verwijderingsopdrachten en de bijbehorende details. Voor meer informatie over de eigenschappen van een schrappingsorde, zie de voorbeeldreactie in de sectie over [zoeken naar een verwijderingsvolgorde](#lookup). |
| `total` | Het totale aantal verwijderde orders dat is gevonden op basis van de huidige filters. |
| `count` | Het totale aantal verwijderde orders dat op elke pagina van de reactie wordt gevonden. |
| `_links` | Bevat pagineringsinformatie om u te helpen de rest reactie onderzoeken:<ul><li>`next`: Bevat een URL voor de volgende pagina in de reactie.</li><li>`page`: Bevat een URL-sjabloon voor toegang tot een andere pagina in het antwoord of voor aanpassing van het aantal items dat op elke pagina wordt geretourneerd.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Haal de status van een identiteitsschrapping (#lookup) op

Nadat u een aanvraag hebt verzonden naar [een identiteit verwijderen](#delete-identities), kunt u de status controleren met een GET-aanvraag.

**API-indeling**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{WORK_ORDER_ID}` | De `workorderId` van de identiteitsschrapping u kijkt. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de verwijderingsbewerking, inclusief de huidige status.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de verwijderingsvolgorde. Dit kan worden gebruikt om de status van de schrapping later omhoog te kijken. |
| `orgId` | De id van uw organisatie. |
| `batchId` | De id van de batch waaraan deze verwijderingsvolgorde is gekoppeld, wordt gebruikt voor foutopsporingsdoeleinden. De veelvoudige schrappingsorden worden gebundeld in een partij die door stroomafwaartse diensten moet worden verwerkt. |
| `bundleOrdinal` | De volgorde waarin deze verwijderingsopdracht werd ontvangen toen deze in een batch voor downstreamverwerking werd gebundeld. Wordt gebruikt voor foutopsporingsdoeleinden. |
| `payloadByteSize` | De grootte, in bytes, van de lijst van identiteiten die in de verzoeklading werden verstrekt die tot deze schrappingsorde leidde. |
| `operationCount` | Het aantal identiteiten waarop deze schrappingsorde van toepassing is. |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `responseMessage` | De meest recente reactie die door het systeem is geretourneerd. Als er tijdens de verwerking een fout optreedt, is deze waarde een JSON-tekenreeks met gedetailleerde foutinformatie om u te helpen begrijpen wat er mogelijk fout is gegaan. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |
