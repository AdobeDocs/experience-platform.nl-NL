---
keywords: Experience Platform;thuis;populaire onderwerpen; stroomvoorziening; updateverbindingen
solution: Experience Platform
title: Verbindingsgegevens bijwerken met de Flow Service API
topic: overview
type: Tutorial
description: In sommige omstandigheden is het mogelijk dat de details van een bestaande bronverbinding moeten worden bijgewerkt. De Flow Service API biedt u de mogelijkheid om details van een bestaande batch- of streamingverbinding toe te voegen, te bewerken en te verwijderen, inclusief de naam, beschrijving en referenties.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---


# Verbindingsgegevens bijwerken met de Flow Service API

In sommige omstandigheden is het mogelijk dat de details van een bestaande bronverbinding moeten worden bijgewerkt. [!DNL Flow Service] biedt u de mogelijkheid om details van een bestaande batch- of streamingverbinding toe te voegen, te bewerken en te verwijderen, inclusief de naam, beschrijving en gegevens.

Deze zelfstudie behandelt de stappen voor het bijwerken van de details en geloofsbrieven van een bestaande verbinding gebruikend [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Voor deze zelfstudie moet u een geldige verbinding-id hebben. Als u geen geldige verbindingsID hebt, selecteer uw schakelaar van keus van [bronnen overzicht](../../home.md) en volg de stappen geschetst alvorens dit leerprogramma te proberen.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten om de verbindingsgegevens met de API [!DNL Flow Service] te kunnen bijwerken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Verbindingsdetails opzoeken

>[!NOTE]
>Deze zelfstudie gebruikt als voorbeeld de [Salesforce-bronconnector](../../connectors/crm/salesforce.md), maar de stappen die worden beschreven, zijn van toepassing op elk van de [beschikbare bronconnectors](../../home.md).

De eerste stap bij het bijwerken van uw verbindingsgegevens is het ophalen van verbindingsgegevens met behulp van uw verbindings-id.

**API-indeling**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id`-waarde voor de verbinding die u wilt ophalen. |

**Verzoek**

In het volgende voorbeeld wordt informatie over uw verbinding-id opgehaald.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de huidige details van uw verbinding met inbegrip van zijn geloofsbrieven, uniek herkenningsteken (`id`), en versie terug.

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

Zodra u een bestaande verbindingsidentiteitskaart hebt, voer een verzoek van PATCH aan [!DNL Flow Service] API uit.

>[!IMPORTANT]
>Een verzoek van PATCH vereist het gebruik van `If-Match` kopbal. De waarde voor deze header is de unieke versie van uw verbinding.

**API-indeling**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id`-waarde voor de verbinding die u wilt bijwerken. |

**Verzoek**

Het volgende verzoek bevat nieuwe informatie waarmee u uw verbinding kunt bijwerken.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om de verbinding bij te werken. Bewerkingen omvatten: `add`, `replace` en `remove`. |
| `path` | Het pad van de parameter die moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een succesvolle reactie retourneert uw verbindings-id en een bijgewerkt label.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Bijgewerkte verbindingsdetails opzoeken

U kunt de zelfde verbindings identiteitskaart terugwinnen u bijwerkte om de veranderingen te zien u door een verzoek van de GET aan [!DNL Flow Service] API aanbracht.

**API-indeling**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id`-waarde voor de verbinding die u wilt ophalen. |

**Verzoek**

Met het volgende verzoek wordt bijgewerkte informatie over uw verbinding-id opgehaald.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de bijgewerkte details van de verbindings-id, inclusief de nieuwe naam, beschrijving en versie.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1598038319627,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "Test salesforce connection",
            "description": "A test salesforce connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{NEW_SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "salesforce-connector-username"
                }
            },
            "version": "\"3600e378-0000-0200-0000-5f40212f0000\"",
            "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
        }
    ]
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de geloofsbrieven en de informatie verbonden aan uw verbinding bijgewerkt gebruikend [!DNL Flow Service] API. Voor meer informatie bij het gebruiken van bronschakelaars, zie [bronnen overzicht](../../home.md).
