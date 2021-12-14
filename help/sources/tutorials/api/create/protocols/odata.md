---
keywords: Experience Platform;home;populaire onderwerpen;Generic OData;generieke gegevens
solution: Experience Platform
title: Een algemene OData-basisverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Generic OData met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
exl-id: 45b302cb-1a43-4fab-a8a2-cb4e1ee129f9
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---

# Een [!DNL Generic OData] basisverbinding met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Generic OData] -connector bevindt zich in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Generic OData] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Generic OData] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Generic OData]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De basis-URL van het dialoogvenster [!DNL Generic OData] service. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Generic Generic OData] is: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

Zie voor meer informatie over het aan de slag gaan [dit [!DNL Generic OData] document](https://www.odata.org/getting-started/basic-tutorial/).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Generic OData] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Generic OData]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Protocols",
        "description": "A test connection for a Protocols source",
        "auth": {
            "specName": "Anonymous Authentication",
        "params": {
            "url":  "{URL}"
            }
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.url` | De gastheer van de [!DNL Generic OData] server. |
| `connectionSpec.id` | De [!DNL Generic OData] Verbindingsspecificatie-id: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL OData] verbinding met de [!DNL Flow Service] API en hebben de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u [protocoltoepassingen verkennen met behulp van de Flow Service API](../../explore/protocols.md).
