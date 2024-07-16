---
keywords: Experience Platform;thuis;populaire onderwerpen;Schopify;winkelen;e-commerce
solution: Experience Platform
title: Een Shopify-basisverbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Shopify met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Een [!DNL Shopify] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Shopify] tot stand te brengen (verder die als &quot; [!DNL Shopify] wordt bedoeld&quot;) gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Sources]](../../../../home.md) [!DNL Experience Platform] : hiermee kunt u gegevens uit verschillende bronnen invoegen en binnenkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] -services.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Shopify] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Shopify] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van de [!DNL Shopify] -server. |
| `accessToken` | Het toegangstoken voor uw [!DNL Shopify] gebruikersaccount. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Shopify] is: `4f63aa36-bd48-4e33-bb83-49fbcd11c708` . |

Voor meer informatie over begonnen worden, verwijs naar dit [ authentificatiedocument ](https://shopify.dev/concepts/about-apis/authentication) veranderen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Shopify] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Shopify] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | Het eindpunt van de [!DNL Shopify] server. |
| `auth.params.accessToken` | Het toegangstoken voor uw [!DNL Shopify] gebruikersaccount. |
| `connectionSpec.id` | The [!DNL Shopify] connection specification ID: `4f63aa36-bd48-4e33-bb83-49fbcd11c708` . |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Shopify] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevens E-Commerce aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/ecommerce.md)
