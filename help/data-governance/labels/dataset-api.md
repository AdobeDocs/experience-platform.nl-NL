---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Gegevensgebruikslabels voor gegevenssets beheren met behulp van API''s '
topic: developer guide
translation-type: tm+mt
source-git-commit: 2f35765c0dfadbfb4782b6c3904e33ae7a330b2f
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---


# Gegevensgebruikslabels voor gegevenssets beheren met behulp van API&#39;s

Met [!DNL Dataset Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) deze optie kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Het maakt deel uit van de mogelijkheden van de gegevenscatalogus van het Adobe Experience Platform, maar staat los van de [!DNL Catalog Service] API die gegevenssetmetagegevens beheert.

In dit document wordt beschreven hoe u labels voor gegevenssets en velden kunt beheren met de [!DNL Dataset Service API]code. Voor stappen op hoe te om de etiketten van het gegevensgebruik zelf te beheren die API vraag gebruiken, zie de gids [van het](../api/labels.md) etiketteneindpunt voor [!DNL Policy Service API].

## Aan de slag

Voordat u deze handleiding leest, volgt u de stappen in de sectie [Aan de](../../catalog/api/getting-started.md) slag in de handleiding voor ontwikkelaars van catalogi om de vereiste gegevens te verzamelen voor het oproepen van [!DNL Platform] API&#39;s.

Om vraag aan de eindpunten te maken die in dit document worden geschetst, moet u de unieke `id` waarde voor een specifieke dataset hebben. Als u deze waarde niet hebt, raadpleegt u de handleiding bij het [weergeven van catalogusobjecten](../../catalog/api/list-objects.md) om de id&#39;s van uw bestaande gegevenssets te vinden.

## De etiketten van de raadpleging voor een dataset {#look-up}

U kunt de etiketten van het gegevensgebruik opzoeken die op een bestaande dataset zijn toegepast door een verzoek van de GET aan [!DNL Dataset Service] API te richten.

**API-indeling**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvan etiketten u omhoog wilt kijken. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
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

## Labels toepassen op een gegevensset {#apply}

U kunt een reeks etiketten voor een dataset tot stand brengen door hen in de nuttige lading van een POST of een verzoek van de PUT aan [!DNL Dataset Service] API te verstrekken. Als u een van deze methoden gebruikt, worden bestaande labels overschreven en vervangen door de labels in de payload.

**API-indeling**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvoor u etiketten creeert. |

**Verzoek**

Het volgende verzoek van de POST voegt een reeks etiketten aan de dataset, evenals een specifiek gebied binnen die dataset toe. De velden in de payload zijn gelijk aan de velden die vereist zijn voor een PUT-aanvraag.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
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
| `optionalLabels` | Een lijst van om het even welke individuele gebieden binnen de dataset die u etiketten aan wilt toevoegen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de kenmerken [!DNL Experience Data Model] (XDM) van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li>id</code>: De URI $id</code> -waarde van het schema dat aan het veld is gekoppeld.</li><li>contentType</code>: Het inhoudstype en het versienummer van het schema. Dit zou de vorm van één van de geldige kopballen <a href="../../xdm/api/look-up-resource.md">van de</a> Acceptie voor een XDM raadplegingsverzoek moeten hebben.</li><li>schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

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

## Labels uit een gegevensset verwijderen {#remove}

U kunt de labels verwijderen die op een gegevensset zijn toegepast door een DELETE-aanvraag in te dienen bij de [!DNL Dataset Service] API.

**API-indeling**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset waarvan etiketten u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde HTTP-respons status 200 (OK) die aangeeft dat de labels zijn verwijderd. U kunt de bestaande etiketten [voor de dataset in een afzonderlijke vraag](#look-up) omhoog kijken om dit te bevestigen.

## Volgende stappen

Door dit document te lezen hebt u geleerd hoe u labels voor gegevensgebruik voor gegevenssets en velden kunt beheren met behulp van de [!DNL Dataset Service] API.

Zodra u de etiketten van het gegevensgebruik op dataset en gebied-niveau hebt toegevoegd, kunt u beginnen gegevens in te nemen [!DNL Experience Platform]. Voor meer informatie begint u met het lezen van de [gegevensinvoerdocumentatie](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie het overzicht [van beleidsregels voor](../policies/overview.md)gegevensgebruik voor meer informatie.

Voor meer informatie bij het beheren van datasets in [!DNL Experience Platform], zie het [datasetoverzicht](../../catalog/datasets/overview.md).