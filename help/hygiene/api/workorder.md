---
title: Eindpunt van API voor werkvolgorde
description: Het /workorder eindpunt in de Hygiene API van Gegevens staat u toe om schrappingstaken voor identiteiten programmatically te beheren.
badgeBeta: label="Beta" type="Informative"
role: Developer
badge: Beta
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: bf819d506b0ee6f3aba6850f598ee46f16695dfa
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Werkordereindpunt {#work-order-endpoint}

Met het `/workorder` -eindpunt in de Data Hygiene API kunt u aanvragen voor het verwijderen van records in Adobe Experience Platform programmatisch beheren.

>[!IMPORTANT]
> 
>De eigenschap van de Schrapping van het Verslag is momenteel in Beta en beschikbaar slechts in a **beperkte versie**. Het is niet beschikbaar voor alle klanten. Registratie-verwijderingsverzoeken zijn alleen beschikbaar voor organisaties in de beperkte release.
>
>Gegevens verwijderen uit records moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Zij zijn **niet** om voor de verzoeken van de rechten van gegevenssubject (naleving) zoals met betrekking tot privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) te worden gebruikt. Voor alle gevallen van het nalevingsgebruik, gebruik [ Adobe Experience Platform Privacy Service ](../../privacy-service/home.md) in plaats daarvan.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Alvorens verder te gaan, te herzien gelieve het [ overzicht ](./overview.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een verzoek tot het verwijderen van records maken {#create}

U kunt één of meerdere identiteiten van één enkele dataset of alle datasets schrappen door een verzoek van de POST aan het `/workorder` eindpunt te doen.

>[!IMPORTANT]
> 
>Er zijn verschillende limieten voor het totale aantal unieke identiteitsrecords dat elke maand kan worden verzonden. Deze limieten zijn gebaseerd op uw licentieovereenkomst. Organisaties die alle edities van Adobe Real-time Customer Data Platform en Adobe Journey Optimizer hebben aangeschaft, kunnen maximaal 100.000 identiteitsgegevens verzenden en elke maand verwijderen. De organisaties die **het Schild van de Gezondheidszorg van de Adobe** of **de Privacy en het Schild van de Adobe** hebben gekocht kunnen tot 600.000 identiteitsverslag voorleggen schrapt elke maand.<br> Één enkel [ verslag schrapt verzoek door UI ](../ui/record-delete.md) staat u toe om 10.000 IDs in één keer voor te leggen. Met de API-methode voor het verwijderen van records kunnen 100.000 id&#39;s tegelijk worden verzonden.<br> het is beste praktijken om zoveel mogelijk IDs per verzoek, tot uw grens van identiteitskaart voor te leggen. Wanneer u een hoog volume id&#39;s wilt verwijderen, moet u een laag volume of één id per record verwijderen.

**API formaat**

```http
POST /workorder
```

>[!NOTE]
>
>De verzoeken van de Levenscyclus van gegevens kunnen datasets slechts wijzigen die op primaire identiteiten of een identiteitskaart worden gebaseerd. Een verzoek moet of de primaire identiteit specificeren, of een identiteitskaart verstrekken.

**Verzoek**

Afhankelijk van de waarde van `datasetId` die in de aanvraaglading wordt verstrekt, zal de API vraag identiteiten van alle datasets of één enkele dataset schrappen die u specificeert. Het volgende verzoek schrapt drie identiteiten van een specifieke dataset.

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
| `action` | De uit te voeren actie. De waarde moet op `delete_identity` worden ingesteld om record te verwijderen. |
| `datasetId` | Als u uit één enkele dataset schrapt, moet deze waarde identiteitskaart van de dataset in kwestie zijn. Als u uit alle datasets schrapt, plaats de waarde aan `ALL`.<br><br> als u één enkele dataset specificeert, moet het bijbehorende Model van de Gegevens van de Ervaring van de dataset (XDM) schema een primaire bepaalde identiteit hebben. Als de dataset geen primaire identiteit heeft, dan moet het een identiteitskaart hebben om door een verzoek van de Levenscyclus van Gegevens te worden gewijzigd.<br> als een identiteitskaart bestaat, zal het als top-level gebied genoemd `identityMap` aanwezig zijn.<br> Merk op dat een datasetrij vele identiteiten in zijn identiteitskaart kan hebben, maar slechts één kan als primair worden gemerkt. `"primary": true` moet worden opgenomen om ervoor te zorgen dat de `id` overeenkomt met een primaire identiteit. |
| `displayName` | De weergavenaam voor het verzoek om het verwijderen van records. |
| `description` | Een beschrijving voor het verzoek om record te verwijderen. |
| `identities` | Een array met de identiteiten van ten minste één gebruiker van wie u de gegevens wilt verwijderen. Elke identiteit wordt samengesteld van een [ identiteit namespace ](../../identity-service/features/namespaces.md) en een waarde:<ul><li>`namespace`: bevat één tekenreekseigenschap, `code` , die de naamruimte van de identiteit vertegenwoordigt. </li><li>`id`: De identiteitswaarde.</ul>Als `datasetId` één gegevensset opgeeft, moet elke entiteit onder `identities` dezelfde naamruimte gebruiken als de primaire identiteit van het schema.<br><br> Als `datasetId` wordt geplaatst aan `ALL`, wordt de `identities` serie beperkt niet tot enige enige namespace aangezien elke dataset verschillend zou kunnen zijn. Nochtans, worden uw verzoeken nog beperkt namespaces beschikbaar aan uw organisatie, zoals die door [ wordt gemeld de Dienst van de Identiteit ](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Reactie**

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
| `action` | De actie die door de het werkorde wordt uitgevoerd. Voor het verwijderen van records is de waarde `identity-delete` . |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `updatedAt` | Een tijdstempel van wanneer de verwijderingsvolgorde voor het laatst is bijgewerkt. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |
| `datasetId` | De id van de gegevensset waarop het verzoek betrekking heeft. Als het verzoek voor alle datasets is, zal de waarde aan `ALL` worden geplaatst. |

{style="table-layout:auto"}

## De status van een record verwijderen {#lookup}

Nadat u [ een verslag creeert schrapt verzoek ](#create), kunt u zijn status controleren gebruikend een verzoek van de GET.

**API formaat**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{WORK_ORDER_ID}` | De `workorderId` van de record die u opzoekt. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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
| `action` | De actie die door de het werkorde wordt uitgevoerd. Voor het verwijderen van records is de waarde `identity-delete` . |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `updatedAt` | Een tijdstempel van wanneer de verwijderingsvolgorde voor het laatst is bijgewerkt. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |
| `datasetId` | De id van de gegevensset waarop het verzoek betrekking heeft. Als het verzoek voor alle datasets is, zal de waarde aan `ALL` worden geplaatst. |
| `productStatusDetails` | Een array die de huidige status van downstreamprocessen met betrekking tot de aanvraag opsomt. Elk matrixobject bevat de volgende eigenschappen:<ul><li>`productName`: De naam van de downstreamservice.</li><li>`productStatus`: De huidige verwerkingsstatus van het verzoek van de downstreamservice.</li><li>`createdAt`: Een tijdstempel met het tijdstip waarop de meest recente status door de service is gepost.</li></ul> |

## Een verzoek tot het verwijderen van records bijwerken

U kunt de `displayName` en `description` voor een record verwijderen door een PUT aan te vragen.

**API formaat**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{WORK_ORDER_ID}` | De `workorderId` van de record die u opzoekt. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X PUT \
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

{style="table-layout:auto"}

**Reactie**

Als de reactie succesvol was, worden de details van de record delete geretourneerd.

```json
{
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de verwijderingsvolgorde. Dit kan worden gebruikt om de status van de schrapping later omhoog te kijken. |
| `orgId` | Uw organisatie-id. |
| `bundleId` | De id van de bundel waaraan deze verwijderingsvolgorde is gekoppeld, wordt gebruikt voor foutopsporingsdoeleinden. Meerdere verwijderingsopdrachten worden gebundeld om door downstreamdiensten te worden verwerkt. |
| `action` | De actie die door de het werkorde wordt uitgevoerd. Voor het verwijderen van records is de waarde `identity-delete` . |
| `createdAt` | Een tijdstempel met het tijdstip waarop de verwijderingsvolgorde is gemaakt. |
| `updatedAt` | Een tijdstempel van wanneer de verwijderingsvolgorde voor het laatst is bijgewerkt. |
| `status` | De huidige status van de verwijderingsopdracht. |
| `createdBy` | De gebruiker die de schrappingsorde creeerde. |
| `datasetId` | De id van de gegevensset waarop het verzoek betrekking heeft. Als het verzoek voor alle datasets is, zal de waarde aan `ALL` worden geplaatst. |
| `productStatusDetails` | Een array die de huidige status van downstreamprocessen met betrekking tot de aanvraag opsomt. Elk matrixobject bevat de volgende eigenschappen:<ul><li>`productName`: De naam van de downstreamservice.</li><li>`productStatus`: De huidige verwerkingsstatus van het verzoek van de downstreamservice.</li><li>`createdAt`: Een tijdstempel met het tijdstip waarop de meest recente status door de service is gepost.</li></ul> |

{style="table-layout:auto"}
