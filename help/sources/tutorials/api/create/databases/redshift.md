---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Amazon Redshift-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# Een Amazon Redshift-connector maken met de Flow Service API

>[!NOTE]
>De Amazon Redshift-connector bevindt zich in bèta. De functies en documentatie kunnen worden gewijzigd.

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om het Experience Platform te verbinden met Amazon Redshift (hierna &quot;Redshift&quot; genoemd).

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met Redshift met de Flow Service API.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met Redshift te verbinden, moet u de volgende verbindingseigenschappen verstrekken:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| `server` | De server die aan uw Redshift-account is gekoppeld. |
| `username` | De gebruikersnaam die aan uw Redshift-account is gekoppeld. |
| `password` | Het wachtwoord dat aan uw Redshift-account is gekoppeld. |
| `database` | De database voor opnieuw plaatsen die u opent. |

Raadpleeg [dit document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)voor opnieuw toewijzen voor meer informatie over aan de slag gaan.

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

Als u een verbinding voor opnieuw verschuiven wilt maken, moet er een reeks verbindingsspecificaties voor opnieuw verschuiven bestaan binnen Flow Service. De eerste stap in het verbinden van Platform aan Redshift is deze specificaties terug te winnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. U kunt verbindingsspecificaties voor Redshift opzoeken door een GET verzoek uit te voeren en vraagparameters te gebruiken.

Het verzenden van een GET verzoek zonder vraagparameters zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=name=="amazon-redshift"` om informatie specifiek voor Redshift te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="amazon-redshift"
```

**Verzoek**

Met het volgende verzoek worden de verbindingsspecificaties voor Redshift opgehaald.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="amazon-redshift"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de verbindingsspecificaties voor Redshift, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "name": "amazon-redshift",
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
                            "server": {
                                "type": "string",
                                "description": "IP address or host name of the Amazon Redshift server"
                            },
                            "username": {
                                "type": "string",
                                "description": "Name of user who has access to the database"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "database": {
                                "type": "string",
                                "description": "Name of the Amazon Redshift database"
                            }
                        },
                        "required": [
                            "server",
                            "username",
                            "password",
                            "database"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één basisverbinding vereist per Redshift-account omdat deze kan worden gebruikt om meerdere bronconnectors te maken om verschillende gegevens in te voeren.

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
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| ------------- | --------------- |
| `auth.params.server` | Uw Redshift-server. |
| `auth.params.database` | De database die aan uw Redshift-account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw Redshift-account is gekoppeld. |
| `auth.params.username` | De gebruikersnaam die aan uw Redshift-account is gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw Redshift-account die in de vorige stap is opgehaald. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een Redshift basisverbinding tot stand gebracht gebruikend de Dienst API van de Stroom, en hebt u de unieke waarde van identiteitskaart van de verbinding verkregen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert om gegevensbestanden of systemen te [onderzoeken NoSQL gebruikend de Dienst API](../../explore/database-nosql.md)van de Stroom.
