---
keywords: Experience Platform;home;popular topics;monitor dataflows;flow service api;Flow Service
solution: Experience Platform
title: Monitorstromen en -uitvoering
topic: overview
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het controleren van gegevens voor stroomuitvoering op volledigheid, fouten en metriek met behulp van de Flow Service API.
translation-type: tm+mt
source-git-commit: 3fb5879ea636d4059a6b42e2f98742ff7df0397c
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Dataflows gebruiken met de Flow Service API

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van [!DNL Platform] services. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren. Bovendien, staat het Experience Platform voor gegevens toe om aan externe partners worden geactiveerd.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De dienst verstrekt een gebruikersinterface en RESTful API waarvan alle gesteunde bronnen en bestemmingen verbindbaar zijn.

In deze zelfstudie worden de stappen beschreven voor het controleren van gegevens over stroomuitvoering op volledigheid, fouten en metriek met de [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)instructies.

## Aan de slag

Voor deze zelfstudie moet u beschikken over de id-waarde van een geldige gegevensstroom. Als u geen geldige dataflow ID hebt, selecteer uw schakelaar van keus van het [bronoverzicht](../../sources/home.md) of [bestemmingsoverzicht](../../destinations/catalog/overview.md) en volg de stappen die alvorens dit leerprogramma te proberen worden geschetst.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

- [Doelen](../../destinations/home.md): Doelen zijn voorgebouwde integraties met veelgebruikte toepassingen die het mogelijk maken om gegevens van Platform naadloos te activeren voor kanaalmarketingcampagnes, e-mailcampagnes, gerichte reclame en vele andere gebruiksgevallen.
- [Bronnen](../../sources/home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om stroomlooppas met succes te controleren gebruikend [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

- `Content-Type: application/json`

## Monitordoorloopstukken

Zodra u een gegevensstroom hebt gemaakt, voer een verzoek van de GET aan [!DNL Flow Service] API uit.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

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
            "imsOrgId": "{IMS_ORG_ID}",
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
| `fileSummary.extensions` | Bevat informatie die specifiek is voor de activiteit. Bijvoorbeeld, `manifest` is slechts een deel van de &quot;Activiteit van de Bevordering&quot;, en daarom is het inbegrepen met het `extensions` voorwerp. |
| `statusSummary` | Toont of de stroomlooppas een succes of een mislukking is. |

## Volgende stappen

Door deze zelfstudie te volgen, hebt u metriek en fouteninformatie over uw gegevensstroom teruggewonnen gebruikend [!DNL Flow Service] API. U kunt nu uw gegevensstroom blijven controleren, afhankelijk van uw innameschema, om zijn status en innamesnelheden te volgen. Voor informatie over hoe te om dataflows voor bronnen te controleren, te lezen gelieve de [controledataflows voor bronnen gebruikend het gebruikersinterfaceleerprogramma](../ui/monitor-sources.md) . Voor meer informatie over hoe te om dataflows voor bestemmingen te controleren, te lezen gelieve de [controledataflows voor bestemmingen gebruikend het gebruikersinterfaceleerprogramma](../ui/monitor-destinations.md) .