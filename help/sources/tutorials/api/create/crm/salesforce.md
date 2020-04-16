---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Salesforce-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: cc999ce1ab426f412c0cc2b69173a336a14024f3

---


# Een Salesforce-connector maken met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Platform te verbinden met een Salesforce-account voor het verzamelen van CRM-gegevens.

Als u het gebruikersinterface in het Platform van de Ervaring liever zou gebruiken, verstrekt de [Dynamica of het Bron Salesforce schakelaar UI leerprogramma](../../../ui/create/crm/dynamics-salesforce.md) geleidelijke instructies voor het uitvoeren van gelijkaardige acties.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om Platform met een rekening van Salesforce met succes te verbinden gebruikend de Dienst API van de Stroom.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met Salesforce te verbinden, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `environmentUrl` | De URL van de Salesforce-broninstantie. |
| `username` | De gebruikersnaam voor de Salesforce-gebruikersaccount. |
| `password` | Het wachtwoord voor de Salesforce-gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de Salesforce-gebruikersaccount. |

Ga voor meer informatie over aan de slag met [dit Salesforce-document](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../../../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief die van de Flow Service, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbindingsspecificaties opzoeken

Voordat u Platform kunt verbinden met een Salesforce-account, moet u controleren of er verbindingsspecificaties bestaan voor Salesforce. Als er geen verbindingsspecificaties bestaan, kan geen verbinding worden gemaakt.

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. U kunt verbindingsspecificaties voor Salesforce opzoeken door een GET verzoek uit te voeren en vraagparameters te gebruiken.

**API-indeling**

Het verzenden van een GET verzoek zonder vraagparameters zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=name=="salesforce"` om informatie specifiek voor Salesforce te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce"
```

**Verzoek**

Het volgende verzoek wint de verbindingsspecificaties voor Salesforce terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name==%22salesforce%22' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de verbindingsspecificaties voor Salesforce, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "name": "salesforce",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
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
            ]
        }
    ]
}
```

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per Salesforce-account is slechts één basisverbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken die verschillende gegevens kunnen inbrengen.

Voer de volgende POST-aanvraag uit om een basisverbinding te maken.

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
        "name": "Salesforce Base Connection",
        "description": "Base connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.username` | De gebruikersnaam die aan uw Salesforce-account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw Salesforce-account is gekoppeld. |
| `auth.params.securityToken` | Het beveiligingstoken dat aan uw Salesforce-account is gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw Salesforce-account die in de vorige stap is opgehaald. |

**Antwoord**

Een geslaagde reactie bevat de unieke id (`id`) van de basisverbinding. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een basisverbinding voor uw Salesforce-account gemaakt met behulp van API&#39;s en is een unieke id opgehaald als onderdeel van de hoofdtekst van de reactie. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert hoe te om de systemen van CRM te [onderzoeken gebruikend de Dienst API](../../explore/crm.md)van de Stroom.