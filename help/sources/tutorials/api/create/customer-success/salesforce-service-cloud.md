---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Salesforce Service Cloud-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: cada7c7eff7597015caa7333559bef16a59eab65
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Een Salesforce Service Cloud-connector maken met de Flow Service API

>[!NOTE]
>De Salesforce Service Cloud-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De Dienst van de stroom wordt gebruikt om klantengegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform te verbinden met de Salesforce Service Cloud (hierna &quot;SSC&quot; genoemd).

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met SSC te verbinden gebruikend de Dienst API van de Stroom.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met SSC te verbinden, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `username` | De gebruikersnaam voor de gebruikersaccount. |
| `password` | Het wachtwoord voor de gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de gebruikersaccount. |

Raadpleeg [dit document](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)van de Salesforce Service Cloud voor meer informatie over aan de slag gaan.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u eerst het [authentificatieleerprogramma](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform, inclusief die van Flow Service, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbindingsspecificaties opzoeken

Om een verbinding tot stand te brengen SSC, moet een reeks SSC verbindingsspecificaties binnen de Dienst van de Stroom bestaan. De eerste stap in het verbinden van Platform met SSC is deze specificaties terug te winnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. Het verzenden van een GET verzoek aan het `/connectionSpecs` eindpunt zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag ook omvatten `property=name=="salesforce-service-cloud"` om informatie specifiek voor SSC te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce-service-cloud"
```

**Verzoek**

Het volgende verzoek wint de verbindingsspecificatie voor SSC terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de verbindingsspecificaties voor SSC, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap voor het maken van een basisverbinding.

```json
{
    "items": [
        {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "name": "salesforce-service-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "BasicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per SSC-account is slechts één basisverbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken die verschillende gegevens kunnen inbrengen.

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
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.username` | De gebruikersnaam die aan uw SSC-account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat is gekoppeld aan uw SSC-account. |
| `auth.params.securityToken` | Het beveiligingstoken dat aan uw SSC-account is gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw rekening SSC die in de vorige stap wordt teruggewonnen. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een SSC-basisverbinding gemaakt met de Flow Service API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert hoe te om de systemen van het succes van de klant te [onderzoeken gebruikend de Dienst API](../../explore/customer-success.md)van de Stroom.
