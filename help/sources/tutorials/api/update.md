---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;updateaccounts
solution: Experience Platform
title: Accounts bijwerken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het bijwerken van de gegevens en referenties van een account met behulp van de Flow Service API.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# Accounts bijwerken met de Flow Service API

In sommige omstandigheden is het mogelijk dat de details van een bestaande bronverbinding moeten worden bijgewerkt. [!DNL Flow Service] biedt u de mogelijkheid om details van een bestaande batch- of streamingverbinding toe te voegen, te bewerken en te verwijderen, inclusief de naam, beschrijving en gegevens.

In deze zelfstudie worden de stappen beschreven voor het bijwerken van de gegevens en referenties van een verbinding met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie moet u beschikken over een bestaande verbinding en een geldige verbinding-id. Als u geen bestaande verbinding hebt, selecteert u de gewenste bron in het menu [overzicht van bronnen](../../home.md) en voer de stappen uit die zijn beschreven voordat u deze zelfstudie uitvoert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

## Verbindingsdetails opzoeken

De eerste stap bij het bijwerken van uw verbinding is het terugwinnen van zijn details gebruikend uw verbindingsidentiteitskaart Als u de huidige gegevens van uw verbinding wilt ophalen, vraagt u een GET aan de [!DNL Flow Service] API terwijl het verstrekken van verbindings identiteitskaart, van de verbinding u wilt bijwerken.

**API-indeling**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` waarde voor de verbinding u wilt terugwinnen. |

**Verzoek**

Het volgende verzoek wint informatie betreffende uw verbinding terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord geeft de huidige details van uw verbinding met inbegrip van zijn geloofsbrieven, uniek herkenningsteken (`id`) en versie. De versiewaarde is vereist om uw verbinding bij te werken.

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

Als u de naam, beschrijving en referenties van uw verbinding wilt bijwerken, moet u een PATCH-verzoek uitvoeren naar de [!DNL Flow Service] API terwijl het verstrekken van uw verbindingsidentiteitskaart, versie, en de nieuwe informatie u wilt gebruiken.

>[!IMPORTANT]
>
>De `If-Match` header is required when making a PATCH request. De waarde voor deze header is de unieke versie van de verbinding die u wilt bijwerken.

**API-indeling**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` waarde voor de verbinding u wilt bijwerken. |

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
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de verbinding bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een succesvolle reactie retourneert uw verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw verbinding-id opgeeft.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de gegevens en gegevens bijgewerkt die aan uw verbinding zijn gekoppeld met de [!DNL Flow Service] API. Voor meer informatie bij het gebruiken van bronschakelaars, zie [overzicht van bronnen](../../home.md).
