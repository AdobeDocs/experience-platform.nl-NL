---
keywords: Experience Platform;home;populaire onderwerpen;Azure Data Lake Storage Gen2;azure data Lake storage;Azure
solution: Experience Platform
title: Een Azure Data Lake Storage Gen2 Base Connection maken met behulp van de Flow Service API
type: Tutorial
description: Leer hoe u Adobe Experience Platform kunt verbinden met Azure Data Lake Storage Gen2 met behulp van de Flow Service API.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Een [!DNL Azure Data Lake Storage Gen2] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Azure Data Lake Storage Gen2] tot stand te brengen (verder die als &quot;ADLS Gen2&quot;worden bedoeld) gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een ADLS Gen2-bronverbinding met de [!DNL Flow Service] API te kunnen maken.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met ADLS Gen2 als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | Het eindpunt voor ADLS Gen2. Het eindpuntpatroon is: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | De client-id van de toepassing. |
| `servicePrincipalKey` | De sleutel van de toepassing. |
| `tenant` | De huurdersinformatie die uw toepassing bevat. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor ADLS Gen2 is: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` . |

Voor meer informatie over deze waarden, verwijs naar [ dit document van ADLS Gen2 ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een POST- verzoek aan het `/connections` eindpunt terwijl het verstrekken van uw authentificatie ADLS Gen2 als deel van de verzoekparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met het volgende verzoek wordt een basisverbinding voor ADLS Gen2 gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.url` | Het URL-eindpunt voor uw ADLS Gen2-account. |
| `auth.params.servicePrincipalId` | De service principal ID van uw ADLS Gen2-account. |
| `auth.params.servicePrincipalKey` | De belangrijkste servicetoets van uw ADLS Gen2-account. |
| `auth.params.tenant` | De huurdersinformatie van uw account van ADLS Gen2. |
| `connectionSpec.id` | The ADLS Gen2 connection specification ID: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een ADLS Gen2-verbinding gemaakt met behulp van API&#39;s en is een unieke id opgehaald als onderdeel van de responsstructuur. U kunt deze verbindingsidentiteitskaart gebruiken om [ wolkenopslag te onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
