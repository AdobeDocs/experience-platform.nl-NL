---
keywords: Experience Platform;thuis;populaire onderwerpen;Azure Data Lake Storage Gen2;azure data Lake storage;Azure
solution: Experience Platform
title: Een Azure Data Lake Storage Gen2 Base Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform kunt verbinden met Azure Data Lake Storage Gen2 met behulp van de Flow Service API.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# Een [!DNL Azure Data Lake Storage Gen2] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Azure Data Lake Storage Gen2] (hierna &quot;ADLS Gen2&quot; genoemd) met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele instantie van het Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om tot een bron van ADLS Gen2 te leiden verbinding gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] Als u verbinding wilt maken met ADLS Gen2, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | Het eindpunt voor ADLS Gen2. Het eindpuntpatroon is: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | De client-id van de toepassing. |
| `servicePrincipalKey` | De sleutel van de toepassing. |
| `tenant` | De huurdersinformatie die uw toepassing bevat. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor ADLS Gen2 is: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Zie voor meer informatie over deze waarden [dit ADLS Gen2-document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw geloofsbrieven van de authentificatie ADLS Gen2 als deel van de verzoekparameters.

**API-indeling**

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
| `connectionSpec.id` | De ID van de ADLS Gen2-verbindingsspecificatie: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een ADLS Gen2-verbinding gemaakt met behulp van API&#39;s en is een unieke id opgehaald als onderdeel van de responsstructuur. U kunt deze verbindings-id gebruiken om [verkennen van cloudopslag met de Flow Service API](../../explore/cloud-storage.md).
