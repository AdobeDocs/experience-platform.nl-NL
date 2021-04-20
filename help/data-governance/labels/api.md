---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;label api voor gegevensgebruik;beleidservice api
solution: Experience Platform
title: 'Labels voor gegevensgebruik beheren met API''s '
topic: developer guide
description: Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API voor catalogusservice die metagegevens van gegevenssets beheert.
translation-type: tm+mt
source-git-commit: 4e75e3fbdcd480c384411c2f33bad5b2cdcc5c42
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 1%

---


# Gegevensgebruikslabels beheren met API&#39;s

Dit document bevat stappen voor het beheren van labels voor gegevensgebruik met de API [!DNL Policy Service] en [!DNL Dataset Service].

[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) verstrekt verscheidene eindpunten die u toestaan om de etiketten van het gegevensgebruik voor uw organisatie tot stand te brengen en te beheren.

Met de [!DNL Dataset Service]-API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Het maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API [!DNL Catalog Service] die metagegevens van gegevenssets beheert.

## Aan de slag

Alvorens u deze gids leest, volg de stappen in [begonnen sectie](../../catalog/api/getting-started.md) in de de ontwikkelaarsgids van de Catalogus worden geschetst om de vereiste geloofsbrieven te verzamelen om vraag aan [!DNL Platform] APIs te maken die.

Als u aanroepen wilt uitvoeren naar de [!DNL Dataset Service]-eindpunten die in dit document worden beschreven, moet u de unieke `id`-waarde voor een specifieke gegevensset hebben. Als u deze waarde niet hebt, zie de gids op [het vermelden van de voorwerpen van de Catalogus](../../catalog/api/list-objects.md) om identiteitskaarts van uw bestaande datasets te vinden.

## Alle labels {#list-labels} weergeven

Met de [!DNL Policy Service] API kunt u alle `core`- of `custom`-labels weergeven door een GET-aanvraag in te dienen bij `/labels/core` of `/labels/custom`.

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

Een succesvolle reactie keert een lijst van douanelabels terug die van het systeem worden teruggewonnen. Aangezien het voorbeeldverzoek hierboven aan `/labels/custom` werd gemaakt, toont de reactie hieronder slechts douanelabels.

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

## Label {#look-up-label} opzoeken

U kunt een specifiek etiket opzoeken door het `name` bezit van dat etiket in de weg van een verzoek van de GET aan [!DNL Policy Service] API te omvatten.

**API-indeling**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De eigenschap `name` van het aangepaste label dat u wilt opzoeken. |

**Verzoek**

Het volgende verzoek wint het douanelabel `L2`, zoals die in de weg wordt vermeld terug.

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

Als u een aangepast label wilt maken of bijwerken, moet u een PUT aanvragen bij de [!DNL Policy Service]-API.

**API-indeling**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{LABEL_NAME}` | De eigenschap `name` van een aangepast label. Als er geen aangepast label met deze naam bestaat, wordt een nieuw label gemaakt. Als er een label bestaat, wordt dat label bijgewerkt. |

**Verzoek**

Met het volgende verzoek wordt een nieuw label gemaakt, `L3`, waarmee gegevens worden beschreven die informatie bevatten over de geselecteerde betaalplannen van klanten.

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
| `category` | De categorie van het etiket. Terwijl u uw eigen categorieën voor douanelabels kunt tot stand brengen, wordt het sterk geadviseerd dat u `Custom` gebruikt als u het etiket in UI wilt verschijnen. |
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

## Labels opzoeken voor een gegevensset {#look-up-dataset-labels}

U kunt de etiketten van het gegevensgebruik opzoeken die op een bestaande dataset zijn toegepast door een verzoek van de GET aan [!DNL Dataset Service] API te richten.

**API-indeling**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id` waarde van de dataset de waarvan etiketten u omhoog wilt kijken. |

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
| `optionalLabels` | Een lijst van individuele gebieden binnen de dataset die de etiketten van het gegevensgebruik hebben op hen worden toegepast. De volgende subeigenschappen zijn vereist:<br/><br/>`option`: Een object dat de [!DNL Experience Data Model] (XDM) kenmerken van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li>`id`: De URI- `$id` waarde van het schema dat aan het veld is gekoppeld.</li><li>`contentType`: Geeft de indeling en versie van het schema aan. Zie de sectie over [schemaversie](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie.</li><li>`schemaPath`: Het pad naar de schemaeigenschap in kwestie, geschreven in  [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersyntax.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

- id: De URI $id-waarde voor het XDM-schema waarop de gegevensset is gebaseerd.
- contentType: Geeft de indeling en versie van het schema aan. Zie de sectie over [schemaversie](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie.
- schemaPath: Het pad naar de schemaeigenschap in kwestie, geschreven in [JSON-aanwijzer](../../landing/api-fundamentals.md#json-pointer) syntaxis.

## Labels toepassen op een gegevensset {#apply-dataset-labels}

U kunt een reeks etiketten voor een dataset tot stand brengen door hen in de nuttige lading van een POST of een verzoek van de PUT aan [!DNL Dataset Service] API te verstrekken. Als u een van deze methoden gebruikt, worden bestaande labels overschreven en vervangen door de labels in de payload.

**API-indeling**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De unieke `id`-waarde van de gegevensset waarvoor u labels maakt. |

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
| `optionalLabels` | Een lijst van om het even welke individuele gebieden binnen de dataset die u etiketten aan wilt toevoegen. Elk item in deze array moet de volgende eigenschappen hebben:<br/><br/>`option`: Een object dat de [!DNL Experience Data Model] (XDM) kenmerken van het veld bevat. De volgende drie eigenschappen zijn vereist:<ul><li>`id`: De URI- `$id` waarde van het schema dat aan het veld is gekoppeld.</li><li>`contentType`: Geeft de indeling en versie van het schema aan. Zie de sectie over [schemaversie](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie.</li><li>`schemaPath`: Het pad naar de schemaeigenschap in kwestie, geschreven in  [JSON ](../../landing/api-fundamentals.md#json-pointer) Pointersyntax.</li></ul>`labels`: Een lijst met gegevensgebruikslabels die u aan het veld wilt toevoegen. |

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

U kunt de etiketten verwijderen die op een dataset worden toegepast door een verzoek van DELETE aan [!DNL Dataset Service] API te doen.

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

Een geslaagde HTTP-respons status 200 (OK) die aangeeft dat de labels zijn verwijderd. U kunt [opzoeken bestaande labels](#look-up-dataset-labels) voor de dataset in een afzonderlijke vraag om dit te bevestigen.

## Volgende stappen

Door dit document te lezen hebt u geleerd hoe u labels voor gegevensgebruik met API&#39;s kunt beheren.

Zodra u de etiketten van het gegevensgebruik op dataset en gebied-niveau hebt toegevoegd, kunt u beginnen om gegevens in [!DNL Experience Platform] in te nemen. Als u meer wilt weten, begint u met het lezen van de [documentatie voor gegevensinvoer](../../ingestion/home.md).

U kunt nu ook beleid voor gegevensgebruik definiëren op basis van de labels die u hebt toegepast. Voor meer informatie, zie [beleidsoverzicht van het gegevensgebruik](../policies/overview.md).

Voor meer informatie over het beheren van datasets in [!DNL Experience Platform], zie [datasetoverzicht](../../catalog/datasets/overview.md).