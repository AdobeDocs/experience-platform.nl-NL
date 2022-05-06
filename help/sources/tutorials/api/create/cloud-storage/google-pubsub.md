---
keywords: Experience Platform;home;populaire onderwerpen;Google PubSub;Google pubsub
solution: Experience Platform
title: Een Google PubSub-bronverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform kunt verbinden met een Google PubSub-account met behulp van de Flow Service API.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Een [!DNL Google PubSub] Bronverbinding met de Flow Service API

Dit leerprogramma begeleidt u door de stappen om te verbinden [!DNL Google PubSub] (hierna &quot;[!DNL PubSub]&quot;) naar Experience Platform, met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken [!DNL PubSub] naar Platform met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om verbinding te maken met [!DNL PubSub]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `projectId` | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| `credentials` | De referentie of sleutel die vereist is voor verificatie [!DNL PubSub]. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en brondoelverbindingen terug. De [!DNL PubSub] Verbindingsspecificatie-id is: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Zie deze voor meer informatie over deze waarden [[!DNL PubSub] verificatie](https://cloud.google.com/pubsub/docs/authentication) document. Om de op rekening-gebaseerde authentificatie van de dienst te gebruiken, zie dit [[!DNL PubSub] handleiding voor het maken van serviceaccounts](https://cloud.google.com/docs/authentication/production#create_service_account) voor stappen over hoe te om uw geloofsbrieven te produceren.

>[!TIP]
>
>Als u de op rekening-gebaseerde authentificatie van de dienst gebruikt, zorg ervoor dat u voldoende gebruikerstoegang tot uw de dienstrekening hebt verleend en dat er geen extra witte ruimten in JSON zijn, wanneer het kopiëren en het kleven van uw geloofsbrieven.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

De eerste stap bij het maken van een bronverbinding is het verifiëren van uw [!DNL PubSub] bron en genereer een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL PubSub] verificatiereferenties als onderdeel van de aanvraagparameters.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.projectId` | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| `auth.params.credentials` | De referentie of sleutel die vereist is voor verificatie [!DNL PubSub]. |
| `connectionSpec.id` | De [!DNL PubSub] verbinding, specificatie-id: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Antwoord**

Een succesvol antwoord retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze basis verbindings identiteitskaart wordt vereist in de volgende stap om een bronverbinding tot stand te brengen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Een bronverbinding maken {#source}

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Google PubSub source connection",
        "description": "A source connection for Google PubSub",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "topicId": "{TOPIC_ID}",
            "subscriptionId": "{SUBSCRIPTION_ID}",
            "dataType": "raw"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opgeven voor meer informatie over uw bronverbinding. |
| `baseConnectionId` | De basis verbindings-id van uw [!DNL PubSub] bron die in de vorige stap is gegenereerd. |
| `connectionSpec.id` | De vaste-verbindingsspecificatie-id voor [!DNL PubSub]. Deze id is: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | Het formaat van de [!DNL PubSub] gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |
| `params.topicId` | De onderwerpidentiteitskaart bepaalt het specifieke genoemde middel dat de berichten door uitgevers worden verzonden |
| `params.subscriptionId` | Abonnement ID bepaalt het specifieke genoemde middel dat de stroom van berichten van één enkel, specifiek onderwerp vertegenwoordigt, dat aan de het abonneren toepassing moet worden geleverd. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm`. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL PubSub] bronverbinding met de [!DNL Flow Service] API. U kunt deze bron-verbindings-id gebruiken in de volgende zelfstudie: [een streaming gegevensstroom maken met de opdracht [!DNL Flow Service] API](../../collect/streaming.md).
