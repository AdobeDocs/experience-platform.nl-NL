---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Maak een SQL Server-aansluiting met behulp van de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 173faf861ca8feb6dd4e2159b0708e41fa0f601f

---


# Een Microsoft SQL Server-connector maken met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Dit leerprogramma gebruikt de Dienst API van de Stroom om u door de stappen te lopen om het Platform van de Ervaring met een Server van Microsoft te verbinden SQL (verder die als &quot;SQL Server&quot;wordt bedoeld).

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met SQL Server te verbinden gebruikend de Dienst API van de Stroom.

### Vereiste referenties verzamelen

Om met SQL Server te verbinden, moet u het volgende verbindingsbezit verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die is gekoppeld aan uw SQL Server-account. |

Gelieve te verwijzen naar [dit document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) voor meer informatie over het worden begonnen met SQL Server.

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

Om een SQL verbinding van de Server tot stand te brengen, moet een reeks SQL de verbindingsspecificaties van de Server binnen de Dienst van de Stroom bestaan. De eerste stap in het verbinden van Platform met SQL Server moet deze specificaties terugwinnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. Het verzenden van een GET verzoek aan het `/connectionSpecs` eindpunt zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag ook omvatten `property=name=="sql-server"` om informatie specifiek voor SQL Server te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="sql-server"
```

**Verzoek**

Het volgende verzoek wint de verbindingsspecificaties voor SQL Server terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="sql-server"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de verbindingsspecificaties voor SQL Server, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "name": "sql-server",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Connection String Based Authentication",
                    "type": "connectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to SQL Server database",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "connection string to connect to any SQL Server database.",
                                "format": "password",
                                "pattern": "^(Data Source=)(.*)(;Initial Catalog=)(.*)(;Integrated Security=)(.*)(;User ID=)(.*)(;Password=)(.*)(;)",
                                "examples": [
                                    "Data Source=<servername>\\<instance name if using named instance>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;"
                                ]
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Slechts één basisverbinding wordt vereist per SQL rekening van de Server aangezien het kan worden gebruikt om veelvoudige bronschakelaars tot stand te brengen om verschillende gegevens in te brengen.

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
        "name": "Base connection for sql-server",
        "description": "Base connection for sql-server",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw SQL Server-verificatie is gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie (`id`) die in de vorige stap wordt verzameld. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een SQL het basisverbinding van de Server gebruikend de Dienst API van de Stroom gecreeerd, en hebt de unieke waarde van identiteitskaart van de verbinding verkregen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert om gegevensbestanden of systemen te [onderzoeken NoSQL gebruikend de Dienst API](../../explore/database-nosql.md)van de Stroom.
