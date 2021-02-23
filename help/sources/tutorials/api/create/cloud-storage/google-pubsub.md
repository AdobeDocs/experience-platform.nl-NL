---
keywords: Experience Platform;home;populaire onderwerpen;Google PubSub;Google pubsub
solution: Experience Platform
title: Een Google PubSub-bronverbinding maken met de Flow Service API
topic: ' - overzicht'
type: Tutorial
description: Leer hoe u Adobe Experience Platform kunt verbinden met een Google PubSub-account met behulp van de Flow Service API.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# Een [!DNL Google PubSub]-bronverbinding maken met de Flow Service API

>[!NOTE]
>
>De [!DNL Google PubSub] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

In deze zelfstudie wordt de [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) gebruikt om u door de stappen te laten lopen om [!DNL Google PubSub] (hierna &quot;[!DNL PubSub]&quot; genoemd) te verbinden met Adobe Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een [!DNL PubSub]-bronverbinding met de [!DNL Flow Service]-API te kunnen maken.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL PubSub], moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `projectId` | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| `credentials` | De referentie of sleutel die is vereist voor verificatie [!DNL PubSub]. |

Zie het volgende [PubSub-verificatie](https://cloud.google.com/pubsub/docs/authentication)-document voor meer informatie over deze waarden.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van de Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in Experience Platform, inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL PubSub]-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere gegevensstromen te maken die verschillende gegevens opleveren.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Als u een [!DNL PubSub]-verbinding wilt maken, moet u de provider-id en de verbindingsspecificatie-id opgeven als onderdeel van het verzoek om POST. De provider-id is `521eee4d-8cbe-4906-bb48-fb6bd4450033` en de verbindingsspecificatie-id is `70116022-a743-464a-bbfe-e226a7f8210c`.

**API-indeling**

```http
POST /connections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google PubSub connection",
        "description": "Google PubSub connection",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Google PubSub authentication credentials",
            "params": {
                "projectId": "{PROJECT_ID}",
                "credentials": "{CREDENTIALS}"
            }
        },
        "connectionSpec": {
            "id": "70116022-a743-464a-bbfe-e226a7f8210c",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.projectId` | De project-id die is vereist voor verificatie [!DNL PubSub]. |
| `auth.params.credentials` | De referentie of sleutel die is vereist voor verificatie [!DNL PubSub]. |
| `connectionSpec.id` | De [!DNL PubSub]-verbindings-ID: `70116022-a743-464a-bbfe-e226a7f8210c`. |

**Antwoord**

Een succesvolle reactie keert verbindingsidentiteitskaart van uw onlangs gecreeerd [!DNL PubSub] verbinding terug. Deze id is vereist voor het verkennen van uw gegevens voor cloudopslag in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL PubSub] verbinding gebruikend [!DNL Flow Service] API gecreeerd en zijn unieke verbindingsidentiteitskaart verworven. Met deze verbindings-id kunt u streaming gegevens [verzamelen met behulp van de Flow Service API](../../collect/streaming.md).
