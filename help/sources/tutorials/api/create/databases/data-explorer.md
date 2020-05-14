---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Azure Data Explorer-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Een Azure Data Explorer-connector maken met de Flow Service API

>[!NOTE]
>De Azure Data Explorer-connector is in bèta. De functies en documentatie kunnen worden gewijzigd.

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Azure Data Explorer (hierna &quot;Data Explorer&quot; genoemd) aan Experience Platform te verbinden.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met de Ontdekkingsreiziger van Gegevens te verbinden gebruikend de Dienst API van de Stroom.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met de Ontdekkingsreiziger van Gegevens te verbinden, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de server van de Ontdekkingsreiziger van Gegevens. |
| `database` | De naam van de gegevensverkenner-database. |
| `tenant` | De unieke huurder-id die wordt gebruikt om verbinding te maken met de gegevensverkenner-database. |
| `servicePrincipalId` | De unieke dienst belangrijkste identiteitskaart die wordt gebruikt om met het gegevensbestand van de Ontdekkingsreiziger van Gegevens te verbinden. |
| `servicePrincipalKey` | De unieke de dienstbelangrijkste sleutel die wordt gebruikt om met het gegevensbestand van de Ontdekkingsreiziger van Gegevens te verbinden. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor Data Explorer is `0479cc14-7651-4354-b233-7480606c2ac3`. |

Voor meer informatie over begonnen worden verwijs naar [dit document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)van de Ontdekkingsreiziger van Gegevens.

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

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één connector vereist per Data Explorer-account omdat deze kan worden gebruikt om meerdere bronconnectors te maken om verschillende gegevens in te brengen.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een verbinding van de Ontdekkingsreiziger van Gegevens tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het POST- verzoek worden verstrekt. De verbindingsspecificatie-id voor Data Explorer is `0479cc14-7651-4354-b233-7480606c2ac3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.endpoint` | Het eindpunt van de server van de Ontdekkingsreiziger van Gegevens. |
| `auth.params.database` | De naam van de gegevensverkenner-database. |
| `auth.params.tenant` | De unieke huurder-id die wordt gebruikt om verbinding te maken met de gegevensverkenner-database. |
| `auth.params.servicePrincipalId` | De unieke dienst belangrijkste identiteitskaart die wordt gebruikt om met het gegevensbestand van de Ontdekkingsreiziger van Gegevens te verbinden. |
| `auth.params.servicePrincipalKey` | De unieke de dienstbelangrijkste sleutel die wordt gebruikt om met het gegevensbestand van de Ontdekkingsreiziger van Gegevens te verbinden. |
| `connectionSpec.id` | De specificatie-id van de gegevensverkenner-verbinding: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een verbinding van de Ontdekkingsreiziger van Gegevens tot stand gebracht gebruikend de Dienst API van de Stroom en hebt u de unieke waarde van identiteitskaart van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u databases kunt [verkennen met behulp van de Flow Service API](../../explore/database-nosql.md).
