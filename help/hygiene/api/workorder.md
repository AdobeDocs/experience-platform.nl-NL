---
title: Eindpunt van API voor werkorder
description: Het /workorder eindpunt in de Hygiene API van Gegevens staat u toe om schrappingstaken voor identiteiten programmatically te beheren.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: da8b5d9fffdf8a176a4d70be5df5b3021cf0df7b
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 0%

---

# Werkordereindpunt

De `/workorder` Het eindpunt in de Hygiene API van Gegevens staat u toe om verslagen te beheren schrapt verzoeken in Adobe Experience Platform.

>[!IMPORTANT]
>
>Aanvragen voor het verwijderen van records zijn alleen beschikbaar voor organisaties die deze hebben aangeschaft **Adobe Healthcare Shield**.
>
>
>Gegevens verwijderen uit records moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Ze zijn **niet** te gebruiken voor verzoeken om rechten van betrokkenen (naleving) met betrekking tot privacyvoorschriften zoals de algemene gegevensbeschermingsverordening (GDPR). Gebruik voor alle gevallen waarin aan de eisen wordt voldaan [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) in plaats daarvan.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Controleer voordat je doorgaat de [overzicht](./overview.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Een verzoek tot verwijdering van records maken {#create}

U kunt één of meerdere identiteiten van één enkele dataset of alle datasets schrappen door een verzoek van de POST aan het `/workorder` eindpunt.

**API-indeling**

```http
POST /workorder
```

**Verzoek**

Afhankelijk van de waarde van de `datasetId` verstrekt in de verzoeklading, zal de API vraag identiteiten van alle datasets of één enkele dataset schrappen die u specificeert. Het volgende verzoek schrapt drie identiteiten van een specifieke dataset.

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
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
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
| `action` | De uit te voeren actie. De waarde moet worden ingesteld op `delete_identity` voor verwijderen van records. |
| `datasetId` | Als u uit één enkele dataset schrapt, moet deze waarde identiteitskaart van de dataset in kwestie zijn. Als u uit alle datasets schrapt, plaats de waarde aan `ALL`.<br><br>Als u één enkele dataset specificeert, moet het bijbehorende schema van de Gegevens van de Ervaring van de dataset van het Model (XDM) een primaire bepaalde identiteit hebben. |
| `displayName` | De weergavenaam voor het verzoek om het verwijderen van records. |
| `description` | Een beschrijving voor het verzoek om record te verwijderen. |
| `identities` | Een array met de identiteiten van ten minste één gebruiker van wie u de gegevens wilt verwijderen. Elke identiteit bestaat uit een [naamruimte identity](../../identity-service/namespaces.md) en een waarde:<ul><li>`namespace`: Bevat één tekenreekseigenschap, `code`, die staat voor de naamruimte identity. </li><li>`id`: De identiteitswaarde.</ul>Indien `datasetId` geeft één gegevensset aan, elke entiteit onder `identities` moet dezelfde naamruimte gebruiken als de primaire identiteit van het schema.<br><br>Indien `datasetId` is ingesteld op `ALL`de `identities` array is niet beperkt tot één naamruimte omdat elke dataset anders kan zijn. Uw verzoeken blijven echter beperkt tot de naamruimten die beschikbaar zijn voor uw organisatie, zoals gerapporteerd door [Identiteitsservice](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Als de reactie succesvol was, worden de details van de record delete geretourneerd.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de verwijderingsvolgorde. Dit kan worden gebruikt om de status van de schrapping later omhoog te kijken. |
| `orgId` | Uw organisatie-id. |
| `bundleId` | De id van de bundel waaraan deze verwijderingsvolgorde is gekoppeld, wordt gebruikt voor foutopsporingsdoeleinden. Meerdere verwijderingsopdrachten worden gebundeld om door downstreamdiensten te worden verwerkt. |
| `action` | De actie die door de het werkorde wordt uitgevoerd. Voor record-verwijderingen is de waarde `identity-delete`. |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `updatedAt` | Een tijdstempel van wanneer de verwijderingsvolgorde voor het laatst is bijgewerkt. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |
| `datasetId` | De id van de gegevensset waarop het verzoek betrekking heeft. Als het verzoek voor alle datasets is, zal de waarde worden geplaatst aan `ALL`. |

{style=&quot;table-layout:auto&quot;}

## De status van een record verwijderen (#lookup)

Na [een verzoek tot verwijdering van records maken](#create), kunt u de status controleren met een GET-aanvraag.

**API-indeling**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{WORK_ORDER_ID}` | De `workorderId` van de record verwijderen die u opzoekt. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de verwijderingsbewerking, inclusief de huidige status.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de verwijderingsvolgorde. Dit kan worden gebruikt om de status van de schrapping later omhoog te kijken. |
| `orgId` | Uw organisatie-id. |
| `bundleId` | De id van de bundel waaraan deze verwijderingsvolgorde is gekoppeld, wordt gebruikt voor foutopsporingsdoeleinden. Meerdere verwijderingsopdrachten worden gebundeld om door downstreamdiensten te worden verwerkt. |
| `action` | De actie die door de het werkorde wordt uitgevoerd. Voor record-verwijderingen is de waarde `identity-delete`. |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `updatedAt` | Een tijdstempel van wanneer de verwijderingsvolgorde voor het laatst is bijgewerkt. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |
| `datasetId` | De id van de gegevensset waarop het verzoek betrekking heeft. Als het verzoek voor alle datasets is, zal de waarde worden geplaatst aan `ALL`. |
| `productStatusDetails` | Een array die de huidige status van downstreamprocessen met betrekking tot de aanvraag opsomt. Elk matrixobject bevat de volgende eigenschappen:<ul><li>`productName`: De naam van de downstreamservice.</li><li>`productStatus`: De huidige verwerkingsstatus van het verzoek van de downstreamdienst.</li><li>`createdAt`: Een tijdstempel van wanneer de meest recente status door de service is gepost.</li></ul> |

## Een verzoek tot het verwijderen van records bijwerken

U kunt de `displayName` en `description` voor een record verwijderen door een PUT aan te vragen.

**API-indeling**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{WORK_ORDER_ID}` | De `workorderId` van de record verwijderen die u opzoekt. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `displayName` | Een bijgewerkte weergavenaam voor het verzoek om het verwijderen van records. |
| `description` | Een bijgewerkte beschrijving voor de aanvraag om het record te verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Als de reactie succesvol was, worden de details van de record delete geretourneerd.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName" : "Update - displayName",
  "description" : "Update - description",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de verwijderingsvolgorde. Dit kan worden gebruikt om de status van de schrapping later omhoog te kijken. |
| `orgId` | Uw organisatie-id. |
| `bundleId` | De id van de bundel waaraan deze verwijderingsvolgorde is gekoppeld, wordt gebruikt voor foutopsporingsdoeleinden. Meerdere verwijderingsopdrachten worden gebundeld om door downstreamdiensten te worden verwerkt. |
| `action` | De actie die door de het werkorde wordt uitgevoerd. Voor record-verwijderingen is de waarde `identity-delete`. |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `updatedAt` | Een tijdstempel van wanneer de verwijderingsvolgorde voor het laatst is bijgewerkt. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |
| `datasetId` | De id van de gegevensset waarop het verzoek betrekking heeft. Als het verzoek voor alle datasets is, zal de waarde worden geplaatst aan `ALL`. |
| `productStatusDetails` | Een array die de huidige status van downstreamprocessen met betrekking tot de aanvraag opsomt. Elk matrixobject bevat de volgende eigenschappen:<ul><li>`productName`: De naam van de downstreamservice.</li><li>`productStatus`: De huidige verwerkingsstatus van het verzoek van de downstreamdienst.</li><li>`createdAt`: Een tijdstempel van wanneer de meest recente status door de service is gepost.</li></ul> |

{style=&quot;table-layout:auto&quot;}
