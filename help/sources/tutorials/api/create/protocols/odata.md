---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Generic OData-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---


# Een [!DNL Generic OData] aansluiting maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Generic OData] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen waarmee u verbinding [!DNL Generic OData] kunt maken [!DNL Experience Platform].

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met OData te verbinden gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Als u verbinding wilt [!DNL Flow Service] maken met OData, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| url | De basis-URL van de [!DNL OData] service. |
| connectionSpec.id | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL OData] is: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3` |

Raadpleeg [dit OData-document](https://www.odata.org/getting-started/basic-tutorial/)voor meer informatie over aan de slag gaan.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot de [!DNL Flow Service]sandboxen behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding per [!DNL OData] account vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een [!DNL OData] verbinding tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor [!DNL OData] is `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`.

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
            "url" :  "{URL}"
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
| `auth.params.url` | De host van de [!DNL OData] server. |
| `connectionSpec.id` | De id van de [!DNL OData] verbindingsspecificatie: `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL OData] verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken terwijl u leert hoe u protocoltoepassingen kunt [verkennen met behulp van de Flow Service API](../../explore/protocols.md).