---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Google BigQuery-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: e6a3f9a834300ffadb28a05c8f4e5355a8de2411

---


# Een Google BigQuery-connector maken met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om het Experience Platform te verbinden met Google BigQuery (hierna &quot;BigQuery&quot; genoemd).

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met BigQuery gebruikend de Dienst API van de Stroom te verbinden.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met BigQuery te verbinden, moet u de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | Projectidentiteitskaart van het standaard project BigQuery aan vraag tegen. |
| `clientID` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `clientSecret` | De geheime waarde die wordt gebruikt om het te produceren vernieuwt teken. |
| `refreshToken` | Het vernieuwingstoken dat bij Google wordt verkregen en waarmee toegang tot BigQuery wordt toegestaan. |

Raadpleeg [dit BigQuery-document](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)voor meer informatie over deze waarden.

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

Als u een BigQuery-verbinding wilt maken, moet er een set BigQuery-verbindingsspecificaties bestaan binnen Flow Service. De eerste stap in het verbinden van Platform met BigQuery is deze specificaties terug te winnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. U kunt verbindingsspecificaties voor BigQuery opzoeken door een GET verzoek uit te voeren en vraagparameters te gebruiken.

Het verzenden van een GET verzoek zonder vraagparameters zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=name=="google-big-query"` om informatie specifiek voor BigQuery te verkrijgen.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="google-big-query"
```

**Verzoek**

Het volgende verzoek wint de verbindingsspecificaties voor BigQuery terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de verbindingsspecificaties voor BigQuery, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een basisverbinding te maken.

```json
{
    "items": [
        {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "name": "google-big-query",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "project": {
                                "type": "string",
                                "description": "The project ID of the default BigQuery project to query against"
                            },
                            "clientId": {
                                "type": "string",
                                "description": "ID of the application used to generate the refresh token."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "Secret of the application used to generate the refresh token.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained from Google used to authorize access to BigQuery.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "project",
                            "clientId",
                            "clientSecret",
                            "refreshToken"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## Een basisverbinding maken

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per BigQuery-account is slechts één basisverbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken die verschillende gegevens kunnen inbrengen.

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
        "name": "BigQuery base connection",
        "description": "Base connection for Google BigQuery",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "project": "{PROJECT}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.project` | Projectidentiteitskaart van het standaard project BigQuery aan vraag. tegen. |
| `auth.params.clientId` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `auth.params.clientSecret` | De clientwaarde die wordt gebruikt om het vernieuwingstoken te genereren. |
| `auth.params.refreshToken` | Het vernieuwingstoken dat bij Google wordt verkregen en waarmee toegang tot BigQuery wordt toegestaan. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw BigQuery-account die in de vorige stap is opgehaald. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "26ced882-729b-470f-8ed8-82729b570f03",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een BigQuery-basisverbinding gemaakt met de Flow Service API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert om gegevensbestanden of systemen te [onderzoeken NoSQL gebruikend de Dienst API](../../explore/database-nosql.md)van de Stroom.
