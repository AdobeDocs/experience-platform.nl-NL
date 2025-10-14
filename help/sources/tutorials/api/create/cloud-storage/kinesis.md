---
title: Een Amazon Kinesis Source Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met een Amazon Kinesis-bron met behulp van de Flow Service API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# Een [!DNL Amazon Kinesis] bronverbinding maken met de Flow Service API

>[!IMPORTANT]
>
>De [!DNL Amazon Kinesis] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Dit leerprogramma begeleidt u door de stappen om [!DNL Amazon Kinesis] (verder die als &quot; [!DNL Kinesis]&quot;worden bedoeld) met Experience Platform te verbinden, gebruikend [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u [!DNL Kinesis] met de API van [!DNL Flow Service] kunt verbinden met Experience Platform.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met uw [!DNL Amazon Kinesis] -account als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangs sleutel-id is de helft van het sleutelpaar dat wordt gebruikt voor het verifiëren van uw [!DNL Kinesis] -account bij Experience Platform. |
| `secretKey` | De geheime toegangstoets is de andere helft van het sleutelpaar voor toegang dat wordt gebruikt om uw [!DNL Kinesis] -account te verifiëren bij Experience Platform. |
| `region` | Het gebied voor uw [!DNL Kinesis] account. Zie de gids op [&#x200B; toevoegend IP adressen aan uw lijst van gewenste personen &#x200B;](../../../../ip-address-allow-list.md) voor meer informatie over gebieden. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De [!DNL Kinesis] -id van de verbindingsspecificatie is: `86043421-563b-46ec-8e6c-e23184711bf6` . |

Voor meer informatie over [!DNL Kinesis] toegangstoetsen en hoe te om hen te produceren, verwijs naar deze [[!DNL AWS]  gids over het beheren van toegangstoetsen voor gebruikers IAM &#x200B;](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

## Een basisverbinding maken

De eerste stap bij het maken van een bronverbinding is het verifiëren van de [!DNL Kinesis] -bron en het genereren van een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Kinesis] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

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
| `auth.params.accessKeyId` | De toegangstoets-id voor uw [!DNL Kinesis] -account. |
| `auth.params.secretKey` | De geheime toegangssleutel voor uw [!DNL Kinesis] account. |
| `auth.params.region` | Het gebied voor uw [!DNL Kinesis] account. |
| `connectionSpec.id` | De [!DNL Kinesis] connection specification ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Een bronverbinding maken {#source}

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en bron identiteitskaart nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie.

Als u een bronverbinding wilt maken, vraagt u een POST-aanvraag naar het `/sourceConnections` -eindpunt van de [!DNL Flow Service] API.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `baseConnectionId` | De basis verbindings-id van de [!DNL Kinesis] -bron die in de vorige stap is gegenereerd. |
| `connectionSpec.id` | The fixed connection specification ID for [!DNL Kinesis]. Deze id is: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | De indeling van de [!DNL Kinesis] -gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json` . |
| `params.stream` | De naam van de gegevensstroom waaruit records moeten worden opgehaald. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm` . |
| `params.reset` | Deze parameter bepaalt hoe de gegevens worden gelezen. Gebruik `latest` om te beginnen met het lezen van de meest recente gegevens en gebruik `earliest` om te beginnen met het lezen van de eerste beschikbare gegevens in de stream. |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>Nadat u een streaming gegevensstroom hebt gemaakt of bijgewerkt, moet u de gegevensinvoer kort na vijf minuten pauzeren om te voorkomen dat gegevens verloren gaan of dat gegevens verloren gaan.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Kinesis] -bronverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze bron verbindingsidentiteitskaart in het volgende leerprogramma gebruiken om [&#x200B; een het stromen dataflow tot stand te brengen gebruikend  [!DNL Flow Service]  API &#x200B;](../../collect/streaming.md).
