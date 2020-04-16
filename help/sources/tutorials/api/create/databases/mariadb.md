---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een MariaDB-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 540e419230cd516a258d39947d6b07c1e8b115c7

---


# Een MariaDB-connector maken met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om het Platform van de Ervaring aan Maria DB te verbinden.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met Maria DB met behulp van de Flow Service API.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met Maria DB te verbinden, moet u het volgende verbindingsbezit verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die is gekoppeld aan uw Maria DB-verificatie. |

Raadpleeg [dit document](https://mariadb.com/kb/en/about-mariadb-connector-odbc/) voor meer informatie over hoe u aan de slag gaat met Maria DB.

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

Om verbinding te maken met Maria DB, moet er een reeks Maria DB-verbindingsspecificaties bestaan binnen Flow Service. De eerste stap bij het verbinden van Platform met Maria DB is deze specificaties terug te winnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. Het verzenden van een GET verzoek aan het `/connectionSpecs` eindpunt zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=name=="maria-db"` om informatie specifiek voor Maria DB te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="maria-db"
```

**Verzoek**

In het volgende verzoek worden de verbindingsspecificaties voor Maria DB opgehaald.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="maria-db"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de verbindingsspecificaties voor Maria DB, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "3000eb99-cd47-43f3-827c-43caf170f015",
            "name": "maria-db",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Connection String Based Authentication",
                    "type": "connectionStringAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to Maria DB",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "connection string to connect to any Maria DB instance.",
                                "format": "password",
                                "pattern": "^(Server=)(.*)(;Port=)(.*)(;Database=)(.*)(;UID=)(.*)(;PWD=)(.*)",
                                "examples": [
                                    "Server=<host>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>"
                                ]
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per Maria DB-account is slechts één basisverbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken die verschillende gegevens kunnen inbrengen.

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
        "name": "base connection for maria-db",
        "description": "base connection for maria-db",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "3000eb99-cd47-43f3-827c-43caf170f015",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die is gekoppeld aan uw Maria DB-verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie (`id`) die in de vorige stap wordt verzameld. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw cloudopslag in de volgende stap te verkennen.

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een Maria DB-basisverbinding gemaakt met de Flow Service API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert om gegevensbestanden of systemen te [onderzoeken NoSQL gebruikend de Dienst API](../../explore/database-nosql.md)van de Stroom.
