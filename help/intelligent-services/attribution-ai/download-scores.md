---
keywords: Experience Platform;attributie ai;access scores;populaire onderwerpen;download scores;attributie ai scores;export;Export
feature: Attribution AI
title: Scores downloaden in Attribution AI
topic-legacy: Downloading scores
description: Dit document dient als richtlijn voor het downloaden van scores voor Attribution AI.
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: 75426b1ddc16af39eb6c423027fac7d4d0e21c6a
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 0%

---

# Muziek downloaden in Attribution AI

Dit document dient als richtlijn voor het downloaden van scores voor Attribution AI.

## Aan de slag

Met Attribution AI kunt u scores downloaden in de Parquet-bestandsindeling. Deze zelfstudie vereist dat u het gedeelte met downloadscores voor Attribution AI in het dialoogvenster [aan de slag](./getting-started.md) hulplijn.

Bovendien, om tot scores voor Attribution AI toegang te hebben, moet u een de dienstinstantie hebben met een succesvolle looppasstatus beschikbaar. Als u een nieuwe service-instantie wilt maken, gaat u naar de [Gebruikershandleiding voor Attribution AI](./user-guide.md). Als u onlangs een de dienstinstantie creeerde en het nog opleidt en het scoring, gelieve 24 uren voor het te beëindigen loopt.

## Uw gegevensset-id zoeken {#dataset-id}

Klik in uw serviceversie voor Attribution AI-inzichten op de knop *Meer handelingen* vervolgkeuzelijst in de navigatie rechtsboven en selecteer **[!UICONTROL Access scores]**.

![meer acties](./images/download-scores/more-actions.png)

Er wordt een nieuw dialoogvenster weergegeven met een koppeling naar de documentatie van downloadscores en de id van de gegevensset voor uw huidige instantie. Kopieer de id van de gegevensset naar het klembord en ga verder met de volgende stap.

![Dataset-id](../customer-ai/images/download-scores/access-scores.png)

## Batch-id ophalen {#retrieve-your-batch-id}

Gebruikend uw dataset identiteitskaart van de vorige stap, moet u een vraag aan de Catalogus API maken om een partijidentiteitskaart terug te winnen. Voor deze API-aanroep worden aanvullende queryparameters gebruikt om de laatste succesvolle batch te retourneren in plaats van een lijst met batches die bij uw organisatie horen. Als u extra batches wilt retourneren, verhoogt u het aantal voor de optie `limit` de vraagparameter aan de gewenste hoeveelheid u wenst om te zijn teruggekeerd. Voor meer informatie over de types van vraagparameters beschikbaar, bezoek de gids op [catalogusgegevens filteren met behulp van queryparameters](../../catalog/api/filter-data.md).

**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lading die een batch-id-object bevat. In dit voorbeeld is de waarde Key voor het geretourneerde object de batch-id `01E5QSWCAASFQ054FNBKYV6TIQ`. Kopieer de batch-id die u wilt gebruiken in de volgende API-aanroep.

>[!NOTE]
>
> Het volgende antwoord heeft de `tags` object geredigeerd voor leesbaarheid.

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

Als je eenmaal een batch-id hebt, kun je een nieuwe aanvraag indienen bij `/batches`. De aanvraag retourneert een koppeling die wordt gebruikt als de volgende API-aanvraag.

**API-indeling**

```http
GET batches/{BATCH_ID}/files
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BATCH_ID}` | De batch-id die is opgehaald in de vorige stap [batch-id ophalen](#retrieve-your-batch-id). |

**Verzoek**

Voer de volgende aanvraag uit met uw eigen batch-id.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een payload die een `_links` object. Binnen de `_links` object is een `href` met een nieuwe API-aanroep als waarde. Kopieer deze waarde om door te gaan naar de volgende stap.

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

Met de `href` Voer een nieuwe aanvraag in om de bestandsmap op te halen.

**API-indeling**

```http
GET files/{DATASETFILE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASETFILE_ID}` | De id dataSetFile wordt geretourneerd in het dialoogvenster `href` waarde van de [vorige stap](#retrieve-the-next-api-call-with-your-batch-id). Het is ook toegankelijk in `data` array onder het objecttype `dataSetFileId`. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
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


Kopieer de `href` waarde voor elk bestandsobject in het dialoogvenster `data` -array en ga vervolgens verder met de volgende stap.

## Bestandsgegevens downloaden

Als u uw bestandsgegevens wilt downloaden, vraagt u een GET naar de `"href"` waarde die u in de vorige stap hebt gekopieerd [ophalen, bestanden](#retrieving-your-files).

>[!NOTE]
>
>Als u dit verzoek direct in bevellijn doet, zou u kunnen worden ertoe aangezet om een output na uw verzoekkopballen toe te voegen. Het volgende aanvraagvoorbeeld gebruikt `--output {FILENAME.FILETYPE}`.

**API-indeling**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATASETFILE_ID}` | De id dataSetFile wordt geretourneerd in het dialoogvenster `href` waarde van een [vorige stap](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | De naam van het bestand. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Zorg ervoor dat u zich in de juiste map of map bevindt waarnaar u het bestand wilt opslaan voordat u de GET-aanvraag indient.

**Antwoord**

Het antwoord downloadt het bestand dat u in de huidige map hebt aangevraagd. In dit voorbeeld is de bestandsnaam &quot;file.parquet&quot;.

![Terminal](./images/download-scores/terminal-output.png)

De gedownloade scores hebben de Parquet-indeling en hebben een [!DNL Spark]-shell of Parquet reader om de scores te bekijken. Voor weergave met onbewerkte score kunt u [Gereedschappen voor Apache Parquet](https://parquet.apache.org/docs/). Met de parketgereedschappen kunt u de gegevens analyseren met [!DNL Spark].

## Volgende stappen

In dit document worden de stappen beschreven die zijn vereist voor het downloaden van scores van Attribution AI. Ga voor meer informatie over de score naar de [In- en uitvoer van AI](./input-output.md) documentatie.

## Muziek openen met Snowflake

>[!IMPORTANT]
>
>Neem contact op met attributionai-support@adobe.com voor meer informatie over het gebruik van scores via Snowflake.

U hebt toegang tot geaggregeerde Attribution AI-scores via Snowflake. U moet momenteel Adobe-ondersteuning via e-mail verzenden naar attributionai-support@adobe.com om de gegevens voor Snowflake in te stellen en te ontvangen bij uw lezeraccount.

Nadat de Adobe-ondersteuning uw verzoek heeft verwerkt, krijgt u een URL voor het lezeraccount naar Snowflake en de bijbehorende referenties hieronder:

- Snowflake URL
- Gebruikersnaam
- Wachtwoord

>[!NOTE]
>
>De lezeraccount is bedoeld voor het opvragen van gegevens met SQL-clients, werkbladen en BI-oplossingen die JDBC-connector ondersteunen.

Zodra u uw geloofsbrieven en URL hebt, kunt u de modellijsten vragen, die door touchpoint datum, of omzettingsdatum worden bijeengevoegd.

### Schema zoeken in Snowflake

Meld u aan bij Snowflake met de opgegeven referenties. Klik op de knop **Werkbladen** in de hoofdnavigatie linksboven, navigeert u naar de databasemap in het linkerdeelvenster.

![Werkbladen en navigatie](./images/download-scores/edited_snowflake_1.png)

Klik op Volgende **Schema selecteren** in de rechterbovenhoek van het scherm. Bevestig in de pop-up die wordt weergegeven dat u de juiste database hebt geselecteerd. Klik op de knop *Schema* en selecteer een van de vermelde schema&#39;s. U kunt rechtstreeks zoeken vanuit de scoretabellen die onder het geselecteerde schema staan.

![zoeken naar een schema](./images/download-scores/edited_snowflake_2.png)

## PowerBI aansluiten op Snowflake (optioneel)

Met uw Snowflake-referenties kunt u een verbinding tot stand brengen tussen PowerBI Desktop- en Snowflake-databases.

Ten eerste, onder de *Server* typt u de URL van de Snowflake. Volgende, onder *Warehouse*, typt u &quot;XSMALL&quot;. Typ vervolgens uw gebruikersnaam en wachtwoord.

![voorbeeld van POWERBI](./images/download-scores/powerbi-snowflake.png)

Nadat de verbinding tot stand is gebracht, selecteert u de Snowflake-database en selecteert u het gewenste schema. U kunt nu alle tabellen laden.
