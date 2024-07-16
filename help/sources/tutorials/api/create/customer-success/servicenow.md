---
keywords: Experience Platform;thuis;populaire onderwerpen;servicenow;ServiceNow
solution: Experience Platform
title: Creeer een Verbinding van de Basis ServiceNow gebruikend de Dienst API van de Stroom
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een ServiceNow-server met behulp van de Flow Service API.
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Een [!DNL ServiceNow] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Google ServiceNow] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een [!DNL ServiceNow] -server via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL ServiceNow] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de [!DNL ServiceNow] server. |
| `username` | De gebruikersnaam die wordt gebruikt voor verbinding met de [!DNL ServiceNow] -server voor verificatie. |
| `password` | Het wachtwoord waarmee verbinding moet worden gemaakt met de [!DNL ServiceNow] -server voor verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL ServiceNow] is: `eb13cb25-47ab-407f-ba89-c0125281c563` . |

Voor meer informatie over begonnen worden, verwijs naar [ dit document ServiceNow ](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL ServiceNow] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL ServiceNow] gemaakt:

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.server` | Het eindpunt van de [!DNL ServiceNow] -server. |
| `auth.params.username` | De gebruikersnaam die wordt gebruikt voor verbinding met de [!DNL ServiceNow] -server voor verificatie. |
| `auth.params.password` | Het wachtwoord waarmee verbinding moet worden gemaakt met de [!DNL ServiceNow] -server voor verificatie. |
| `connectionSpec.id` | De [!DNL ServiceNow] connection specification ID: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL ServiceNow] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van het klantensucces aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/customer-success.md)
