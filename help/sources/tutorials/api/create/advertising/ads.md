---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een Google AdWords-connector maken met de Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Een Google AdWords-connector maken met de Flow Service API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen het Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform te verbinden met Google AdWords.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [Bronnen](../../../../home.md): Het Platform van de ervaring laat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien u van de capaciteit om inkomende gegevens te structureren, te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [Sandboxen](../../../../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met Ad via de Flow Service API.

### Vereiste referenties verzamelen

Voor de Dienst van de Stroom om met AdWords te verbinden, moet u waarden voor de volgende verbindingseigenschappen verstrekken:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| Klant-id klant | De klant-id van de client van het account AdWords. |
| Developer Token | Het ontwikkelaarstoken verbonden aan de managerrekening. |
| Token vernieuwen | Het vernieuwingstoken dat bij Google is verkregen voor het toestaan van toegang tot AdWords. |
| Client-id | De client-id van de Google-toepassing waarmee de vernieuwingstoken wordt aangeschaft. |
| Clientgeheim | Het clientgeheim van de Google-toepassing die wordt gebruikt om het vernieuwingstoken te verkrijgen. |
| Verbindingsspecificatie-id | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor Google AdWords is: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Raadpleeg dit [Google AdWords-document](https://developers.google.com/adwords/api/docs/guides/authentication)voor meer informatie over deze waarden.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../../../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief de bronnen die bij Flow Service horen, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding vereist per Google AdWords-account, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het invoeren van verschillende gegevens.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe verbinding AdWords, die door de eigenschappen wordt gevormd die in de lading worden verstrekt:


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
| `auth.params.clientCustomerID` | De client-id van uw AdWords-account. |
| `auth.params.developerToken` | De ontwikkelaarstoken van uw account AdWords. |
| `auth.params.refreshToken` | Het vernieuwingstoken van uw account AdWords. |
| `auth.params.clientID` | De client-id van uw AdWords-account. |
| `auth.params.clientSecret` | Het clientgeheim van uw AdWords-account. |
| `connectionSpec.id` | De Google AdWords-verbindingsspecificatie-id: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een Google AdWords-verbinding gemaakt met de Flow Service API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken als u wilt leren [op welke manier u advertentiesystemen kunt verkennen met behulp van de Flow Service API](../../explore/advertising.md).
