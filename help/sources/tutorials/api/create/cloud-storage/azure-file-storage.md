---
keywords: Experience Platform;home;popular topics;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Een Azure File Storage-connector maken met de Flow Service API
topic: overview
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Azure File Storage te verbinden met Experience Platform.
translation-type: tm+mt
source-git-commit: d332226541685108b58d88096146ed6048606774
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---


# Een [!DNL Azure File Storage] aansluiting maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Azure File Storage] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen waarmee u verbinding [!DNL Azure File Storage] kunt maken [!DNL Experience Platform].

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Azure File Storage] [!DNL Flow Service] de API.

### Vereiste referenties verzamelen

Als u verbinding wilt [!DNL Flow Service] maken met [!DNL Azure File Storage], moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van de [!DNL Azure File Storag]e instantie waartoe u toegang hebt. |
| `userId` | De gebruiker met voldoende toegang tot het [!DNL Azure File Storage] eindpunt. |
| `password` | Het wachtwoord voor uw [!DNL Azure File Storage] exemplaar |
| Verbindingsspecificatie-id | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL Azure File Storage] is: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Raadpleeg [dit Azure File Storage-document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)voor meer informatie over hoe u aan de slag gaat.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

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

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding vereist per Azure File Storage-account, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe [!DNL Azure File Storage] verbinding, die door de eigenschappen wordt gevormd die in de lading worden verstrekt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | Het eindpunt van de [!DNL Azure File Storage] instantie waartoe u toegang hebt. |
| `auth.params.userId` | De gebruiker met voldoende toegang tot het [!DNL Azure File Storage] eindpunt. |
| `auth.params.password` | De [!DNL Azure File Storage] toegangstoets. |
| `connectionSpec.id` | De id van de [!DNL Azure File Storage] verbindingsspecificatie: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Azure File Storage] verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken als u leert hoe u een externe cloudopslag kunt [verkennen met de Flow Service API](../../explore/cloud-storage.md).
