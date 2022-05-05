---
keywords: Experience Platform;home;populaire onderwerpen;PayPal-aansluiting;paypal;Paypal
solution: Experience Platform
title: Een PayPal-basisverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u PayPal met Adobe Experience Platform verbindt via de Flow Service API.
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: c0d750ef61ad2e295568cccabca5c52a758997c2
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# Een [!DNL PayPal] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL PayPal] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele instantie van het Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL PayPal] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL PayPal]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De URL van de [!DNL PayPal] -instantie. (standaard: api.sandbox.paypal.com). |
| `clientId` | De client-id die aan uw [!DNL PayPal] toepassing. |
| `clientSecret` | Het clientgeheim dat aan uw [!DNL PayPal] toepassing. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL PayPal] is: `221c7626-58f6-4eec-8ee2-042b0226f03b` |

Zie voor meer informatie over het aan de slag gaan [dit PayPal-document](https://developer.paypal.com/docs/api/overview/#get-credentials).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL PayPal] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL PayPal]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | De URL van de [!DNL PayPal] -instantie. |
| `auth.params.clientId` | De client-id die aan uw [!DNL PayPal] -instantie. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL PayPal] -instantie. |
| `connectionSpec.id` | De [!DNL PayPal] Verbindingsspecificatie-id: `221c7626-58f6-4eec-8ee2-042b0226f03b`. |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL PayPal] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om betalingsgegevens naar het Platform te verzenden met de opdracht [!DNL Flow Service] API](../../collect/payments.md)
