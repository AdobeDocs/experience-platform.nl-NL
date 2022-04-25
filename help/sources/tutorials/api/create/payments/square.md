---
keywords: Experience Platform;thuis;populaire onderwerpen;Vierkant;vierkant
title: Vierkante basisverbinding maken met de Flow Service API
description: Leer hoe u Square met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
source-git-commit: f2f602fd618dc6b59ba13c275ca0c2964e3ea1f4
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# Een [!DNL Square] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Square] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele instantie van het Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Square] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Square]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| --- | --- |
| `host` | De URL van de [!DNL Square] -instantie. |
| `clientId` | De client-id die aan uw [!DNL Square] account. |
| `clientSecret` | Het clientgeheim dat aan uw [!DNL Square] account. |
| `accessToken` | Het toegangstoken wordt gebruikt om uw voor authentiek te verklaren [!DNL Square] account met OAuth 2.0-verificatie. Het toegangstoken kan worden verkregen van [!DNL Square]. |
| `refreshToken` | Vernieuw teken wordt gebruikt om nieuwe toegangstoken te produceren zodra uw huidige toegangstoken verloopt. Het vernieuwingstoken kan worden verkregen van [!DNL Square]. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Square] is: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Voor meer informatie over deze geloofsbrieven en hoe te om hen te verkrijgen, zie [[!DNL Square] documentatie over OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Square] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | De URL van de [!DNL Square] -instantie. |
| `auth.params.clientId` | De client-id die aan uw [!DNL Square] account. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL Square] account. |
| `auth.params.accessToken` | Het toegangstoken wordt gebruikt om uw voor authentiek te verklaren [!DNL Square] account met OAuth 2.0-verificatie. Het toegangstoken kan worden verkregen van [!DNL Square]. |
| `auth.params.refreshToken` | Vernieuw teken wordt gebruikt om nieuwe toegangstoken te produceren zodra uw huidige toegangstoken verloopt. Het vernieuwingstoken kan worden verkregen van [!DNL Square]. |
| `connectionSpec.id` | De [!DNL Square] Verbindingsspecificatie-id: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Square] verbinding met de [!DNL Flow Service] API en hebben de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u [betalingstoepassing verkennen met de Flow Service API](../../explore/payments.md).
