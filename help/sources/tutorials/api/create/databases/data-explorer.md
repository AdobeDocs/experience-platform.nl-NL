---
keywords: Experience Platform;home;populaire onderwerpen;Azure Azure Data Explorer;Azure Data Explorer;Azure Data Explorer
solution: Experience Platform
title: Een Azure Azure Data Explorer Base Connection maken met de Flow Service API
type: Tutorial
description: Leer hoe u Azure Data Explorer aan Adobe Experience Platform koppelt met behulp van de Flow Service API.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Een [!DNL Azure Azure Data Explorer] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Azure Data Explorer] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Azure Data Explorer] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Azure Data Explorer] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de [!DNL Azure Data Explorer] server. |
| `database` | De naam van de [!DNL Azure Data Explorer] -database. |
| `tenant` | De unieke huurder-id die wordt gebruikt om verbinding te maken met de [!DNL Azure Data Explorer] -database. |
| `servicePrincipalId` | De unieke service principal-id die wordt gebruikt om verbinding te maken met de [!DNL Azure Data Explorer] -database. |
| `servicePrincipalKey` | De unieke service principal-sleutel die wordt gebruikt om verbinding te maken met de [!DNL Azure Data Explorer] -database. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Azure Data Explorer] is `0479cc14-7651-4354-b233-7480606c2ac3` . |

Voor meer informatie over begonnen worden verwijs naar dit [[!DNL Azure Data Explorer]  document ](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Azure Data Explorer] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Azure Data Explorer] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.endpoint` | Het eindpunt van de [!DNL Azure Data Explorer] server. |
| `auth.params.database` | De naam van de [!DNL Azure Data Explorer] -database. |
| `auth.params.tenant` | De unieke huurder-id die wordt gebruikt om verbinding te maken met de [!DNL Azure Data Explorer] -database. |
| `auth.params.servicePrincipalId` | De unieke service principal-id die wordt gebruikt om verbinding te maken met de [!DNL Azure Data Explorer] -database. |
| `auth.params.servicePrincipalKey` | De unieke service principal-sleutel die wordt gebruikt om verbinding te maken met de [!DNL Azure Data Explorer] -database. |
| `connectionSpec.id` | The [!DNL Azure Data Explorer] connection specification ID: `0479cc14-7651-4354-b233-7480606c2ac3` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Azure Data Explorer] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
