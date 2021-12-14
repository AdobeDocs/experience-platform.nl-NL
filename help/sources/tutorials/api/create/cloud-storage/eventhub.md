---
keywords: Experience Platform;home;populaire onderwerpen;gebeurtenishub;Azure-gebeurtenishub;Event-hub
solution: Experience Platform
title: Een Azure Event Hubs Source Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een Azure Event Hubs-account met behulp van de Flow Service API.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---


# Een [!DNL Azure Event Hubs] bronverbinding met de [!DNL Flow Service] API

Dit leerprogramma begeleidt u door de stappen om te verbinden [!DNL Azure Event Hubs] (hierna &quot;[!DNL Event Hubs]&quot;) naar Experience Platform, met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
- [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken [!DNL Event Hubs] naar Platform met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om verbinding te maken met uw [!DNL Event Hubs] account, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De primaire sleutel van de [!DNL Event Hubs] naamruimte. De `sasPolicy` de `sasKey` komt overeen met `manage` rechten die zijn geconfigureerd voor de [!DNL Event Hubs] in te vullen lijst. |
| `namespace` | De naamruimte van de [!DNL Event Hubs] u hebt toegang. An [!DNL Event Hubs] namespace verstrekt een unieke bereikcontainer, waarin u één of meerdere kunt tot stand brengen [!DNL Event Hubs]. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De [!DNL Event Hubs] Verbindingsspecificatie-id is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Zie voor meer informatie over deze waarden [this Event Hubs document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

De eerste stap bij het maken van een bronverbinding is het verifiëren van uw [!DNL Event Hubs] bron en genereer een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Event Hubs] verificatiereferenties als onderdeel van de aanvraagparameters.

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
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `auth.params.sasKey` | De gegenereerde handtekening voor gedeelde toegang. |
| `auth.params.namespace` | De naamruimte van de [!DNL Event Hubs] u hebt toegang. |
| `connectionSpec.id` | De [!DNL Event Hubs] Verbindingsspecificatie-id is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze verbinding-id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Een bronverbinding maken

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en een identiteitskaart van de bronverbinding nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie IMS.

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan `/sourceConnections` van het [!DNL Flow Service] API.

**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_Org}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opgeven voor meer informatie over uw bronverbinding. |
| `baseConnectionId` | De verbinding-id van uw [!DNL Event Hubs] bron die in de vorige stap is gegenereerd. |
| `connectionSpec.id` | De vaste-verbindingsspecificatie-id voor [!DNL Event Hubs]. Deze id is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | Het formaat van de [!DNL Event Hubs] gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |
| `params.eventHubName` | De naam voor uw [!DNL Event Hubs] bron. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm`. |
| `params.reset` | Deze parameter bepaalt hoe de gegevens worden gelezen. Gebruiken `latest` beginnen met lezen van de meest recente gegevens en gebruiken `earliest` om te beginnen met lezen van de eerste beschikbare gegevens in de stream. Deze parameter is optioneel en wordt standaard ingesteld op `earliest` indien niet verstrekt. |
| `params.consumerGroup` | Het publicatie- of abonnementsmechanisme dat moet worden gebruikt voor [!DNL Event Hubs]. Deze parameter is optioneel en wordt standaard ingesteld op `$Default` indien niet verstrekt. Zie dit [[!DNL Event Hubs] gids over evenementen voor consumenten](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) voor meer informatie . |

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Event Hubs] bronverbinding met de [!DNL Flow Service] API. U kunt deze bron-verbindings-id gebruiken in de volgende zelfstudie: [een streaming gegevensstroom maken met de opdracht [!DNL Flow Service] API](../../collect/streaming.md).
