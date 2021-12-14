---
keywords: Experience Platform;home;populaire onderwerpen;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Een Amazon Kinesis Source Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een Amazon Kinesis-bron met behulp van de Flow Service API.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Een [!DNL Amazon Kinesis] bronverbinding met behulp van de Flow Service API

Dit leerprogramma begeleidt u door de stappen om te verbinden [!DNL Amazon Kinesis] (hierna &quot;[!DNL Kinesis]&quot;) naar Experience Platform, met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken [!DNL Kinesis] naar Platform met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om verbinding te maken met uw [!DNL Amazon Kinesis] account, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangs belangrijkste identiteitskaart is één helft van het sleutelpaar dat wordt gebruikt om uw voor authentiek te verklaren [!DNL Kinesis] aan Platform. |
| `secretKey` | De geheime toegangstoets is de andere helft van het sleutelpaar van de toegang dat wordt gebruikt om uw voor authentiek te verklaren [!DNL Kinesis] aan Platform. |
| `region` | Het gebied voor uw [!DNL Kinesis] account. Zie de handleiding op [het toevoegen van IP adressen aan uw lijst van gewenste personen](../../../../ip-address-allow-list.md) voor meer informatie over de regio &#39; s . |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De [!DNL Kinesis] Verbindingsspecificatie-id is: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Voor meer informatie over [!DNL Kinesis] zie deze [[!DNL AWS] handleiding voor het beheren van toegangstoetsen voor IAM-gebruikers](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

De eerste stap bij het maken van een bronverbinding is het verifiëren van uw [!DNL Kinesis] bron en genereer een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Kinesis] verificatiereferenties als onderdeel van de aanvraagparameters.

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
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.accessKeyId` | De toegangstoets-id voor uw [!DNL Kinesis] account. |
| `auth.params.secretKey` | De geheime toegangssleutel voor uw [!DNL Kinesis] account. |
| `auth.params.region` | Het gebied voor uw [!DNL Kinesis] account. |
| `connectionSpec.id` | De [!DNL Kinesis] Verbindingsspecificatie-id: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Een bronverbinding maken {#source}

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en bron identiteitskaart nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie IMS.

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan `/sourceConnections` van het [!DNL Flow Service] API.

**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opgeven voor meer informatie over uw bronverbinding. |
| `baseConnectionId` | De basis verbindings-id van uw [!DNL Kinesis] bron die in de vorige stap is gegenereerd. |
| `connectionSpec.id` | De vaste-verbindingsspecificatie-id voor [!DNL Kinesis]. Deze id is: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Het formaat van de [!DNL Kinesis] gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |
| `params.stream` | De naam van de gegevensstroom waaruit records moeten worden opgehaald. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm`. |
| `params.reset` | Deze parameter bepaalt hoe de gegevens worden gelezen. Gebruiken `latest` beginnen met lezen van de meest recente gegevens en gebruiken `earliest` om te beginnen met lezen van de eerste beschikbare gegevens in de stream. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Kinesis] bronverbinding met de [!DNL Flow Service] API. U kunt deze bron-verbindings-id gebruiken in de volgende zelfstudie: [een streaming gegevensstroom maken met de opdracht [!DNL Flow Service] API](../../collect/streaming.md).
