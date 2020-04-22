---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Gegevensgebruikslabels beheren met API''s '
topic: developer guide
translation-type: tm+mt
source-git-commit: d685f1851badf54ce1d1ac3cbacd69d62894c33f

---


# Gegevensgebruikslabels beheren met API&#39;s

Dit document bevat stappen voor het beheren van labels voor gegevensgebruik op dataset- en veldniveau met behulp van de Catalogusservice-API.

## Aan de slag

Alvorens u deze gids leest, adviseert men dat u het overzicht [van de Dienst van de](../../catalog/home.md) Catalogus voor een robuustere inleiding aan de dienst leest. Daarnaast moet u ook de stappen volgen die worden beschreven in de sectie [](../../catalog/api/getting-started.md) Aan de slag in de handleiding voor ontwikkelaars van catalogi om de vereiste referenties te verzamelen voor het oproepen van de API van Catalog.

Om vraag aan de eindpunten te maken die in de hieronder secties worden geschetst, moet u de unieke `id` waarde voor een specifieke dataset hebben. Als u deze waarde niet hebt, zie de sectie van de ontwikkelaarsgids bij het [vermelden van de voorwerpen](../../catalog/api/list-objects.md) van de Catalogus om identiteitskaarts van uw bestaande datasets te vinden.

## De etiketten van de raadpleging voor een dataset {#lookup}

U kunt de etiketten van het gegevensgebruik opzoeken die op een bestaande dataset zijn toegepast door een GET verzoek te doen.

**API-indeling**

```http
GET /dataSets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvan etiketten u omhoog wilt kijken. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de etiketten van het gegevensgebruik terug die op de dataset zijn toegepast.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die op de dataset zijn toegepast. |
| `optionalLabels` | Een lijst van individuele gebieden binnen de dataset die de etiketten van het gegevensgebruik hebben op hen worden toegepast. |

## Labels toepassen op een gegevensset

U kunt een reeks etiketten voor een dataset tot stand brengen door hen in de nuttige lading van een POST of PLAATS verzoek te verstrekken. Als u een van deze methoden gebruikt, worden bestaande labels overschreven en vervangen door de labels in de payload.

**API-indeling**

```http
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvoor u etiketten creeert. |

**Verzoek**

Het volgende POST- verzoek voegt een reeks etiketten aan de dataset, evenals een specifiek gebied binnen die dataset toe. De velden in de payload zijn gelijk aan de velden die vereist zijn voor een PUT-aanvraag.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `labels` | Een lijst van de etiketten van het gegevensgebruik die u aan de dataset wilt toevoegen. |
| `optionalLabels` | Een lijst van om het even welke individuele gebieden binnen de dataset die u etiketten aan wilt toevoegen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de XDM-kenmerken (Experience Data Model) van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li>id</code>: De URI $id</code> -waarde van het schema dat aan het veld is gekoppeld.</li><li>contentType</code>: Het inhoudstype en het versienummer van het schema. Dit zou de vorm van één van de geldige kopballen <a href="../../xdm/api/look-up-resource.md">van de</a> Acceptie voor een XDM raadplegingsverzoek moeten hebben.</li><li>schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

**Antwoord**

Een succesvolle reactie keert de etiketten terug die aan de dataset zijn toegevoegd.

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## Labels voor een gegevensset verwijderen

U kunt de etiketten schrappen die op een dataset door een verzoek van de SCHRAPPING worden toegepast.

**API-indeling**

```http
DELETE /dataSets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvan etiketten u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde HTTP-status 200 voor reacties (OK) die aangeeft dat de labels zijn verwijderd. U kunt de bestaande etiketten [voor de dataset in een afzonderlijke vraag](#lookup) omhoog kijken om dit te bevestigen.

## Volgende stappen

Nu u de etiketten van het gegevensgebruik op dataset en gebied-niveau hebt toegevoegd, kunt u beginnen om gegevens in het Platform van de Ervaring op te nemen. Voor meer informatie begint u met het lezen van de [gegevensinvoerdocumentatie](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie het overzicht [van beleidsregels voor](../policies/overview.md)gegevensgebruik voor meer informatie.