---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een MariaDB-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: e4ed6ae3ee668cd0db741bd07d2fb7be593db4c9
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---


# Een MariaDB-connector maken met de Flow Service API

>[!NOTE]
>De MariaDB-connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

De Dienst van de stroom wordt gebruikt om klantengegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform met MariaDB te verbinden.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met MariaDB met behulp van de Flow Service API.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met MariaDB te verbinden, moet u het volgende verbindingsbezit verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die aan uw MariaDB-verificatie is gekoppeld. Het MariaDB-patroon van de verbindingstekenreeks is: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | De id die wordt gebruikt om een verbinding te genereren. De vaste verbinding-specificatie-id voor MariaDB is `3000eb99-cd47-43f3-827c-43caf170f015`. |

Raadpleeg [dit MariaDB-document](https://mariadb.com/kb/en/about-mariadb-connector-odbc/)voor meer informatie over het verkrijgen van een verbindingstekenreeks.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u eerst het [authentificatieleerprogramma](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in Experience Platform, inclusief die van de Flow Service, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding vereist per MariaDB-account, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Als u een MariaDB-verbinding wilt maken, moet de unieke specificatie-id van de verbinding worden opgegeven als onderdeel van de POST-aanvraag. De verbindingsspecificatie-id voor MariaDB is `3000eb99-cd47-43f3-827c-43caf170f015`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for maria-db",
        "description": "Test connection for maria-db",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
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
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw MariaDB-verificatie is gekoppeld. Het MariaDB-patroon van de verbindingstekenreeks is: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | De MariaDB-verbindings-specificatie-id is: `3000eb99-cd47-43f3-827c-43caf170f015`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw database in de volgende stap te verkennen.

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een MariaDB-verbinding gemaakt met de Flow Service API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsID in de volgende zelfstudie gebruiken aangezien u leert hoe te om gegevensbestanden of systemen te [onderzoeken NoSQL gebruikend de Dienst API](../../explore/database-nosql.md)van de Stroom.
