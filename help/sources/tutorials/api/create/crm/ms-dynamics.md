---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Microsoft Dynamics-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 72c1d53295d5c4204c02959c857edc06f246534c
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---


# Een Microsoft Dynamics-connector maken met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Dit leerprogramma gebruikt de Dienst API van de Stroom om u door de stappen te lopen om Platform met een rekening van de Dynamiek van Microsoft (verder als &quot;Dynamica&quot;wordt bedoeld) te verbinden voor het verzamelen van de gegevens van CRM.

Als u de gebruikersinterface in het Platform van de Ervaring liever zou gebruiken, verstrekt de UI-zelfstudie [van de bron van de](../../../ui/create/crm/dynamics.md) Dynamica geleidelijke instructies voor het uitvoeren van gelijkaardige acties.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om Platform met een rekening van de Dynamiek met succes te verbinden gebruikend de Dienst API van de Stroom.

### Vereiste referenties verzamelen

Opdat de Dienst van de Stroom met Dynamica verbindt, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUri` | De service-URL van uw instantie Dynamics. |
| `username` | De gebruikersnaam voor uw gebruikersaccount voor dynamiek. |
| `password` | Het wachtwoord voor uw rekening van de Dynamiek. |

Voor meer informatie over aan de slag gaan, bezoek [dit document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)van de Dynamiek.

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

Alvorens Platform met een rekening van de Dynamiek aan te sluiten, moet u verifiëren dat de verbindingsspecificaties voor Dynamiek bestaan. Als er geen verbindingsspecificaties bestaan, kan geen verbinding worden gemaakt.

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. U kunt verbindingsspecificaties voor Dynamica opzoeken door een GET verzoek uit te voeren en vraagparameters te gebruiken.

**API-indeling**

Het verzenden van een GET verzoek zonder vraagparameters zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=name=="dynamics-online"` om informatie specifiek voor Dynamica te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**Verzoek**

Het volgende verzoek wint de verbindingsspecificaties voor Dynamica terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de verbindingsspecificaties voor Dynamiek, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een basisverbinding te maken.

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

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per rekening van de Dynamiek wordt slechts één basisverbinding vereist aangezien het kan worden gebruikt om veelvoudige bronschakelaars tot stand te brengen om verschillende gegevens in te brengen.

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
| `auth.params.serviceUri` | De dienst URI verbonden aan uw instantie van de Dynamiek. |
| `auth.params.username` | De gebruikersnaam die aan uw rekening van de Dynamiek wordt gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw rekening van de Dynamiek wordt gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw rekening van de Dynamiek die in de vorige stap wordt teruggewonnen. |

**Antwoord**

Een geslaagde reactie bevat de unieke id (`id`) van de basisverbinding. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een basisverbinding voor uw rekening van de Dynamiek gecreeerd gebruikend APIs en unieke identiteitskaart werd verkregen als deel van het reactievermogen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert hoe te om de systemen van CRM te [onderzoeken gebruikend de Dienst API](../../explore/crm.md)van de Stroom.