---
keywords: Experience Platform;home;populaire onderwerpen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Creeer een Verbinding van de Basis van Zoho CRM gebruikend de Dienst API van de Stroom
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met Zoho CRM met behulp van de Flow Service API.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Een [!DNL Zoho CRM] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Zoho CRM] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met [!DNL Zoho CRM] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Zoho CRM]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| --- | --- |
| `endpoint` | Het eindpunt van het [!DNL Zoho CRM] server waarop u uw verzoek indient. |
| `accountsUrl` | De account-URL wordt gebruikt om uw toegangs- en vernieuwingstokens te genereren. De URL moet domeinspecifiek zijn. |
| `clientId` | De client-id die overeenkomt met uw [!DNL Zoho CRM] gebruikersaccount. |
| `clientSecret` | Het clientgeheim dat overeenkomt met uw [!DNL Zoho CRM] gebruikersaccount. |
| `accessToken` | Het toegangstoken verleent uw veilige en tijdelijke toegang tot uw [!DNL Zoho CRM] account. |
| `refreshToken` | Een vernieuwingstoken is een teken dat wordt gebruikt om een nieuw toegangstoken te produceren, zodra uw toegangstoken is verlopen. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Zoho CRM] is: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Zie de documentatie over [[!DNL Zoho CRM] verificatie](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Zoho CRM] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

>[!TIP]
>
>Het URL-domein van uw accounts moet overeenkomen met de juiste domeinlocatie. Hieronder ziet u de verschillende domeinen en de bijbehorende account-URL&#39;s:<ul><li>Verenigde Staten: https://accounts.zoho.com</li><li>Australië: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De naam van uw [!DNL Zoho CRM] basisverbinding. U kunt deze naam gebruiken om uw [!DNL Zoho CRM] basisverbinding. |
| `description` | Een optionele beschrijving voor uw [!DNL Zoho CRM] basisverbinding. |
| `auth.specName` | Het verificatietype dat voor de verbinding wordt gebruikt. |
| `auth.params.endpoint` | Het eindpunt van het [!DNL Zoho CRM] server waarop u uw verzoek indient. |
| `auth.params.accountsUrl` | De account-URL wordt gebruikt om uw toegangs- en vernieuwingstokens te genereren. De URL moet domeinspecifiek zijn. |
| `auth.params.clientId` | De client-id die overeenkomt met uw [!DNL Zoho CRM] gebruikersaccount. |
| `auth.params.clientSecret` | Het clientgeheim dat overeenkomt met uw [!DNL Zoho CRM] gebruikersaccount. |
| `auth.params.accessToken` | Het toegangstoken verleent uw veilige en tijdelijke toegang tot uw [!DNL Zoho CRM] account. |
| `auth.params.refreshToken` | Een vernieuwingstoken is een teken dat wordt gebruikt om een nieuw toegangstoken te produceren, zodra uw toegangstoken is verlopen. |
| `connectionSpec.id` | De verbindingsspecificatie-id voor [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Zoho] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van CRM aan Platform te brengen gebruikend [!DNL Flow Service] API](../../collect/crm.md)
