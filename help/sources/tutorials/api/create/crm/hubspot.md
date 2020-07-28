---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een schakelaar HubSpot gebruikend de Dienst API van de Stroom
topic: overview
translation-type: tm+mt
source-git-commit: 5839e4695589455bd32b6e3e33a7c377343f920d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Een [!DNL HubSpot] aansluiting maken met de [!DNL Flow Service] API

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen waarmee u verbinding [!DNL Experience Platform] kunt maken [!DNL HubSpot].

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL HubSpot] [!DNL Flow Service] de API.

### Vereiste referenties verzamelen

Als u verbinding wilt [!DNL Flow Service] maken met [!DNL HubSpot], moet u de volgende verbindingseigenschappen opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientId` | De client-id die aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| `clientSecret` | Het clientgeheim dat aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| `accessToken` | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |

Voor meer informatie over begonnen worden, verwijs naar dit [document](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)HubSpot.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot de [!DNL Flow Service]sandboxen behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Verbindingsspecificaties opzoeken

Om een [!DNL HubSpot] verbinding tot stand te brengen, moet een reeks [!DNL HubSpot] verbindingsspecificaties binnen bestaan [!DNL Flow Service]. De eerste stap bij het verbinden [!DNL Platform] met [!DNL HubSpot] is deze specificaties terug te winnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. Het verzenden van een verzoek van de GET naar het `/connectionSpecs` eindpunt zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag ook omvatten `property=name=="hubspot"` om informatie specifiek voor te verkrijgen [!DNL HubSpot].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="hubspot"
```

**Verzoek**

In het volgende verzoek worden de verbindingsspecificaties opgehaald voor [!DNL HubSpot].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="hubspot"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de verbindingsspecificatie voor [!DNL HubSpot], inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een verbinding voor de API te maken.

```json
{
    "items": [
        {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "name": "hubspot",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to HubSpot",
                        "properties": {
                            "clientId": {
                                "type": "string",
                                "description": "The client ID associated with your HubSpot application."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret associated with your HubSpot application.",
                                "format": "password"
                            },
                            "accessToken": {
                                "type": "string",
                                "description": "The access token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientId",
                            "clientSecret",
                            "accessToken",
                            "refreshToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Verbinding maken voor de API

Een verbinding voor API specificeert een bronnen en bevat uw geloofsbrieven voor die bron. Per [!DNL HubSpot] account is slechts één verbinding voor de API vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het opnemen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.clientId` | De client-id die aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| `auth.params.accessToken` | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `auth.params.refreshToken` | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding voor de API, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2eb9c78b-e8b8-4400-b9c7-8be8b86400b2",
    "etag": "\"05026cf5-0000-0200-0000-5e4c42920000\""
}
```

Als u deze zelfstudie volgt, hebt u een [!DNL HubSpot] verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsidentiteitskaart in de volgende zelfstudie gebruiken aangezien u leert hoe te om de systemen van CRM te [onderzoeken gebruikend de Dienst API](../../explore/crm.md)van de Stroom.