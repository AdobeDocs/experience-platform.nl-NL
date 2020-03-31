---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van gegevenstoegang
topic: tutorial
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# De dataset van de vraag gegevens gebruikend API van de Toegang van Gegevens

Dit document biedt een stapsgewijze zelfstudie waarin wordt uitgelegd hoe u in een gegevensset opgeslagen gegevens kunt zoeken, openen en downloaden met behulp van de API voor gegevenstoegang in het Adobe Experience Platform. U zult ook aan enkele unieke eigenschappen van de Toegang API van Gegevens, zoals het pagineren en gedeeltelijke downloads worden geïntroduceerd.

## Aan de slag

Deze zelfstudie die inzicht geeft in hoe u een gegevensset kunt maken en vullen. Zie de [datasetverwezenlijking zelfstudie](../../catalog/datasets/create.md) voor meer informatie.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Sequentiediagram

Deze zelfstudie volgt de stappen die in het onderstaande reeksdiagram worden beschreven en markeert de kernfunctionaliteit van de API voor gegevenstoegang.</br>
![](../images/sequence_diagram.png)

Met de catalogus-API kunt u informatie over batches en bestanden ophalen. Met de API voor gegevenstoegang kunt u deze bestanden openen en downloaden via HTTP als volledige of gedeeltelijke downloads, afhankelijk van de grootte van het bestand.

## De gegevens zoeken

Voordat u de API voor gegevenstoegang kunt gaan gebruiken, moet u de locatie identificeren van de gegevens waartoe u toegang wilt hebben. In de Catalog API, zijn er twee eindpunten die u kunt gebruiken om de meta-gegevens van een organisatie te doorbladeren en identiteitskaart van een partij of een dossier terug te winnen dat u wilt toegang hebben:

- `GET /batches`: Retourneert een lijst met batches onder uw organisatie
- `GET /dataSetFiles`: Hiermee wordt een lijst met bestanden binnen uw organisatie geretourneerd

Raadpleeg de [API-naslaggids](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)voor een uitgebreide lijst met eindpunten in de catalogus-API.

## Een lijst met batches ophalen onder uw IMS-organisatie

Met de Catalog-API kunt u een lijst met batches retourneren onder uw organisatie:

**API-indeling**

```http
GET /batches
```

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie bevat een object dat een lijst bevat met alle batches die betrekking hebben op de IMS-organisatie, waarbij elke waarde op hoofdniveau een batch vertegenwoordigt. De afzonderlijke batchobjecten bevatten de gegevens voor die specifieke batch. De onderstaande reactie is geminimaliseerd voor ruimte.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### De lijst met batches filteren

Filters moeten vaak een bepaalde batch zoeken om relevante gegevens voor een bepaald gebruiksgeval op te halen. Parameters kunnen aan een `GET /batches` verzoek worden toegevoegd om de geretourneerde reactie te filteren. De onderstaande aanvraag retourneert alle batches die na een opgegeven tijd zijn gemaakt, binnen een bepaalde gegevensset, gesorteerd op het tijdstip waarop ze zijn gemaakt.

**API-indeling**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{START_TIMESTAMP}` | De begintijdstempel in milliseconden (bijvoorbeeld 1514836799000). |
| `{DATASET_ID}` | De id van de gegevensset. |
| `{SORT_BY}` | Sorteert de reactie met de opgegeven waarde. Hiermee kunt u bijvoorbeeld de objecten op aanmaakdatum in aflopende volgorde sorteren. `desc:created` |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{IMS_ORG}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

Een volledige lijst met parameters en filters vindt u in de API-naslaggids voor [catalogi](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

## Een lijst ophalen van alle bestanden die tot een bepaalde batch behoren

Nu u de id hebt van de batch waartoe u toegang wilt hebben, kunt u de API voor gegevenstoegang gebruiken om een lijst op te halen met bestanden die tot die batch behoren.

**API-indeling**

```http
GET /batches/{BATCH_ID}/files
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De batch-id van de batch waartoe u toegang probeert te krijgen. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `data._links.self.href` | De URL voor toegang tot dit bestand. |

De reactie bevat een gegevensarray met alle bestanden in de opgegeven batch. Er wordt naar bestanden verwezen door de bestands-id, die in het `dataSetFileId` veld staat.

## Een bestand openen met een bestands-id

Als u een unieke bestands-id hebt, kunt u de API voor gegevenstoegang gebruiken om toegang te krijgen tot de specifieke gegevens over het bestand, zoals de naam, grootte in bytes en een koppeling om het bestand te downloaden.

**API-indeling**

```http
GET /files/{FILE_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand dat u wilt openen. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Afhankelijk van of de bestands-id naar een afzonderlijk bestand of naar een map verwijst, kan de geretourneerde gegevensarray één item of een lijst met bestanden bevatten die tot die map behoren. Elk bestandselement bevat details zoals de naam van het bestand, de grootte in bytes en een koppeling om het bestand te downloaden.

**Zaak 1: Bestand-id verwijst naar één bestand**

**Antwoord**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
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

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | De naam van het bestand. |
| `_links.self.href` | De URL waarmee het bestand moet worden gedownload. |

**Zaak 2: Bestand-id verwijst naar een map**

**Antwoord**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `data._links.self.href` | De URL waarmee het gekoppelde bestand moet worden gedownload. |

Deze reactie retourneert een map met twee afzonderlijke bestanden, met id&#39;s `{FILE_ID_2}` en `{FILE_ID_3}`. In dit scenario moet u de URL van elk bestand volgen om toegang te krijgen tot het bestand.

## De metagegevens van een bestand ophalen

U kunt de metagegevens van een bestand ophalen door een HEAD-verzoek in te dienen. Hiermee worden de metagegevenskoppen van het bestand geretourneerd, inclusief de grootte in bytes en bestandsindeling.

**API-indeling**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand. |
| `{FILE_NAME`} | De bestandsnaam (bijvoorbeeld profiles.parquet) |

**Verzoek**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De antwoordheaders bevatten de metagegevens van het bestand waarnaar wordt gevraagd, waaronder:
- `Content-Length`: Geeft de grootte van de payload in bytes aan
- `Content-Type`: Geeft het bestandstype aan.

## De inhoud van een bestand openen

U kunt de inhoud van een bestand ook benaderen met de API voor gegevenstoegang.

**API-indeling**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand. |
| `{FILE_NAME`} | De bestandsnaam (bijvoorbeeld profiles.parquet). |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Met een succesvol antwoord wordt de inhoud van het bestand geretourneerd.

## Gedeeltelijke inhoud van een bestand downloaden

Met de API voor gegevenstoegang kunt u bestanden downloaden in blokken. Een bereikkoptekst kan worden opgegeven tijdens een `GET /files/{FILE_ID}` verzoek om een specifieke reeks bytes te downloaden uit een bestand. Als het bereik niet wordt opgegeven, downloadt de API standaard het gehele bestand.

In het HEAD-voorbeeld in de [vorige sectie](#retrieve-the-metadata-of-a-file) wordt de grootte van een specifiek bestand in bytes weergegeven.

**API-indeling**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID} ` | De id van het bestand. |
| `{FILE_NAME}` | De bestandsnaam (bijvoorbeeld profiles.parquet) |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `Range: bytes=0-99` | Geeft het bereik aan van bytes dat moet worden gedownload. Als dit niet is opgegeven, downloadt de API het gehele bestand. In dit voorbeeld worden de eerste 100 bytes gedownload. |

**Antwoord**

De hoofdtekst van de reactie bevat de eerste 100 bytes van het bestand (zoals opgegeven door de header &quot;Range&quot; in de aanvraag) samen met HTTP Status 206 (Partiële inhoud). De reactie omvat ook de volgende kopteksten:

- Content-Length: 100 (het aantal geretourneerde bytes)
- Inhoudstype: application/parquet (er is een parketbestand aangevraagd, zodat het type inhoud van het antwoord parket is)
- Inhoudsbereik: bytes 0-99/249058 (het gevraagde bereik (0-99) van het totale aantal bytes (249058))

## Paginering van API-reactie configureren

Reacties binnen de API voor gegevenstoegang worden gepagineerd. Standaard is het maximumaantal items per pagina 100. U kunt parameters voor paginering gebruiken om het standaardgedrag te wijzigen.

- `limit`: U kunt het aantal items per pagina volgens uw vereisten opgeven met de parameter &quot;limit&quot;.
- `start`: De verschuiving kan worden ingesteld door de queryparameter &quot;start&quot;.
- `&`: U kunt ampersand gebruiken om veelvoudige parameters in één enkele vraag te combineren.

**API-indeling**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De batch-id van de batch waartoe u toegang probeert te krijgen. |
| `{OFFSET}` | De opgegeven index die de resultaatarray moet starten (bijvoorbeeld start=0) |
| `{LIMIT}` | Bepaalt hoeveel resultaten worden geretourneerd in de resultaatarray (bijvoorbeeld limit=1) |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**:

De reactie bevat een `"data"` array met één element, zoals opgegeven door de parameter request `limit=1`. This element is an object containing the details of the first available file, as specified by the `start=0` parameter in the request (Herinner dat bij op nul gebaseerde nummering het eerste element &quot;0&quot; is).

De `_links.next.href` waarde bevat de koppeling naar de volgende pagina met reacties, waar u kunt zien dat de `start` parameter naar gevorderd is `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
