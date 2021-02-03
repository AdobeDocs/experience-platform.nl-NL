---
keywords: Experience Platform;home;populaire onderwerpen;bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: Een Google BigQuery-connector maken met de Flow Service API
topic: overview
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform aan Google BigQuery (hierna "BigQuery" genoemd) te verbinden.
translation-type: tm+mt
source-git-commit: ddf5be2f30bc347a881bdcbc6b880f087c03e263
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# Een [!DNL Google BigQuery]-connector maken met de [!DNL Flow Service]-API

>[!NOTE]
>
>De [!DNL Google BigQuery] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de [!DNL Flow Service]-API gebruikt om u door de stappen te laten lopen om [!DNL Experience Platform] te verbinden met [!DNL Google BigQuery] (hierna &quot;BigQuery&quot; genoemd).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met BigQuery met succes te verbinden gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] om BigQuery aan Platform aan te sluiten, moet u de volgende OAuth 2.0 authentificatiewaarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `project` | Projectidentiteitskaart van het gebrek [!DNL BigQuery] project om tegen te vragen. |
| `clientID` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `clientSecret` | De geheime waarde die wordt gebruikt om het te produceren vernieuwt teken. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen van [!DNL Google] wordt gebruikt om toegang tot [!DNL BigQuery] toe te staan. |

Voor meer informatie over deze waarden, verwijs naar [dit document BigQuery](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL BigQuery]-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere gegevensstromen te maken die verschillende gegevens opleveren.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een [!DNL BigQuery] verbinding tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor [!DNL BigQuery] is `3c9b37f8-13a6-43d8-bad3-b863b941fedd`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.project` | Projectidentiteitskaart van het gebrek [!DNL BigQuery] project aan vraag. tegen. |
| `auth.params.clientId` | De waarde van identiteitskaart die wordt gebruikt om het vernieuwingstoken te produceren. |
| `auth.params.clientSecret` | De clientwaarde die wordt gebruikt om het vernieuwingstoken te genereren. |
| `auth.params.refreshToken` | Het vernieuwingstoken dat wordt verkregen van [!DNL Google] wordt gebruikt om toegang tot [!DNL BigQuery] toe te staan. |
| `connectionSpec.id` | De verbindingsspecificatie `id` van uw [!DNL BigQuery] rekening die in de vorige stap wordt teruggewonnen. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen hebt u een [!DNL BigQuery]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsID in de volgende zelfstudie gebruiken aangezien u leert hoe te om [gegevensbestanden of systemen te onderzoeken NoSQL gebruikend de Dienst API van de Stroom](../../explore/database-nosql.md).
