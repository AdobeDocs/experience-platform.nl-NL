---
keywords: Experience Platform;home;populaire onderwerpen;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Een Amazon Kinesis Source Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een Amazon Kinesis-bron met behulp van de Flow Service API.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Een [!DNL Amazon Kinesis]-bronverbinding maken met de Flow Service API

Deze zelfstudie begeleidt u door de stappen om [!DNL Amazon Kinesis] (verder genoemd als &quot;[!DNL Kinesis]&quot;) met Experience Platform te verbinden, gebruikend [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van  [!DNL Platform] services.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om [!DNL Kinesis] met succes te kunnen verbinden met een Platform via de [!DNL Flow Service]-API.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met uw [!DNL Amazon Kinesis]-account, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangs belangrijkste identiteitskaart is de helft van het sleutelpaar dat wordt gebruikt om uw [!DNL Kinesis] rekening aan Platform voor authentiek te verklaren. |
| `secretKey` | De geheime toegangstoets is de andere helft van het sleutelpaar van de toegang dat wordt gebruikt om uw [!DNL Kinesis] rekening aan Platform voor authentiek te verklaren. |
| `region` | Het gebied voor uw [!DNL Kinesis] rekening. Zie de gids op [toevoegend IP adressen aan uw lijst van gewenste personen](../../../../ip-address-allow-list.md) voor meer informatie over gebieden. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De [!DNL Kinesis] ID van de verbindingsspecificatie is: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Voor meer informatie over [!DNL Kinesis] toegangssleutels en hoe te om hen te produceren, verwijs naar deze [[!DNL AWS] gids over het beheren van toegangstoetsen voor gebruikers IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

De eerste stap bij het creëren van een bronverbinding moet uw [!DNL Kinesis] bron voor authentiek verklaren en een identiteitskaart van de basisverbinding produceren. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Kinesis] authentificatiegeloofsbrieven als deel van de verzoekparameters.

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
| `auth.params.accessKeyId` | De toegangs belangrijkste identiteitskaart voor uw [!DNL Kinesis] rekening. |
| `auth.params.secretKey` | De geheime toegangssleutel voor uw [!DNL Kinesis] rekening. |
| `auth.params.region` | Het gebied voor uw [!DNL Kinesis] rekening. |
| `connectionSpec.id` | De [!DNL Kinesis] ID van de verbindingsspecificatie: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Een bronverbinding maken {#source}

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en bron identiteitskaart nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie IMS.

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan het `/sourceConnections` eindpunt van [!DNL Flow Service] API.

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
| `baseConnectionId` | De basis verbindingsID van uw [!DNL Kinesis] bron die in de vorige stap werd geproduceerd. |
| `connectionSpec.id` | The fixed connection specification ID for [!DNL Kinesis]. Deze id is: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | De indeling van de [!DNL Kinesis]-gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json`. |
| `params.stream` | De naam van de gegevensstroom waaruit records moeten worden opgehaald. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm`. |
| `params.reset` | Deze parameter bepaalt hoe de gegevens worden gelezen. Gebruik `latest` om te beginnen met het lezen van de meest recente gegevens en gebruik `earliest` om te beginnen met het lezen van de eerste beschikbare gegevens in de stream. |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Kinesis] bronverbinding tot stand gebracht gebruikend [!DNL Flow Service] API. U kunt deze bron verbindings-id in de volgende zelfstudie gebruiken om een streaminggegevensstroom te maken met de API [!DNL Flow Service] API](../../collect/streaming.md).[
