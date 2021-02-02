---
keywords: Experience Platform;home;populaire onderwerpen;Google Cloud Storage;google cloud-opslag;google;Google
solution: Experience Platform
title: Een Google Cloud Storage-connector maken met de Flow Service API
topic: overview
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform te verbinden met een Google Cloud Storage-account.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---


# Een [!DNL Google Cloud Storage]-connector maken met de [!DNL Flow Service]-API

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de [!DNL Flow Service]-API gebruikt om u door de stappen te laten lopen om [!DNL Experience Platform] te verbinden met een [!DNL Google Cloud Storage]-account.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een Google Cloud Storage-account met de [!DNL Flow Service]-API.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met uw [!DNL Google Cloud Storage]-account, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | De toegangs belangrijkste identiteitskaart voor uw [!DNL Google Cloud Storage] rekening. |
| `secretAccessKey` | De geheime toegangssleutel voor uw [!DNL Google Cloud Storage] rekening. |

Voor meer informatie over het aan de slag gaan, gaat u naar [dit Google Cloud-document](https://cloud.google.com/docs/authentication).

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

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL Google Cloud Storage]-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Om een [!DNL Google Cloud Storage] verbinding tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor [!DNL Google Cloud Storage] is `32e8f412-cdf7-464c-9885-78184cb113fd`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.accessKeyId` | De toegangs belangrijkste identiteitskaart verbonden aan uw [!DNL Google Cloud Storage] rekening. |
| `auth.params.secretAccessKey` | De geheime toegangssleutel verbonden aan uw [!DNL Google Cloud Storage] rekening. |
| `connectionSpec.id` | De [!DNL Google Cloud Storage] ID van de verbindingsspecificatie: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist voor het verkennen van uw gegevens voor cloudopslag in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Google Cloud Storage] verbinding gebruikend APIs gecreeerd en een unieke identiteitskaart werd verkregen als deel van het reactievermogen. Met deze verbindings-id kunt u [cloudopslag verkennen met de Flow Service API](../../explore/cloud-storage.md) of [Inst Parquet-gegevens met behulp van de Flow Service API](../../cloud-storage-parquet.md).