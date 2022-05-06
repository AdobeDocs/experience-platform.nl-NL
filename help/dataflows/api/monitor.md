---
keywords: Experience Platform;huis;populaire onderwerpen;monitordataflows;de stroomdienst api;De Dienst van de stroom
solution: Experience Platform
title: Gegevensstromen controleren met behulp van de Flow Service API
topic-legacy: overview
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het controleren van gegevens voor stroomuitvoering op volledigheid, fouten en metriek met behulp van de Flow Service API.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# Dataflows gebruiken met de Flow Service API

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van [!DNL Platform] diensten. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren. Bovendien, staat het Experience Platform voor gegevens toe om aan externe partners worden geactiveerd.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De dienst verstrekt een gebruikersinterface en RESTful API waarvan alle gesteunde bronnen en bestemmingen verbindbaar zijn.

In deze zelfstudie worden de stappen beschreven voor het controleren van gegevens voor stroomuitvoering op volledigheid, fouten en metriek met behulp van de [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie moet u beschikken over de id-waarde van een geldige gegevensstroom. Als u geen geldige dataflow-id hebt, selecteert u de gewenste connector in het menu [overzicht van bronnen](../../sources/home.md) of [Overzicht van doelen](../../destinations/catalog/overview.md) en voer de stappen uit die zijn beschreven voordat u deze zelfstudie uitvoert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

- [Doelen](../../destinations/home.md): Doelen zijn voorgebouwde integraties met veelgebruikte toepassingen die het mogelijk maken om gegevens van Platform naadloos te activeren voor kanaalmarketingcampagnes, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.
- [Bronnen](../../sources/home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om stroomlooppas met succes te controleren gebruikend [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

- `Content-Type: application/json`

## Monitordoorloopstukken

Zodra u een gegevensstroom hebt gemaakt, voer een verzoek van de GET aan [!DNL Flow Service] API.

**API-indeling**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` waarde voor de gegevensstroom u wilt controleren. |

**Verzoek**

Het volgende verzoek wint de specificaties voor een bestaande gegevensstroom terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert details betreffende uw stroomlooppas, met inbegrip van informatie over zijn aanmaakdatum, bron en doelverbindingen, evenals uniek herkenningsteken van de stroomlooppas (`id`).

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `items` | Bevat één enkele lading meta-gegevens verbonden aan uw specifieke stroomlooppas. |
| `metrics` | De kenmerken van de gegevens in de stroomrun. |
| `activities` | Toont hoe de gegevens worden getransformeerd. |
| `durationSummary` | De begin- en eindtijd van de flow. |
| `sizeSummary` | Het volume van de gegevens in bytes. |
| `recordSummary` | The record count of the data. |
| `fileSummary` | De bestandsaantallen van de gegevens. |
| `fileSummary.extensions` | Bevat informatie die specifiek is voor de activiteit. Bijvoorbeeld: `manifest` maakt slechts deel uit van de &quot;bevorderingsactiviteit&quot; en is daarom opgenomen in de `extensions` object. |
| `statusSummary` | Toont of de stroomlooppas een succes of een mislukking is. |

## Volgende stappen

Door deze zelfstudie te volgen, hebt u metriek en fouteninformatie over uw gegevensstroom teruggewonnen gebruikend [!DNL Flow Service] API. U kunt nu uw gegevensstroom blijven controleren, afhankelijk van uw innameschema, om zijn status en innamesnelheden te volgen. Voor informatie over hoe te om dataflows voor bronnen te controleren, gelieve te lezen [het controleren van gegevensstromen voor bronnen gebruikend het gebruikersinterface](../ui/monitor-sources.md) zelfstudie. Voor meer informatie over hoe te om dataflows voor bestemmingen te controleren, gelieve te lezen [het controleren van gegevensstromen voor bestemmingen die het gebruikersinterface gebruiken](../ui/monitor-destinations.md) zelfstudie.
