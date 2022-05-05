---
keywords: Experience Platform;thuis;populaire onderwerpen;[!DNL Azure Table Storage];[!DNL Azure Table Storage];Azure table storage
solution: Experience Platform
title: Een Azure Table Storage Base Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Azure Table Storage met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
exl-id: 8ebd5d77-ed1f-47e1-8212-efb6c5e84ec1
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# Een [!DNL Azure Table Storage] basisverbinding met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Azure Table Storage] -connector bevindt zich in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Azure Table Storage] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Azure Table Storage] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Azure Table Storage]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met een [!DNL Azure Table Storage] -instantie. Het patroon van de verbindingstekenreeks voor [!DNL Azure Table Storage] is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Azure Table Storage] is `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

Voor meer informatie over het verkrijgen van een verbindingstekenreeks raadpleegt u [dit [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Azure Table Storage] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Azure Table Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met een [!DNL Azure Table Storage] -instantie. Het patroon van de verbindingstekenreeks voor [!DNL Azure Table Storage] is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | De [!DNL Azure Table Storage] Verbindingsspecificatie-id: `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

**Antwoord**

Een succesvol antwoord retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Azure Table Storage] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het Platform te brengen met de [!DNL Flow Service] API](../../collect/database-nosql.md)
