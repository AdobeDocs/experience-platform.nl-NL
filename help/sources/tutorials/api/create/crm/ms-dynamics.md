---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Een Microsoft Dynamics-connector maken met de Flow Service API
topic: overview
type: Tutorial
description: Dit leerprogramma gebruikt de Dienst API van de Stroom om u door de stappen te lopen om Platform met een rekening van de Dynamiek van Microsoft (verder als "Dynamica") te verbinden voor het verzamelen van de gegevens van CRM.
translation-type: tm+mt
source-git-commit: d332226541685108b58d88096146ed6048606774
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Een [!DNL Microsoft Dynamics] aansluiting maken met de [!DNL Flow Service] API

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de [!DNL Flow Service] API gebruikt om u door de stappen te laten lopen om verbinding [!DNL Platform] te maken met een [!DNL Microsoft Dynamics] (hierna &quot;Dynamics&quot; genoemd) account voor het verzamelen van CRM-gegevens.

Als u het gebruikersinterface binnen liever zou gebruiken [!DNL Experience Platform], verstrekt de het bronschakelaarUI van de [Dynamica leerprogramma](../../../ui/create/crm/dynamics.md) geleidelijke instructies voor het uitvoeren van gelijkaardige acties.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): E[!DNL xperience Platform] biedt virtuele sandboxen die één [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes [!DNL Platform] met een rekening van de Dynamiek te verbinden gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Als u verbinding [!DNL Flow Service] wilt maken met [!DNL Dynamics], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] account. |

Voor meer informatie over aan de slag gaan, bezoek [dit document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)van de Dynamiek.

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

Voordat u verbinding maakt [!DNL Platform] met een [!DNL Dynamics] account, moet u controleren of er verbindingsspecificaties bestaan voor [!DNL Dynamics]. Als er geen verbindingsspecificaties bestaan, kan geen verbinding worden gemaakt.

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. U kunt verbindingsspecificaties voor opzoeken [!DNL Dynamics] door een verzoek van de GET uit te voeren en vraagparameters te gebruiken.

**API-indeling**

Het verzenden van een verzoek van de GET zonder vraagparameters zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=name=="dynamics-online"` om informatie specifiek voor te verkrijgen [!DNL Dynamics].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Verzoek**

In het volgende verzoek worden de verbindingsspecificaties opgehaald voor [!DNL Dynamics].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de verbindingsspecificaties voor [!DNL Dynamics], inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Verbinding maken voor de API

Een verbinding voor API specificeert een bronnen en bevat uw geloofsbrieven voor die bron. Per [!DNL Dynamics] account is slechts één verbinding voor de API vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het opnemen van verschillende gegevens.

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
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.serviceUri` | De service-URI die aan uw [!DNL Dynamics] instantie is gekoppeld. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Dynamics] account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Dynamics] account is gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw [!DNL Dynamics] account die in de vorige stap is opgehaald. |

**Antwoord**

Een geslaagde reactie bevat de unieke id (`id`) van de basisverbinding. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding voor uw [!DNL Dynamics] account gemaakt met behulp van API&#39;s en is een unieke id verkregen als onderdeel van de hoofdtekst van de reactie. U kunt deze verbindingsidentiteitskaart in de volgende zelfstudie gebruiken aangezien u leert hoe te om de systemen van CRM te [onderzoeken gebruikend de Dienst API](../../explore/crm.md)van de Stroom.