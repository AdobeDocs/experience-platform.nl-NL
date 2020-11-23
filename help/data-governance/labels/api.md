---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api
solution: Experience Platform
title: 'Gegevensgebruikslabels beheren met API''s '
topic: developer guide
description: Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API voor catalogusservice die metagegevens van gegevenssets beheert.
translation-type: tm+mt
source-git-commit: 4b5e116d221e6689f95c8da0c54ef3af6827adc1
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---


# Gegevensgebruikslabels beheren met API&#39;s

In dit document worden stappen beschreven voor het beheren van labels voor gegevensgebruik met de [!DNL Policy Service] API en de [!DNL Dataset Service] API.

Het [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) biedt verschillende eindpunten waarmee u labels voor gegevensgebruik voor uw organisatie kunt maken en beheren.

Met de [!DNL Dataset Service] API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Het maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de [!DNL Catalog Service] API die metagegevens van gegevenssets beheert.

## Aan de slag

Voordat u deze handleiding leest, volgt u de stappen in de sectie [Aan de](../../catalog/api/getting-started.md) slag in de handleiding voor ontwikkelaars van catalogi om de vereiste gegevens te verzamelen voor het oproepen van [!DNL Platform] API&#39;s.

Om vraag aan de [!DNL Dataset Service] eindpunten te maken die in dit document worden geschetst, moet u de unieke `id` waarde voor een specifieke dataset hebben. Als u deze waarde niet hebt, raadpleegt u de handleiding bij het [weergeven van catalogusobjecten](../../catalog/api/list-objects.md) om de id&#39;s van uw bestaande gegevenssets te vinden.

## Alle labels weergeven {#list-labels}

Met de [!DNL Policy Service] API kunt u alle `core` of `custom` labels weergeven door een aanvraag voor een GET in te dienen bij `/labels/core` of `/labels/custom`.

**API-indeling**

```http
GET /labels/core
GET /labels/custom
```

**Verzoek**

In het volgende verzoek worden alle aangepaste labels weergegeven die in uw organisatie zijn gemaakt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van douanelabels terug die van het systeem worden teruggewonnen. Aangezien de voorbeeldaanvraag hierboven is ingediend, worden in de onderstaande reactie alleen aangepaste labels weergegeven. `/labels/custom`

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Een label opzoeken {#look-up-label}

U kunt een specifiek label opzoeken door de `name` eigenschap van dat label op te nemen in het pad van een aanvraag van een GET naar de [!DNL Policy Service] API.

**API-indeling**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De `name` eigenschap van het aangepaste label dat u wilt opzoeken. |

**Verzoek**

Met het volgende verzoek wordt het aangepaste label opgehaald, `L2`zoals aangegeven in het pad.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Als de reactie is gelukt, worden de details van het aangepaste label geretourneerd.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Een aangepast label maken of bijwerken {#create-update-label}

Als u een aangepast label wilt maken of bijwerken, moet u een aanvraag voor een PUT indienen bij de [!DNL Policy Service] API.

**API-indeling**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De `name` eigenschap van een aangepast label. Als er geen aangepast label met deze naam bestaat, wordt een nieuw label gemaakt. Als er een label bestaat, wordt dat label bijgewerkt. |

**Verzoek**

Het volgende verzoek leidt tot een nieuw etiket, `L3`dat gegevens beschrijft die informatie met betrekking tot de geselecteerde betalingsplannen van klanten bevatten.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | Een unieke tekenreeks-id voor het label. Deze waarde wordt gebruikt voor raadplegingsdoeleinden en het toepassen van het etiket op datasets en gebieden, en daarom wordt geadviseerd dat het kort en beknopt is. |
| `category` | De categorie van het etiket. Hoewel u uw eigen categorieën voor douanelabels kunt tot stand brengen, wordt het sterk geadviseerd dat u gebruikt `Custom` als u het etiket in UI wilt verschijnen. |
| `friendlyName` | Een vriendelijke naam voor het label, dat wordt gebruikt voor weergavedoeleinden. |
| `description` | (Optioneel) Een beschrijving van het label voor verdere context. |

**Antwoord**

Een geslaagde reactie retourneert de details van het aangepaste label, met HTTP-code 200 (OK) als een bestaand label is bijgewerkt, of 201 (Gemaakt) als een nieuw label is gemaakt.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## De etiketten van de raadpleging voor een dataset {#look-up-dataset-labels}

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

## Labels toepassen op een gegevensset {#apply-dataset-labels}

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
| `optionalLabels` | Een lijst van om het even welke individuele gebieden binnen de dataset die u etiketten aan wilt toevoegen. Elk item in deze array moet de volgende eigenschappen hebben: <br/><br/>`option`: Een object dat de kenmerken [!DNL Experience Data Model] (XDM) van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li>id</code>: De URI $id</code> -waarde van het schema dat aan het veld is gekoppeld.</li><li>contentType</code>: Het inhoudstype en het versienummer van het schema. Dit zou de vorm van één van de geldige kopballen <a href="../../xdm/api/getting-started.md#accept">van de</a> Acceptie voor een XDM raadplegingsverzoek moeten hebben.</li><li>schemaPath</code>: De weg aan het gebied binnen het schema van de dataset.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

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

## Labels uit een gegevensset verwijderen {#remove-dataset-labels}

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

Een geslaagde HTTP-respons status 200 (OK) die aangeeft dat de labels zijn verwijderd. U kunt de bestaande etiketten [voor de dataset in een afzonderlijke vraag](#look-up-dataset-labels) omhoog kijken om dit te bevestigen.

## Volgende stappen

Door dit document te lezen hebt u geleerd hoe u labels voor gegevensgebruik met API&#39;s kunt beheren.

Zodra u de etiketten van het gegevensgebruik op dataset en gebied-niveau hebt toegevoegd, kunt u beginnen gegevens in te nemen [!DNL Experience Platform]. Voor meer informatie begint u met het lezen van de [gegevensinvoerdocumentatie](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Zie het overzicht [van beleidsregels voor](../policies/overview.md)gegevensgebruik voor meer informatie.

Voor meer informatie bij het beheren van datasets in [!DNL Experience Platform], zie het [datasetoverzicht](../../catalog/datasets/overview.md).