---
keywords: Experience Platform;home;populaire onderwerpen;monitor dataflows;flow service api;Flow Service
solution: Experience Platform
title: Gegevensstromen controleren met behulp van de Flow Service API
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het controleren van gegevens voor stroomuitvoering op volledigheid, fouten en metriek met behulp van de Flow Service API.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Dataflows gebruiken met de Flow Service API

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere. Bovendien staat Experience Platform toe dat gegevens worden geactiveerd voor externe partners.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De dienst verstrekt een gebruikersinterface en RESTful API waarvan alle gesteunde bronnen en bestemmingen verbindbaar zijn.

Deze zelfstudie behandelt de stappen voor het controleren van de gegevens van de stroomlooppas voor volledigheid, fouten, en metriek gebruikend [[!DNL Flow Service API] ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie moet u beschikken over de id-waarde van een geldige gegevensstroom. Als u geen geldige dataflow identiteitskaart hebt, selecteer uw schakelaar van keus van het [ overzicht van bronnen ](../../sources/home.md) of [ overzicht van bestemmingen ](../../destinations/catalog/overview.md) en volg de stappen alvorens dit leerprogramma te proberen.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

- [ Doelen ](../../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Experience Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen toestaan.
- [ Bronnen ](../../sources/home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
- [ Sandboxen ](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om stromen met succes te kunnen controleren met behulp van de [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

- `Content-Type: application/json`

## Monitordoorloopstukken

Nadat u een gegevensstroom hebt uitgevoerd, moet u een GET-aanvraag voor de [!DNL Flow Service] API uitvoeren.

**API formaat**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de gegevensstroom die u wilt controleren. |

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

**Reactie**

Een succesvolle reactie keert details betreffende uw stroomlooppas, met inbegrip van informatie over zijn aanmaakdatum, bron en doelverbindingen, evenals uniek herkenningsteken van de stroomlooppas (`id`) terug.

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
| `fileSummary` | Het aantal bestanden van de gegevens. |
| `fileSummary.extensions` | Bevat informatie die specifiek is voor de activiteit. `manifest` maakt bijvoorbeeld slechts deel uit van de promotieactiviteit en is daarom opgenomen in het object `extensions` . |
| `statusSummary` | Toont of de stroomlooppas een succes of een mislukking is. |

## Volgende stappen

Aan de hand van deze zelfstudie hebt u metrische gegevens en foutgegevens over uw gegevensstroom opgehaald met de API [!DNL Flow Service] . U kunt nu uw gegevensstroom blijven controleren, afhankelijk van uw innameschema, om zijn status en innamesnelheden te volgen. Voor informatie over hoe te om dataflows voor bronnen te controleren, te lezen gelieve [ controledataflows voor bronnen gebruikend het gebruikersinterface ](../ui/monitor-sources.md) leerprogramma. Voor meer informatie over hoe te om dataflows voor bestemmingen te controleren, te lezen gelieve [ controledataflows voor bestemmingen gebruikend het gebruikersinterface ](../ui/monitor-destinations.md) leerprogramma.
