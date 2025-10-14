---
keywords: Experience Platform;home;populaire onderwerpen;Square;square
title: Vierkante basisverbinding maken met de Flow Service API
description: Leer hoe u Square met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Een [!DNL Square] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Square] tot stand te brengen gebruikend [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Square] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Square] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| `host` | De URL van de instantie [!DNL Square] . |
| `clientId` | De client-id die aan uw [!DNL Square] -account is gekoppeld. |
| `clientSecret` | Het clientgeheim dat aan uw [!DNL Square] -account is gekoppeld. |
| `accessToken` | Het toegangstoken wordt gebruikt om uw [!DNL Square] rekening met authentificatie te verifiëren OAuth 2.0. Het toegangstoken kan uit [!DNL Square] worden verkregen. |
| `refreshToken` | Vernieuw teken wordt gebruikt om nieuwe toegangstoken te produceren zodra uw huidige toegangstoken verloopt. Het token voor vernieuwen kan worden opgehaald uit [!DNL Square] . |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Square] is: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Voor meer informatie over deze geloofsbrieven en hoe te om hen te verkrijgen, zie de [[!DNL Square]  documentatie over OAuth &#x200B;](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Square] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Square] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | De URL van de instantie [!DNL Square] . |
| `auth.params.clientId` | De client-id die aan uw [!DNL Square] -account is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL Square] -account is gekoppeld. |
| `auth.params.accessToken` | Het toegangstoken wordt gebruikt om uw [!DNL Square] rekening met authentificatie te verifiëren OAuth 2.0. Het toegangstoken kan uit [!DNL Square] worden verkregen. |
| `auth.params.refreshToken` | Vernieuw teken wordt gebruikt om nieuwe toegangstoken te produceren zodra uw huidige toegangstoken verloopt. Het token voor vernieuwen kan worden opgehaald uit [!DNL Square] . |
| `connectionSpec.id` | The [!DNL Square] connection specification ID: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` . |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Square] -verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze identiteitskaart in het volgende leerprogramma gebruiken aangezien u leert hoe te [&#x200B; betalingstoepassing onderzoeken gebruikend de Dienst API van de Stroom &#x200B;](../../explore/payments.md).
