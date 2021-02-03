---
keywords: Experience Platform;home;populaire onderwerpen;google adwords;Google AdWords;adwords
solution: Experience Platform
title: Een Google AdWords-connector maken met de Flow Service API
topic: overview
type: Tutorial
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform te verbinden met Google AdWords.
translation-type: tm+mt
source-git-commit: 48a5dcfe5679e360da1e33f6021dc1229b92948f
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---


# Een [!DNL Google AdWords]-connector maken met de [!DNL Flow Service]-API

>[!NOTE]
>
>De [!DNL Google AdWords] schakelaar is in bèta. Zie [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te leiden om [!DNL Experience Platform] aan [!DNL Google AdWords] te verbinden.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om een verbinding met Advertentie met de API [!DNL Flow Service] tot stand te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt verbinden met AdWords, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| `clientCustomerId` | De klant-id van de client van het account AdWords. |
| `developerToken` | Het ontwikkelaarstoken verbonden aan de managerrekening. |
| `refreshToken` | Het vernieuwingstoken dat van [!DNL Google] wordt verkregen om toegang tot AdWords toe te staan. |
| `clientId` | De client-id van de [!DNL Google]-toepassing die wordt gebruikt om het vernieuwingstoken te verkrijgen. |
| `clientSecret` | Het clientgeheim van de toepassing [!DNL Google] die wordt gebruikt om het vernieuwingstoken te verkrijgen. |
| `connectionSpec` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL Google AdWords] is: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Raadpleeg dit [Google AdWords-document](https://developers.google.com/adwords/api/docs/guides/authentication) voor meer informatie over deze waarden.

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

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Per [!DNL Google AdWords]-account is slechts één verbinding vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Om een [!DNL Google AdWords] verbinding tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor [!DNL Google AdWords] is `d771e9c1-4f26-40dc-8617-ce58c4b53702`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.clientCustomerID` | De client-id van uw [!DNL AdWords]-account. |
| `auth.params.developerToken` | De ontwikkelaarstoken van uw [!DNL AdWords]- rekening. |
| `auth.params.refreshToken` | Het vernieuwingstoken van uw [!DNL AdWords]-account. |
| `auth.params.clientID` | De client-id van uw [!DNL AdWords]-account. |
| `auth.params.clientSecret` | Het clientgeheim van uw [!DNL AdWords]-account. |
| `connectionSpec.id` | De [!DNL Google AdWords] ID van de verbindingsspecificatie: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen hebt u een [!DNL Google AdWords]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken wanneer u leert hoe u advertentiesystemen kunt [verkennen met behulp van de Flow Service API](../../explore/advertising.md).
