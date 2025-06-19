---
title: Verzoeken om verwijdering opnemen (werkordereindpunt)
description: Het /workorder eindpunt in de Hygiene API van Gegevens staat u toe om schrappingstaken voor identiteiten programmatically te beheren.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 1%

---

# Verzoeken om gegevens te verwijderen (eindpunt van werkorder) {#work-order-endpoint}

Met het `/workorder` -eindpunt in de Data Hygiene API kunt u aanvragen voor het verwijderen van records in Adobe Experience Platform programmatisch beheren.

>[!IMPORTANT]
> 
>Gegevens verwijderen uit records moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Zij zijn **niet** om voor de verzoeken van de rechten van gegevenssubject (naleving) zoals met betrekking tot privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) te worden gebruikt. Voor alle gevallen van het nalevingsgebruik, gebruik [ Adobe Experience Platform Privacy Service ](../../privacy-service/home.md) in plaats daarvan.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Alvorens verder te gaan, te herzien gelieve het [ overzicht ](./overview.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API met succes te maken.

## Quoten en verwerkingstijdlijnen {#quotas}

Aanvragen voor het verwijderen van records zijn onderworpen aan dagelijkse en maandelijkse indieningslimieten voor id&#39;s, die worden bepaald door de licentierechten van uw organisatie. Deze limieten gelden voor verwijderingsaanvragen voor zowel de gebruikersinterface als de API.

>[!NOTE]
>
>U kunt tot **1.000.000 herkenningstekens per dag** voorleggen, maar slechts als uw resterende maandquotum het toestaat. Als uw maandelijks maximum minder dan 1 miljoen bedraagt, kan uw dagelijkse inzending die limiet niet overschrijden.

### Maandelijkse indieningstoeslagrechten per product {#quota-limits}

In de onderstaande tabel worden de indieningslimieten voor id&#39;s per product en machtigingsniveau weergegeven. Voor elk product is de maandelijkse limiet de laagste van twee waarden: een vast identificatieplafond of een op percentage gebaseerde drempel die is gekoppeld aan uw gelicentieerde gegevensvolume.

| Product | Beschrijving van rechten | Maandelijkse limiet (Welke lager is) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP of Adobe Journey Optimizer | Zonder &#39;Privacy and Security Shield&#39; of &#39;Healthcare Shield Add-on&#39; | 2.000.000 ID&#39;s of 5% van het adresseerbare publiek |
| Real-Time CDP of Adobe Journey Optimizer | Met privacy- en beveiligingsschild of de invoegtoepassing Gezondheidsschild | 15.000.000 id&#39;s of 10% van het adresseerbare publiek |
| Customer Journey Analytics | Zonder &#39;Privacy and Security Shield&#39; of &#39;Healthcare Shield Add-on&#39; | 2.000.000 ID&#39;s of 100 ID&#39;s per miljoen CJA rijen met rechten |
| Customer Journey Analytics | Met privacy- en beveiligingsschild of de invoegtoepassing Gezondheidsschild | 15.000.000 ID&#39;s of 200 ID&#39;s per miljoen CJA rijen met rechten |

>[!NOTE]
>
> De meeste organisaties zullen lagere maandelijkse grenzen hebben die op hun werkelijk adresseerbare publiek of de rijaanspraken van CJA worden gebaseerd.

De quota zijn opnieuw ingesteld op de eerste dag van elke kalendermaand. Ongebruikte quota **niet** draagt over.

>[!NOTE]
>
>De quota&#39;s zijn gebaseerd op de vergunning gegeven maandelijkse bevoegdheid van uw organisatie voor **voorgelegde herkenningstekens**. Deze worden niet afgedwongen door systeemtrails, maar kunnen worden gecontroleerd en herzien.
>
>De Schrapping van het verslag is a **gedeelde dienst**. Uw maandelijkse limiet weerspiegelt de hoogste rechten voor Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics en alle toepasselijke add-ons voor schild.

### Tijdlijnen verwerken voor id-verzending {#sla-processing-timelines}

Na verzending worden aanvragen voor het verwijderen van records in de wachtrij geplaatst en verwerkt op basis van uw machtigingsniveau.

| Beschrijving van product en rechten | Duur wachtrij | Maximale verwerkingstijd (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Zonder &#39;Privacy and Security Shield&#39; of &#39;Healthcare Shield Add-on&#39; | Tot 15 dagen | 30 dagen |
| Met privacy- en beveiligingsschild of de invoegtoepassing Gezondheidsschild | Doorgaans 24 uur | 15 dagen |

Als uw organisatie hogere limieten nodig heeft, neemt u contact op met uw Adobe-vertegenwoordiger voor een beoordeling van uw rechten.

>[!TIP]
>
>Om uw huidige quotagebruik of machtigingsrij te controleren, zie de [ gids van de de verwijzingsverwijzing van de Quota ](../api/quota.md).

## Een verzoek tot het verwijderen van records maken {#create}

U kunt één of meerdere identiteiten van één enkele dataset of alle datasets schrappen door een POST- verzoek aan het `/workorder` eindpunt te doen.

>[!TIP]
>
>Elk verslag schrapt verzoek dat door API wordt voorgelegd kan tot **100.000 identiteiten** omvatten. Om de efficiëntie te maximaliseren, dient u zoveel mogelijk identiteiten per aanvraag in en vermijdt u kleine verzendingen, zoals werkorders met één id.

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

Nadat u [ een verslag creeert schrapt verzoek ](#create), kunt u zijn status controleren gebruikend een verzoek van GET.

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

U kunt de `displayName` en `description` voor een record verwijderen door een PUT-aanvraag in te dienen.

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
