---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;updateaccounts
solution: Experience Platform
title: Accounts bijwerken met de Flow Service API
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het bijwerken van de gegevens en referenties van een account met behulp van de Flow Service API.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Accounts bijwerken met de Flow Service API

In sommige omstandigheden is het mogelijk dat de details van een bestaande bronverbinding moeten worden bijgewerkt. [!DNL Flow Service] biedt u de mogelijkheid om details van een bestaande batch- of streamingverbinding toe te voegen, te bewerken en te verwijderen, inclusief de naam, beschrijving en gegevens.

Dit leerprogramma behandelt de stappen voor het bijwerken van de details en de geloofsbrieven van een verbinding gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie moet u beschikken over een bestaande verbinding en een geldige verbinding-id. Als u geen bestaande verbinding hebt, selecteer uw bron van keus van het [ overzicht van bronnen ](../../home.md) en volg de stappen die alvorens dit leerprogramma te proberen worden geschetst.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).

## Verbindingsdetails opzoeken

De eerste stap bij het bijwerken van uw verbinding is het terugwinnen van zijn details gebruikend uw verbindingsidentiteitskaart Als u de huidige gegevens van uw verbinding wilt ophalen, vraagt u de GET aan de [!DNL Flow Service] API terwijl u de verbinding-id opgeeft, van de verbinding die u wilt bijwerken.

**API formaat**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` -waarde voor de verbinding die u wilt ophalen. |

**Verzoek**

Met het volgende verzoek wordt informatie over uw verbinding opgehaald.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de huidige details van uw verbinding met inbegrip van zijn geloofsbrieven, unieke herkenningsteken (`id`), en versie terug. De versiewaarde is vereist om uw verbinding bij te werken.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Verbinding bijwerken

Als u de naam, beschrijving en referenties van uw verbinding wilt bijwerken, voert u een PATCH-aanvraag uit naar de API van [!DNL Flow Service] en geeft u uw verbinding-id, versie en de nieuwe informatie op die u wilt gebruiken.

>[!IMPORTANT]
>
>De header `If-Match` is vereist wanneer een PATCH-aanvraag wordt ingediend. De waarde voor deze header is de unieke versie van de verbinding die u wilt bijwerken.

**API formaat**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` waarde voor de verbinding die u wilt bijwerken. |

**Verzoek**

De volgende aanvraag bevat een nieuwe naam en beschrijving, plus een nieuwe set referenties waarmee u de verbinding kunt bijwerken.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de verbinding bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een succesvolle reactie retourneert uw verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een aanvraag voor een GET in te dienen bij de [!DNL Flow Service] API en tegelijk uw verbinding-id op te geven.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de referenties en informatie bijgewerkt die aan uw verbinding zijn gekoppeld met de API van [!DNL Flow Service] . Voor meer informatie bij het gebruiken van bronschakelaars, zie het [ overzicht van bronnen ](../../home.md).
