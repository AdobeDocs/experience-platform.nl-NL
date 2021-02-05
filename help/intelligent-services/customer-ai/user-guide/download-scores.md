---
keywords: Experience Platform;downloadscores;klantenservice;populaire onderwerpen;Exporteren;exporteren;klantenservice downloaden;klantenservice scores
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Scores downloaden in AI van klant
topic: Downloading scores
description: Met AI van de klant kunt u scores downloaden in de Parquet-bestandsindeling.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# Muziek downloaden in AI van klant

Dit document fungeert als richtlijn voor het downloaden van scores voor AI-bestanden van de Klant.

## Aan de slag

Met AI van de klant kunt u scores downloaden in de Parquet-bestandsindeling. Deze zelfstudie vereist dat u de sectie voor het downloaden van AI-scores van de klant in de [Aan de slag](../getting-started.md)-handleiding hebt gelezen en voltooid.

Daarnaast moet u een service-instantie met een geslaagde status hebben om toegang te krijgen tot scores voor de AIR-service. Als u een nieuwe service-instantie wilt maken, gaat u naar [Een Customer AI-instantie configureren](./configure.md). Als u onlangs een de dienstinstantie creeerde en het nog opleidt en het scoring, gelieve 24 uren voor het te beëindigen loopt.

Er zijn momenteel twee manieren om AI-scores van klanten te downloaden:

1. Als u de scores op het individuele niveau wilt downloaden en/of geen In real time toegelaten Profiel van de Klant wilt hebben, begin door aan [zoekend uw dataset ID](#dataset-id) te navigeren.
2. Als u Profiel hebt ingeschakeld en segmenten wilt downloaden die u hebt geconfigureerd met Customer AI, navigeert u naar [een segment downloaden dat is geconfigureerd met Customer AI](#segment).

## Uw gegevensset-id {#dataset-id} zoeken

Binnen uw de dienstinstantie voor de Inzichten van de Klant AI, klik *Meer acties* dropdown in de top-right navigatie dan uitgezocht **[!UICONTROL de scores van de Toegang]**.

![meer acties](../images/insights/more-actions.png)

Er wordt een nieuw dialoogvenster weergegeven met een koppeling naar de documentatie van downloadscores en de id van de gegevensset voor uw huidige instantie. Kopieer de id van de gegevensset naar het klembord en ga verder met de volgende stap.

![Dataset-id](../images/download-scores/access-scores.png)

## De batch-id {#retrieve-your-batch-id} ophalen

Gebruikend uw dataset identiteitskaart van de vorige stap, moet u een vraag aan de Catalogus API maken om een partijidentiteitskaart terug te winnen. Voor deze API-aanroep worden aanvullende queryparameters gebruikt om de laatste succesvolle batch te retourneren in plaats van een lijst met batches die bij uw organisatie horen. Om extra partijen terug te keren, verhoog het aantal voor de parameter van de grensvraag tot de gewenste hoeveelheid u wenst om te zijn teruggekeerd. Voor meer informatie over de types van vraagparameters beschikbaar, bezoek de gids over [het filtreren van de gegevens van de Catalogus gebruikend vraagparameters](../../../catalog/api/filter-data.md).

**API-indeling**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De dataset-id beschikbaar in het dialoogvenster &quot;Toegangsscores&quot;. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lading die een batch-id-object bevat. In dit voorbeeld is de sleutelwaarde voor het geretourneerde object de batch-id `01E5QSWCAASFQ054FNBKYV6TIQ`. Kopieer de batch-id die u wilt gebruiken in de volgende API-aanroep.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## De volgende API-aanroep ophalen met uw batch-id {#retrieve-the-next-api-call-with-your-batch-id}

Zodra u uw partij-identiteitskaart hebt, kunt u een nieuw verzoek van de GET aan `/batches` indienen. De aanvraag retourneert een koppeling die wordt gebruikt als de volgende API-aanvraag.

**API-indeling**

```http
GET batches/{BATCH_ID}/files
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De batch-id die is opgehaald in de vorige stap [haalt uw batch-id](#retrieve-your-batch-id) op. |

**Verzoek**

Voer de volgende aanvraag uit met uw eigen batch-id.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die een object `_links` bevat. Binnen het `_links` voorwerp is een `href` met een nieuwe API vraag als zijn waarde. Kopieer deze waarde om door te gaan naar de volgende stap.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## Bestanden {#retrieving-your-files} ophalen

Gebruikend de `href` waarde u in de vorige stap als API vraag kreeg, doe een nieuw verzoek van de GET om uw dossierfolder terug te winnen.

**API-indeling**

```http
GET files/{DATASETFILE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASETFILE_ID}` | De dataSetFile-id wordt geretourneerd in de `href`-waarde van de [vorige stap](#retrieve-the-next-api-call-with-your-batch-id). Het is ook toegankelijk in de `data` serie onder het objecten type `dataSetFileId`. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie bevat een gegevensarray die één item kan hebben, of een lijst met bestanden die tot die map behoren. Het onderstaande voorbeeld bevat een lijst met bestanden en is gecondenseerd voor leesbaarheid. In dit scenario moet u de URL van elk bestand volgen om toegang te krijgen tot het bestand.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `_links.self.href` | De aanvraag-URL van de GET die wordt gebruikt om een bestand in uw map te downloaden. |


Kopieer de waarde `href` voor een willekeurig bestandsobject in de array `data` en ga vervolgens verder met de volgende stap.

## Bestandsgegevens downloaden

Als u de bestandsgegevens wilt downloaden, vraagt u een GET aan om de `"href"`-waarde die u in de vorige stap hebt gekopieerd [bestanden ophalen](#retrieving-your-files).

>[!NOTE]
>
>Als u dit verzoek direct in bevellijn doet, zou u kunnen worden ertoe aangezet om een output na uw verzoekkopballen toe te voegen. In het volgende aanvraagvoorbeeld wordt `--output {FILENAME.FILETYPE}` gebruikt.

**API-indeling**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASETFILE_ID}` | De dataSetFile-id wordt geretourneerd in de `href`-waarde van een [vorige stap](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | De naam van het bestand. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Zorg ervoor dat u zich in de juiste map of map bevindt waarnaar u het bestand wilt opslaan voordat u de GET-aanvraag indient.

**Antwoord**

Het antwoord downloadt het bestand dat u in de huidige map hebt aangevraagd. In dit voorbeeld is de bestandsnaam &quot;filename.parquet&quot;.

![Terminal](../images/download-scores/response.png)

## Een segment downloaden dat is geconfigureerd met Customer AI {#segment}

Een andere manier om uw score te downloaden is door uw publiek naar een dataset te exporteren. Nadat een segmentatietaak met succes is voltooid (de waarde van het `status` attribuut is &quot;SUCCEEDED&quot;), kunt u uw publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld. Voor meer informatie over segmentatie gaat u naar [segmentatieoverzicht](../../../segmentation/home.md).

>[!IMPORTANT]
>
>Om deze methode van het uitvoeren te gebruiken, moet het Profiel van de Klant in real time voor de dataset worden toegelaten.

De [uitvoer een segment](../../../segmentation/tutorials/evaluate-a-segment.md) sectie in de gids van de segmentevaluatie behandelt de vereiste stappen om een publieksdataset uit te voeren. In de handleiding worden de volgende voorbeelden geschetst en gegeven:

- **Creeer een doeldataset:** Creeer de dataset om publieksleden te houden.
- **Genereer publieksprofielen in de dataset:** Vul de dataset met Individuele Profielen XDM die op de resultaten van een segmentbaan worden gebaseerd.
- **Voortgang van exporteren controleren:** controleer de huidige voortgang van het exportproces.
- **Lees publieksgegevens:** Haal de resulterende afzonderlijke XDM-profielen op die de leden van uw publiek vertegenwoordigen.

## Volgende stappen

In dit document worden de stappen beschreven die zijn vereist voor het downloaden van AI-scores van de klant. U kunt nu door de andere [Intelligente services](../../home.md) en gidsen blijven bladeren die worden aangeboden.
