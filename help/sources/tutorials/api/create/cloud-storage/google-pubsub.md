---
keywords: Experience Platform;home;populaire onderwerpen;Google PubSub;Google pubsub
solution: Experience Platform
title: Een Google PubSub-bronverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform kunt verbinden met een Google PubSub-account met behulp van de Flow Service API.
exl-id: f5b8f9bf-8a6f-4222-8eb2-928503edb24f
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Een [!DNL Google PubSub]-bronverbinding maken met de Flow Service API

>[!NOTE]
>
>De [!DNL Google PubSub] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie begeleidt u door de stappen om [!DNL Google PubSub] (verder genoemd als &quot;[!DNL PubSub]&quot;) met Experience Platform te verbinden, gebruikend [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om [!DNL PubSub] met succes te kunnen verbinden met een Platform via de [!DNL Flow Service]-API.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL PubSub], moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `projectId` | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| `credentials` | De referentie of sleutel die is vereist voor verificatie [!DNL PubSub]. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en brondoelverbindingen terug. De [!DNL PubSub] ID van de verbindingsspecificatie is: `70116022-a743-464a-bbfe-e226a7f8210c`. |

Voor meer informatie over deze waarden, zie dit [[!DNL PubSub] authentificatie](https://cloud.google.com/pubsub/docs/authentication) document. Om de op rekening-gebaseerde authentificatie van de dienst te gebruiken, zie deze [[!DNL PubSub] gids bij het creëren van de dienstrekeningen](https://cloud.google.com/docs/authentication/production#create_service_account) voor stappen op hoe te om uw geloofsbrieven te produceren.

>[!TIP]
>
>Als u de op rekening-gebaseerde authentificatie van de dienst gebruikt, zorg ervoor dat u voldoende gebruikerstoegang tot uw de dienstrekening hebt verleend en dat er geen extra witte ruimten in JSON zijn, wanneer het kopiëren en het kleven van uw geloofsbrieven.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

De eerste stap bij het creëren van een bronverbinding moet uw [!DNL PubSub] bron voor authentiek verklaren en een identiteitskaart van de basisverbinding produceren. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL PubSub] authentificatiegeloofsbrieven als deel van de verzoekparameters.

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
| `auth.params.credentials` | De referentie of sleutel die is vereist voor verificatie [!DNL PubSub]. |
| `connectionSpec.id` | De [!DNL PubSub]-verbindings-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze basis verbindings identiteitskaart wordt vereist in de volgende stap om een bronverbinding tot stand te brengen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Een bronverbinding maken {#source}

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
| `baseConnectionId` | De basis verbindingsID van uw [!DNL PubSub] bron die in de vorige stap werd geproduceerd. |
| `connectionSpec.id` | The fixed connection specification ID for [!DNL PubSub]. Deze id is: `70116022-a743-464a-bbfe-e226a7f8210c` |
| `data.format` | De indeling van de [!DNL PubSub]-gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |
| `params.topicId` | De onderwerpidentiteitskaart bepaalt het specifieke genoemde middel dat de berichten door uitgevers worden verzonden |
| `params.subscriptionId` | Abonnement ID bepaalt het specifieke genoemde middel dat de stroom van berichten van één enkel, specifiek onderwerp vertegenwoordigt, dat aan de het abonneren toepassing moet worden geleverd. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm`. |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL PubSub] bronverbinding tot stand gebracht gebruikend [!DNL Flow Service] API. U kunt deze bron verbindings-id in de volgende zelfstudie gebruiken om een streaminggegevensstroom te maken met de API [!DNL Flow Service] API](../../collect/streaming.md).[
