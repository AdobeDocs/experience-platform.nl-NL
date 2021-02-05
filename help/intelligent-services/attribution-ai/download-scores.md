---
keywords: Experience Platform;attributie ai;access scores;populaire onderwerpen;download scores;attributie ai scores;export;Export
solution: Experience Platform, Intelligent Services
title: Scores downloaden in Attribution AI
topic: Downloading scores
description: Dit document dient als richtlijn voor het downloaden van scores voor Attribution AI.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---


# Muziek downloaden in Attribution AI

Dit document dient als richtlijn voor het downloaden van scores voor Attribution AI.

## Aan de slag

Met Attribution AI kunt u scores downloaden in de Parquet-bestandsindeling. Deze zelfstudie vereist dat u de sectie met downloadscores in de [Aan de slag](./getting-started.md)-handleiding hebt gelezen en voltooid.

Bovendien, om tot scores voor Attribution AI toegang te hebben, moet u een de dienstinstantie hebben met een succesvolle looppasstatus beschikbaar. Als u een nieuwe service-instantie wilt maken, gaat u naar de [Gebruikershandleiding voor Attribution AI](./user-guide.md). Als u onlangs een de dienstinstantie creeerde en het nog opleidt en het scoring, gelieve 24 uren voor het te beëindigen loopt.

## Uw gegevensset-id {#dataset-id} zoeken

Binnen uw de dienstinstantie voor Attribution AI inzichten, klik *Meer acties* dropdown in de top-juiste navigatie dan selecteren **[!UICONTROL de scores van de Toegang]**.

![meer acties](./images/download-scores/more-actions.png)

Er wordt een nieuw dialoogvenster weergegeven met een koppeling naar de documentatie van downloadscores en de id van de gegevensset voor uw huidige instantie. Kopieer de id van de gegevensset naar het klembord en ga verder met de volgende stap.

![Dataset-id](../customer-ai/images/download-scores/access-scores.png)

## De batch-id {#retrieve-your-batch-id} ophalen

Gebruikend uw dataset identiteitskaart van de vorige stap, moet u een vraag aan de Catalogus API maken om een partijidentiteitskaart terug te winnen. Voor deze API-aanroep worden aanvullende queryparameters gebruikt om de laatste succesvolle batch te retourneren in plaats van een lijst met batches die bij uw organisatie horen. Om extra partijen terug te keren, verhoog het aantal voor de `limit` vraagparameter tot de gewenste hoeveelheid u wenst om te zijn teruggekeerd. Voor meer informatie over de types van vraagparameters beschikbaar, bezoek de gids over [het filtreren van de gegevens van de Catalogus gebruikend vraagparameters](../../catalog/api/filter-data.md).

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

Een geslaagde reactie retourneert een lading die een batch-id-object bevat. In dit voorbeeld is de waarde Key aan het geretourneerde object de batch-id `01E5QSWCAASFQ054FNBKYV6TIQ`. Kopieer de batch-id die u wilt gebruiken in de volgende API-aanroep.

>[!NOTE]
>
> In de volgende reactie is het object `tags` gereed voor leesbaarheid.

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
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
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

De gedownloade scores hebben de Parquet-indeling en hebben een [!DNL Spark]-shell of een Parquet-lezer nodig om de scores weer te geven. Voor het bekijken van onbewerkte scores kunt u [Apache Parquet-gereedschappen](https://github.com/apache/parquet-mr/tree/master/parquet-tools) gebruiken. Met de gereedschappen Parquet kunt u de gegevens analyseren met [!DNL Spark].

## Volgende stappen

In dit document worden de stappen beschreven die zijn vereist voor het downloaden van scores van Attribution AI. Voor meer informatie over de score gaat u naar de [documentatie voor AIR-invoer en -uitvoer](./input-output.md).

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

Meld u aan bij Snowflake met de opgegeven referenties. Klik op het tabblad **Werkbladen** in de hoofdnavigatie linksboven en navigeer naar de databasemap in het linkerdeelvenster.

![Werkbladen en navigatie](./images/download-scores/edited_snowflake_1.png)

Klik vervolgens op **Schema** in de rechterbovenhoek van het scherm. Bevestig in de pop-up die wordt weergegeven dat u de juiste database hebt geselecteerd. Klik vervolgens op het vervolgkeuzemenu *Schema* en selecteer een van de weergegeven schema&#39;s. U kunt rechtstreeks zoeken vanuit de scoretabellen die onder het geselecteerde schema staan.

![zoeken naar een schema](./images/download-scores/edited_snowflake_2.png)

## PowerBI aansluiten op Snowflake (optioneel)

Met uw Snowflake-referenties kunt u een verbinding tot stand brengen tussen PowerBI Desktop- en Snowflake-databases.

Typ eerst onder het vak *Server* de URL van de Snowflake. Typ vervolgens onder *Winkel* &quot;XSMALL&quot;. Typ vervolgens uw gebruikersnaam en wachtwoord.

![voorbeeld van POWERBI](./images/download-scores/powerbi-snowflake.png)

Nadat de verbinding tot stand is gebracht, selecteert u de Snowflake-database en selecteert u het gewenste schema. U kunt nu alle tabellen laden.
