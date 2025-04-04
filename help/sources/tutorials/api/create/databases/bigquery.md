---
title: Google BigQuery met de Flow Service-API verbinden met Experience Platform
description: Leer hoe u Adobe Experience Platform verbindt met Google BigQuery met behulp van de Flow Service API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL Google BigQuery]

>[!IMPORTANT]
>
>De [!DNL Google BigQuery] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze gids om te leren hoe te om uw [!DNL Google BigQuery] gegevensbestand met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

### Vereiste referenties verzamelen

Lees de [[!DNL Google BigQuery]  authentificatiegids ](../../../../connectors/databases/bigquery.md#prerequisites) voor gedetailleerde stappen bij het terugwinnen van uw [!DNL Google BigQuery] geloofsbrieven.

## Verbind [!DNL Google BigQuery] met Experience Platform op Azure {#azure}

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL Google BigQuery] -bron kunt verbinden met Experience Platform on Azure.

### Een basisverbinding maken voor [!DNL Google BigQuery] op Experience Platform in Azure {#azure-base}

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Google BigQuery] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB  Basisauthentificatie van het Gebruik ]

+++verzoek

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Google BigQuery] gemaakt met behulp van basisverificatie.

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

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB  de dienstauthentificatie van het Gebruik ]


+++verzoek

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

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## Verbinding maken [!DNL Google BigQuery] met Experience Platform op Amazon Web Services (AWS) {#aws}

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL Google BigQuery] -database kunt verbinden met Experience Platform op AWS.

### Een basisverbinding maken voor [!DNL Google BigQuery] op Experience Platform op AWS

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../../landing/multi-cloud.md).

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt om [!DNL Google BigQuery] op AWS te verbinden met Experience Platform.

+++Selecteren om voorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.projectId` | De project-id van het standaard [!DNL Google BigQuery] -project waarop moet worden gezocht. tegen. |
| `auth.params.keyFileContent` | Het sleuteldossier dat wordt gebruikt om de de dienstrekening voor authentiek te verklaren. U moet de inhoud van het sleutelbestand coderen in [!DNL Base64] . |
| `auth.params.datasetId` | De gegevensset-id die overeenkomt met uw [!DNL Google BigQuery] -bron. Deze id geeft aan waar de gegevenstabellen zich bevinden. |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw opslag te verkennen in de volgende zelfstudie.

+++Selecteren om voorbeeld weer te geven

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Google BigQuery] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
