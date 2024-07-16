---
keywords: Experience Platform;thuis;populaire onderwerpen;veeva crm;Veeva CRM;Veeva CRM;
solution: Experience Platform
title: Een Veeva CRM-basisverbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met Veeva CRM met behulp van de Flow Service API.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Een [!DNL Veeva CRM] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Veeva CRM] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met [!DNL Veeva CRM] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Veeva CRM] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `environmentUrl` | De URL van de instantie [!DNL Veeva CRM] . |
| `username` | De gebruikersnaam van uw [!DNL Veeva CRM] -account. |
| `password` | De wachtwoordwaarde van uw [!DNL Veeva CRM] -account. |
| `securityToken` | Het beveiligingstoken voor uw [!DNL Veeva CRM] -instantie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Veeva CRM] is: `fcad62f3-09b0-41d3-be11-449d5a621b69` . |

Voor meer informatie over deze waarden, verwijs naar dit [[!DNL Veeva CRM]  document ](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Veeva CRM] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Veeva CRM] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De naam van uw [!DNL Veeva CRM] basisverbinding. U kunt deze naam gebruiken om uw [!DNL Veeva CRM] basisverbinding te zoeken. |
| `description` | Een optionele beschrijving voor uw [!DNL Veeva CRM] basisverbinding. |
| `auth.specName` | Het verificatietype dat voor de verbinding wordt gebruikt. |
| `auth.params.environmentUrl` | De URL van de instantie [!DNL Veeva CRM] . |
| `auth.params.username` | De gebruikersnaam van uw [!DNL Veeva CRM] -account. |
| `auth.params.password` | De wachtwoordwaarde van uw [!DNL Veeva CRM] -account. |
| `auth.params.securityToken` | Het beveiligingstoken voor uw [!DNL Veeva CRM] -instantie. |
| `connectionSpec.id` | De verbindingsspecificatie-id voor [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Veeva CRM] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van CRM aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/crm.md)
