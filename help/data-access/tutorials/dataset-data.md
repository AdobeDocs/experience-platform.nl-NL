---
keywords: Experience Platform;home;populaire onderwerpen;toegang tot gegevens;API voor gegevenstoegang;toegang tot querygegevens
solution: Experience Platform
title: Gegevens gegevensset weergeven met de API voor gegevenstoegang
type: Tutorial
description: Leer hoe u gegevens kunt zoeken, openen en downloaden die zijn opgeslagen in een gegevensset met de API voor gegevenstoegang in Adobe Experience Platform. In dit document worden enkele unieke functies van de API voor gegevenstoegang geïntroduceerd, zoals pagineren en gedeeltelijke downloads.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Gegevenssetgegevens weergeven met de API [!DNL Data Access]

In deze stapsgewijze zelfstudie leert u hoe u in een gegevensset opgeslagen gegevens kunt zoeken, openen en downloaden met de API van [!DNL Data Access] in Adobe Experience Platform. In dit document worden enkele unieke functies van de API van [!DNL Data Access] geïntroduceerd, zoals pagineren en gedeeltelijke downloads.

## Aan de slag

Deze zelfstudie vereist een goed begrip van hoe u een dataset maakt en vult. Zie het [ leerprogramma van de datasetverwezenlijking ](../../catalog/datasets/create.md) voor meer informatie.

De volgende secties verstrekken extra informatie die u moet weten om met succes vraag aan Experience Platform APIs te maken.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](../../landing/api-authentication.md) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Sequentiediagram

Deze zelfstudie volgt de stappen die in het onderstaande reeksdiagram worden beschreven en markeert de kernfunctionaliteit van de [!DNL Data Access] API.

![ een opeenvolgingsdiagram van de de kernfunctionaliteit van de Toegang API van Gegevens.](../images/sequence_diagram.png)

Gebruik de API van [!DNL Catalog] om informatie over batches en bestanden op te halen. Gebruik de API [!DNL Data Access] om deze bestanden via HTTP te openen en te downloaden als volledige of gedeeltelijke downloads, afhankelijk van de grootte van het bestand.

## De gegevens zoeken

Voordat u de API van [!DNL Data Access] kunt gaan gebruiken, moet u de locatie identificeren van de gegevens waartoe u toegang wilt hebben. In de API van [!DNL Catalog] zijn er twee eindpunten die u kunt gebruiken om de meta-gegevens van een organisatie te doorbladeren en identiteitskaart van een partij of een dossier terug te winnen dat u wilt toegang hebben:

- `GET /batches`: retourneert een lijst met batches in uw organisatie
- `GET /dataSetFiles`: retourneert een lijst met bestanden binnen uw organisatie

Voor een uitvoerige lijst van eindpunten in [!DNL Catalog] API, verwijs naar de [ API Verwijzing ](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## Een lijst met batches in uw organisatie ophalen

Met de API van [!DNL Catalog] kunt u een lijst met batches retourneren onder uw organisatie:

**API formaat**

```http
GET /batches
```

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

De reactie omvat een voorwerp dat van alle partijen met betrekking tot de organisatie een lijst maakt, met elke top-level waarde die een partij vertegenwoordigt. De afzonderlijke batchobjecten bevatten de gegevens voor die specifieke batch. De onderstaande reactie is geminimaliseerd voor ruimte.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
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

### De lijst met batches filteren {#filter-batches-list}

Filters moeten vaak een bepaalde batch zoeken om relevante gegevens voor een bepaald gebruiksgeval op te halen. Parameters kunnen worden toegevoegd aan een `GET /batches` -aanvraag om de geretourneerde reactie te filteren. De onderstaande aanvraag retourneert alle batches die na een opgegeven tijd zijn gemaakt, binnen een bepaalde gegevensset, gesorteerd op het tijdstip waarop ze zijn gemaakt.

**API formaat**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{START_TIMESTAMP}` | De begintijdstempel in milliseconden (bijvoorbeeld 1514836799000). |
| `{DATASET_ID}` | De id van de gegevensset. |
| `{SORT_BY}` | Sorteert de reactie met de opgegeven waarde. `desc:created` sorteert de objecten bijvoorbeeld op aanmaakdatum in aflopende volgorde. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

Een volledige lijst van parameters en filters kan in de [ van de Catalogus API verwijzing ](https://developer.adobe.com/experience-platform-apis/references/catalog/) worden gevonden.

## Een lijst ophalen van alle bestanden die tot een bepaalde batch behoren

Nu u de id hebt van de batch waartoe u toegang wilt hebben, kunt u de API van [!DNL Data Access] gebruiken om een lijst op te halen met bestanden die tot die batch behoren.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

De reactie bevat een gegevensarray met alle bestanden in de opgegeven batch. Naar bestanden wordt verwezen door hun bestands-id, die u vindt onder het veld `dataSetFileId` .

## Een bestand openen met een bestands-id {#access-file-with-file-id}

Als u een unieke bestands-id hebt, kunt u de API van [!DNL Data Access] gebruiken om toegang te krijgen tot de specifieke details van het bestand, zoals de naam, grootte in bytes en een koppeling om het bestand te downloaden.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Afhankelijk van of de bestands-id naar een afzonderlijk bestand of naar een map verwijst, kan de geretourneerde gegevensarray één item of een lijst met bestanden bevatten die tot die map behoren. Elk bestandselement bevat details zoals de naam van het bestand, de grootte in bytes en een koppeling om het bestand te downloaden.

**Geval 1: Identiteitskaart van het dossier richt aan één enkel dossier**

**Reactie**

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

**Geval 2: Identiteitskaart van het dossier richt aan een folder**

**Reactie**

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

Deze reactie retourneert een map met twee afzonderlijke bestanden, met id&#39;s `{FILE_ID_2}` en `{FILE_ID_3}` . In dit scenario moet u de URL van elk bestand volgen om toegang te krijgen tot het bestand.

## De metagegevens van een bestand ophalen

U kunt de metagegevens van een bestand ophalen door een HEAD-aanvraag in te dienen. Hiermee worden de metagegevenskoppen van het bestand geretourneerd, inclusief de grootte in bytes en bestandsindeling.

**API formaat**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand. |
| `{FILE_NAME}` | De bestandsnaam (bijvoorbeeld profiles.parquet) |

**Verzoek**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

De antwoordheaders bevatten de metagegevens van het bestand waarnaar wordt gevraagd, waaronder:

- `Content-Length`: geeft de grootte van de payload in bytes aan
- `Content-Type` - Geeft het bestandstype aan.

## De inhoud van een bestand openen

U kunt de inhoud van een bestand ook benaderen met de API [!DNL Data Access] .

**API formaat**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand. |
| `{FILE_NAME}` | De bestandsnaam (bijvoorbeeld profiles.parquet). |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Als de reactie is gelukt, wordt de inhoud van het bestand geretourneerd.

## Gedeeltelijke inhoud van een bestand downloaden {#download-partial-file-contents}

Als u een specifiek bytebereik van een bestand wilt downloaden, geeft u een bereikkoptekst op tijdens een `GET /files/{FILE_ID}` -aanvraag naar de [!DNL Data Access] API. Als het bereik niet is opgegeven, downloadt de API standaard het gehele bestand.

Het voorbeeld van HEAD in de [ vorige sectie ](#retrieve-the-metadata-of-a-file) geeft de grootte van een specifiek dossier in bytes.

**API formaat**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{FILE_ID}` | De id van het bestand. |
| `{FILE_NAME}` | De bestandsnaam (bijvoorbeeld profiles.parquet) |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Eigenschap | Beschrijving |
| -------- | ----------- | 
| `Range: bytes=0-99` | Geeft het bereik aan van bytes dat moet worden gedownload. Als dit niet is opgegeven, downloadt de API het gehele bestand. In dit voorbeeld worden de eerste 100 bytes gedownload. |

**Reactie**

De hoofdtekst van de reactie bevat de eerste 100 bytes van het bestand (zoals opgegeven door de header &quot;Range&quot; in de aanvraag) samen met HTTP Status 206 (Partiële inhoud). De reactie omvat ook de volgende kopteksten:

- Content-Length: 100 (het aantal geretourneerde bytes)
- Content-type: application/parquet (er is een Parquet-bestand aangevraagd, daarom is het type inhoud voor reactie `parquet`)
- Content-Range: bytes 0-99/249058 (het gevraagde bereik (0-99) van het totale aantal bytes (249058))

## Paginering van API-reactie configureren {#configure-response-pagination}

Reacties binnen de API van [!DNL Data Access] worden gepagineerd. Standaard is het maximumaantal items per pagina 100. U kunt het standaardgedrag met het pagineren parameters wijzigen.

- `limit`: u kunt het aantal items per pagina volgens uw vereisten opgeven met de parameter &quot;limit&quot;.
- `start`: De verschuiving kan worden ingesteld door de queryparameter &quot;start&quot;.
- `&`: U kunt een ampersand gebruiken om veelvoudige parameters in één enkele vraag te combineren.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**:

De reactie bevat een `"data"` -array met één element, zoals opgegeven door de parameter request `limit=1` . Dit element is een object dat de details bevat van het eerste beschikbare bestand, zoals opgegeven door de parameter `start=0` in de aanvraag (houd er rekening mee dat bij op nul gebaseerde nummering het eerste element &quot;0&quot; is).

De waarde `_links.next.href` bevat de koppeling naar de volgende pagina met reacties, waar u kunt zien dat de parameter `start` is doorgegeven aan `start=1` .

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
