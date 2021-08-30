---
keywords: Experience Platform;home;populaire onderwerpen;gebeurtenishub;Azure-gebeurtenishub;Event-hub
solution: Experience Platform
title: Een Azure Event Hubs Source Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een Azure Event Hubs-account met behulp van de Flow Service API.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---


# Een [!DNL Azure Event Hubs]-bronverbinding maken met de [!DNL Flow Service]-API

Deze zelfstudie begeleidt u door de stappen om [!DNL Azure Event Hubs] (verder genoemd als &quot;[!DNL Event Hubs]&quot;) met Experience Platform te verbinden, gebruikend [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
- [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om [!DNL Event Hubs] met succes te kunnen verbinden met een Platform via de [!DNL Flow Service]-API.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met uw [!DNL Event Hubs]-account, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De gegenereerde handtekening voor gedeelde toegang. |
| `namespace` | De naamruimte van de [!DNL Event Hubs] die u opent. Een [!DNL Event Hubs] namespace verstrekt een unieke bereikingscontainer, waarin u één of meerdere [!DNL Event Hubs] kunt tot stand brengen. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De [!DNL Event Hubs] ID van de verbindingsspecificatie is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

Voor meer informatie over deze waarden, verwijs naar [dit document van de Hubs van Gebeurtenis](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

De eerste stap bij het creëren van een bronverbinding moet uw [!DNL Event Hubs] bron voor authentiek verklaren en een identiteitskaart van de basisverbinding produceren. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Event Hubs] authentificatiegeloofsbrieven als deel van de verzoekparameters.

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
| `auth.params.namespace` | De naamruimte van de [!DNL Event Hubs] die u opent. |
| `connectionSpec.id` | De [!DNL Event Hubs] ID van de verbindingsspecificatie is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze verbinding-id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Een bronverbinding maken

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en een identiteitskaart van de bronverbinding nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie IMS.

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan het `/sourceConnections` eindpunt van [!DNL Flow Service] API.

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
| `baseConnectionId` | De verbindingsID van uw [!DNL Event Hubs] bron die in de vorige stap werd geproduceerd. |
| `connectionSpec.id` | The fixed connection specification ID for [!DNL Event Hubs]. Deze id is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | De indeling van de [!DNL Event Hubs]-gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |
| `params.eventHubName` | De naam voor uw [!DNL Event Hubs] bron. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm`. |
| `params.reset` | Deze parameter bepaalt hoe de gegevens worden gelezen. Gebruik `latest` om te beginnen met het lezen van de meest recente gegevens en gebruik `earliest` om te beginnen met het lezen van de eerste beschikbare gegevens in de stream. Deze parameter is optioneel en wordt standaard ingesteld op `earliest` als deze parameter niet wordt opgegeven. |
| `params.consumerGroup` | Het publicatie- of abonnementsmechanisme dat moet worden gebruikt voor [!DNL Event Hubs]. Deze parameter is optioneel en wordt standaard ingesteld op `$Default` als deze parameter niet wordt opgegeven. Raadpleeg deze [[!DNL Event Hubs] handleiding over gebeurtenisconsumenten](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) voor meer informatie. |

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Event Hubs] bronverbinding tot stand gebracht gebruikend [!DNL Flow Service] API. U kunt deze bron verbindings-id in de volgende zelfstudie gebruiken om een streaminggegevensstroom te maken met de API [!DNL Flow Service] API](../../collect/streaming.md).[
