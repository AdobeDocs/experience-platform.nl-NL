---
title: Een Google BigQuery Base-verbinding maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Google BigQuery met behulp van de Flow Service API.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Een [!DNL Google BigQuery] basisverbinding maken met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De [!DNL Google BigQuery] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees deze gids om te leren hoe te om een basisverbinding voor [!DNL Google BigQuery] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Google BigQuery] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Lees de [[!DNL Google BigQuery]  authentificatiegids ](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) voor gedetailleerde stappen bij het verzamelen van uw vereiste geloofsbrieven.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Google BigQuery] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB  Basisauthentificatie van het Gebruik ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Google BigQuery] gemaakt met behulp van basisverificatie:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.project` | De project-id van het standaard [!DNL Google BigQuery] -project waarop moet worden gezocht. tegen. |
| `auth.params.clientId` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `auth.params.clientSecret` | De clientwaarde die wordt gebruikt om het vernieuwingstoken te genereren. |
| `auth.params.refreshToken` | Het vernieuwingstoken dat u van [!DNL Google] hebt gekregen om toegang tot [!DNL Google BigQuery] te verlenen. |
| `connectionSpec.id` | The [!DNL Google BigQuery] connection specification ID: `3c9b37f8-13a6-43d8-bad3-b863b941fedd` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!TAB  de dienstauthentificatie van het Gebruik ]


**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Google BigQuery] gemaakt met behulp van service-verificatie:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery base connection with service account",
        "description": "Google BigQuery connection with service account",
        "auth": {
            "specName": "Service Authentication",
            "params": {
                    "projectId": "{PROJECT_ID}",
                    "keyFileContent": "{KEY_FILE_CONTENT},
                    "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.projectId` | De project-id van het standaard [!DNL Google BigQuery] -project waarop moet worden gezocht. tegen. |
| `auth.params.keyFileContent` | Het sleuteldossier dat wordt gebruikt om de de dienstrekening voor authentiek te verklaren. U moet de inhoud van het sleutelbestand coderen in [!DNL Base64] . |
| `auth.params.largeResultsDataSetId` | (Optioneel) De vooraf gemaakte [!DNL Google BigQuery] dataset-id die vereist is om ondersteuning voor grote resultaatsets mogelijk te maken. |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

>[!ENDTABS]


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Google BigQuery] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
