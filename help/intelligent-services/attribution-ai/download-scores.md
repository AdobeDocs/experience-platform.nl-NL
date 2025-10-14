---
keywords: Experience Platform;attributie ai;access scores;populaire onderwerpen;download scores;attributie ai scores;export;Export
feature: Attribution AI
title: Scores downloaden in Attribution AI
description: Dit document dient als richtlijn voor het downloaden van scores voor Attribution AI.
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---

# Muziek downloaden in Attribution AI

Dit document dient als richtlijn voor het downloaden van scores voor Attribution AI.

## Aan de slag

Met Attribution AI kunt u scores downloaden in de Parquet-bestandsindeling. Dit leerprogramma vereist dat u hebt gelezen en de het downloaden sectie van de scores van Attribution AI in [&#x200B; gebeëindigd die &#x200B;](./getting-started.md) gids begonnen wordt.

Bovendien, om tot scores voor Attribution AI toegang te hebben, moet u een de dienstinstantie hebben met een succesvolle looppasstatus beschikbaar. Om een nieuwe de dienstinstantie tot stand te brengen, bezoek de [&#x200B; gebruikersgids van de Attribution AI &#x200B;](./user-guide.md). Als u onlangs een de dienstinstantie creeerde en het nog opleidt en het scoring, gelieve 24 uren voor het te beëindigen loopt.

## Uw gegevensset-id zoeken {#dataset-id}

Binnen uw de dienstinstantie voor Attribution AI inzichten, klik *Meer acties* dropdown in de top-juiste navigatie dan selecteren **[!UICONTROL Access scores]**.

![&#x200B; meer acties &#x200B;](./images/download-scores/more-actions.png)

Er wordt een nieuw dialoogvenster weergegeven met een koppeling naar de documentatie van downloadscores en de id van de gegevensset voor uw huidige instantie. Kopieer de id van de gegevensset naar het klembord en ga verder met de volgende stap.

![&#x200B; identiteitskaart van de Dataset &#x200B;](../customer-ai/images/download-scores/access-scores.png)

## Batch-id ophalen {#retrieve-your-batch-id}

Gebruikend uw dataset identiteitskaart van de vorige stap, moet u een vraag aan de Catalogus API maken om een partijidentiteitskaart terug te winnen. Voor deze API-aanroep worden aanvullende queryparameters gebruikt om de laatste succesvolle batch te retourneren in plaats van een lijst met batches die bij uw organisatie horen. Als u extra batches wilt retourneren, verhoogt u het getal voor de parameter `limit` query tot de gewenste hoeveelheid die u wilt retourneren. Voor meer informatie over de types van beschikbare vraagparameters, bezoek de gids bij [&#x200B; het filtreren gegevens van de Catalogus gebruikend vraagparameters &#x200B;](../../catalog/api/filter-data.md).

**API formaat**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASET_ID}` | De dataset-id beschikbaar in het dialoogvenster &quot;Toegangsscores&quot;. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert een lading die een batch-id-object bevat. In dit voorbeeld is de waarde Key aan het geretourneerde object de batch-id `01E5QSWCAASFQ054FNBKYV6TIQ` . Kopieer uw batch-id voor gebruik in de volgende API-aanroep.

>[!NOTE]
>
> In de volgende reactie is het `tags` -object hervormd voor leesbaarheid.

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
                "id": "5e8f81cf7a4ecb28a8d85b22"
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

Als u eenmaal een batch-id hebt, kunt u een nieuwe aanvraag indienen bij `/batches` . De aanvraag retourneert een koppeling die wordt gebruikt als de volgende API-aanvraag.

**API formaat**

```http
GET batches/{BATCH_ID}/files
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De partijidentiteitskaart die in de vorige stap [&#x200B; werd teruggewonnen wint uw partijidentiteitskaart &#x200B;](#retrieve-your-batch-id) terug. |

**Verzoek**

Voer de volgende aanvraag uit met uw eigen batch-id.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert een payload die een `_links` -object bevat. Binnen het `_links` -object bevindt zich een `href` met een nieuwe API-aanroep als waarde. Kopieer deze waarde om door te gaan naar de volgende stap.

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
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

## Bestanden ophalen {#retrieving-your-files}

Maak een nieuwe aanvraag voor het ophalen van de bestandsmap met de `href` -waarde die u in de vorige stap als API-aanroep hebt gekregen.

**API formaat**

```http
GET files/{DATASETFILE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASETFILE_ID}` | ID dataSetFile is teruggekeerd in de `href` waarde van de [&#x200B; vorige stap &#x200B;](#retrieve-the-next-api-call-with-your-batch-id). De eigenschap is ook toegankelijk in de array `data` onder het objecttype `dataSetFileId` . |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

De reactie bevat een gegevensarray die één item kan hebben, of een lijst met bestanden die tot die map behoren. Het onderstaande voorbeeld bevat een lijst met bestanden en is gecondenseerd voor leesbaarheid. In dit scenario moet u de URL van elk bestand volgen om toegang te krijgen tot het bestand.

```json
{
    "data": [
        {
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
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

| Parameter | Beschrijving |
| --------- | ----------- |
| `_links.self.href` | De aanvraag-URL van de GET die wordt gebruikt om een bestand in uw map te downloaden. |


Kopieer de `href` -waarde voor een willekeurig bestandsobject in de `data` -array en ga vervolgens verder met de volgende stap.

## Bestandsgegevens downloaden

Om uw dossiergegevens te downloaden, doe een verzoek van de GET aan de `"href"` waarde u in de vorige stap [&#x200B; het terugwinnen van uw dossiers &#x200B;](#retrieving-your-files) kopieerde.

>[!NOTE]
>
>Als u dit verzoek direct in bevellijn doet, zou u kunnen worden ertoe aangezet om een output na uw verzoekkopballen toe te voegen. In het volgende aanvraagvoorbeeld wordt `--output {FILENAME.FILETYPE}` gebruikt.

**API formaat**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASETFILE_ID}` | ID dataSetFile is teruggekeerd in de `href` waarde van a [&#x200B; vorige stap &#x200B;](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | De naam van het bestand. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Zorg ervoor dat u zich in de juiste map of map bevindt waarnaar u het bestand wilt opslaan voordat u de GET-aanvraag indient.

**Reactie**

Het antwoord downloadt het bestand dat u in de huidige map hebt aangevraagd. In dit voorbeeld is de bestandsnaam &quot;file.parquet&quot;.

![&#x200B; Eind &#x200B;](./images/download-scores/terminal-output.png)

De gedownloade scores hebben de Parquet-indeling en hebben een [!DNL Spark]-shell- of Parquet-lezer nodig om de scores weer te geven. Voor onbewerkte score die, kunt u [&#x200B; gebruiken de hulpmiddelen van het Pakket Apache &#x200B;](https://parquet.apache.org/docs/). Met de gereedschappen Parquet kunt u de gegevens analyseren met [!DNL Spark] .

## Volgende stappen

In dit document worden de stappen beschreven die zijn vereist voor het downloaden van scores van Attribution AI. Voor meer informatie over de score output, gelieve te bezoeken de [&#x200B; input en outputAI van de Attribune &#x200B;](./input-output.md) documentatie.

## Muziek openen met Snowflake

>[!IMPORTANT]
>
>Neem contact op met attributionai-support@adobe.com voor meer informatie over het gebruik van scores via Snowflake.

U kunt tot samengevoegde Attribution AI scores door Snowflake toegang hebben. U moet momenteel ondersteuning voor Adoben via e-mail verzenden naar attributionai-support@adobe.com om de referenties voor Snowflake in te stellen en te ontvangen bij uw lezeraccount.

Nadat de ondersteuning van de Adobe uw verzoek heeft verwerkt, krijgt u een URL voor het lezeraccount naar de Snowflake en de bijbehorende referenties hieronder:

- Snowflake-URL
- Gebruikersnaam
- Wachtwoord

>[!NOTE]
>
>De lezeraccount is bedoeld voor het opvragen van gegevens met SQL-clients, werkbladen en BI-oplossingen die JDBC-connector ondersteunen.

Zodra u uw geloofsbrieven en URL hebt, kunt u de modellijsten vragen, die door touchpoint datum, of omzettingsdatum worden bijeengevoegd.

### Schema zoeken in Snowflake

Meld u aan bij Snowflake met de opgegeven referenties. Klik het **lusje van Werkbladen** in de top-linker belangrijkste navigatie, dan navigeer aan uw gegevensbestandfolder in het linkerpaneel.

![&#x200B; Werkbladen &amp; het navigeren &#x200B;](./images/download-scores/edited_snowflake_1.png)

Daarna, klik **Uitgezochte Schema** in de hoger-juiste hoek van het scherm. Bevestig in de pop-up die wordt weergegeven dat u de juiste database hebt geselecteerd. Daarna, klik het *Schema* dropdown en selecteer één van uw vermelde schema&#39;s. U kunt rechtstreeks zoeken vanuit de scoretabellen die onder het geselecteerde schema staan.

![&#x200B; vind een schema &#x200B;](./images/download-scores/edited_snowflake_2.png)

## PowerBI aansluiten op Snowflake (optioneel)

Uw aanmeldingsgegevens voor de Snowflake kunnen worden gebruikt om een verbinding tot stand te brengen tussen PowerBI Desktop- en Snowflake-databases.

Eerst, onder het *vakje van de Server*, type in uw Snowflake URL. Daarna, onder *Warehouse*, type in &quot;XSMALL&quot;. Typ vervolgens uw gebruikersnaam en wachtwoord.

![&#x200B; voorbeeld van POWERBI &#x200B;](./images/download-scores/powerbi-snowflake.png)

Nadat de verbinding wordt gevestigd, selecteer uw gegevensbestand van de Snowflake, dan selecteer het aangewezen schema. U kunt nu alle tabellen laden.
