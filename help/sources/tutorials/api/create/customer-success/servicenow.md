---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een schakelaar ServiceNow gebruikend de Dienst API van de Stroom
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# Een [!DNL ServiceNow] aansluiting maken met de [!DNL Flow Service] API

>[!NOTE]
>De [!DNL ServiceNow] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen om verbinding [!DNL Experience Platform] te maken met een [!DNL ServiceNow] server.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten om verbinding te kunnen maken met een [!DNL ServiceNow] server via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Als u verbinding [!DNL Flow Service] wilt maken met [!DNL ServiceNow], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de [!DNL ServiceNow] server. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de [!DNL ServiceNow] server voor verificatie. |
| `password` | Het wachtwoord om verbinding te maken met de [!DNL ServiceNow] server voor verificatie. |

Voor meer informatie over begonnen worden, verwijs naar [dit document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbindingsspecificaties opzoeken

Om een [!DNL ServiceNow] verbinding tot stand te brengen, moet een reeks [!DNL ServiceNow] verbindingsspecificaties binnen bestaan [!DNL Flow Service]. De eerste stap bij het verbinden [!DNL Platform] met [!DNL ServiceNow] is deze specificaties terug te winnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. Het verzenden van een GET verzoek aan het `/connectionSpecs` eindpunt zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag ook omvatten `property=name=="service-now"` om informatie specifiek voor te verkrijgen [!DNL ServiceNow].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="service-now"
```

**Verzoek**

In het volgende verzoek worden de verbindingsspecificaties opgehaald voor [!DNL ServiceNow].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="service-now"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de verbindingsspecificaties voor [!DNL ServiceNow], inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "name": "service-now",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to ServiceNow server",
                        "properties": {
                            "endpoint": {
                                "type": "string",
                                "description": "The endpoint of the ServiceNow server (http://<instance>.service-now.com)."
                            },
                            "username": {
                                "type": "string",
                                "description": "The user name used to connect to the ServiceNow server for authentication."
                            },
                            "password": {
                                "type": "string",
                                "description": "password to connect to the ServiceNow server for authentication.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "endpoint",
                            "username",
                            "password"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL ServiceNow] account is slechts één basisverbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for service-now",
        "description": "Base connection for service-now,
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

| Eigenschap | Beschrijving |
| ------------- | --------------- |
| `auth.params.server` | Het eindpunt van uw [!DNL ServiceNow] server. |
| `auth.params.username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de [!DNL ServiceNow] server voor verificatie. |
| `auth.params.password` | Het wachtwoord om verbinding te maken met de [!DNL ServiceNow] server voor verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie-id die aan [!DNL ServiceNow]is gekoppeld. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw CRM in de volgende stap te verkennen.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL ServiceNow] basisverbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert hoe te om de systemen van het succes van de klant te [onderzoeken gebruikend de Dienst API](../../explore/customer-success.md)van de Stroom.