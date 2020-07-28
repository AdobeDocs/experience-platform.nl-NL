---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Amazon Redshift-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# Een [!DNL Amazon Redshift] aansluiting maken met de [!DNL Flow Service] API

>[!NOTE]
>De [!DNL Amazon Redshift] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de [!DNL Flow Service] API gebruikt om u door de stappen te laten lopen waarmee u verbinding [!DNL Experience Platform] kunt maken [!DNL Amazon Redshift] (hierna &quot;[!DNL Redshift]&quot; genoemd).

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Redshift] [!DNL Flow Service] de API.

### Vereiste referenties verzamelen

Als u verbinding wilt [!DNL Flow Service] maken met [!DNL Redshift], moet u de volgende verbindingseigenschappen opgeven:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| `server` | De server die aan uw [!DNL Redshift] account is gekoppeld. |
| `username` | De gebruikersnaam die aan uw [!DNL Redshift] account is gekoppeld. |
| `password` | Het wachtwoord dat aan uw [!DNL Redshift] account is gekoppeld. |
| `database` | De [!DNL Redshift] database die u opent. |

Raadpleeg [dit document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)voor opnieuw toewijzen voor meer informatie over aan de slag gaan.

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

Om een [!DNL Redshift] verbinding tot stand te brengen, moet een reeks [!DNL Redshift] verbindingsspecificaties binnen bestaan [!DNL Flow Service]. De eerste stap bij het verbinden [!DNL Platform] met [!DNL Redshift] is deze specificaties terug te winnen.

**API-indeling**

Elke beschikbare bron heeft zijn eigen unieke reeks verbindingsspecificaties voor het beschrijven van schakelaareigenschappen zoals authentificatievereisten. U kunt verbindingsspecificaties voor opzoeken [!DNL Redshift] door een verzoek van de GET uit te voeren en vraagparameters te gebruiken.

Het verzenden van een verzoek van de GET zonder vraagparameters zal verbindingsspecificaties voor alle beschikbare bronnen terugkeren. U kunt de vraag omvatten `property=name=="amazon-redshift"` om informatie specifiek voor te verkrijgen [!DNL Redshift].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="amazon-redshift"
```

**Verzoek**

In het volgende verzoek worden de verbindingsspecificaties opgehaald voor [!DNL Redshift].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="amazon-redshift"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de verbindingsspecificaties voor [!DNL Redshift], inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een basisverbinding te maken.

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

Een basisverbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL Redshift] account is slechts één basisverbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

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
| `auth.params.server` | Uw [!DNL Redshift] server. |
| `auth.params.database` | De database die aan uw [!DNL Redshift] account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Redshift] account is gekoppeld. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Redshift] account is gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw [!DNL Redshift] account die in de vorige stap is opgehaald. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Redshift] basisverbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze basis verbindings identiteitskaart in de volgende zelfstudie gebruiken aangezien u leert om gegevensbestanden of systemen te [onderzoeken NoSQL gebruikend de Dienst API](../../explore/database-nosql.md)van de Stroom.
