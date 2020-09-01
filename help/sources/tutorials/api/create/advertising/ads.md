---
keywords: Experience Platform;home;popular topics;google adwords;Google AdWords;adwords
solution: Experience Platform
title: Een Google AdWords-connector maken met de Flow Service API
topic: overview
description: Deze zelfstudie gebruikt de Flow Service API om u door de stappen te laten lopen om Experience Platform te verbinden met Google AdWords.
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Een [!DNL Google AdWords] aansluiting maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Google AdWords] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen waarmee u verbinding [!DNL Experience Platform] kunt maken [!DNL Google AdWords].

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met Advertentie met behulp van de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Als u verbinding wilt maken [!DNL Flow Service] met AdWords, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| Klant-id klant | De klant-id van de client van het account AdWords. |
| Developer Token | Het ontwikkelaarstoken verbonden aan de managerrekening. |
| Token vernieuwen | Vernieuw teken dat van [!DNL Google] voor het machtigen van toegang tot AdWords wordt verkregen. |
| Client-id | De client-id van de [!DNL Google] toepassing waarmee het vernieuwingstoken wordt opgehaald. |
| Clientgeheim | Het clientgeheim van de [!DNL Google] toepassing die wordt gebruikt om het token voor vernieuwen te verkrijgen. |
| Verbindingsspecificatie-id | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL Google AdWords] is: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Raadpleeg dit [Google AdWords-document](https://developers.google.com/adwords/api/docs/guides/authentication)voor meer informatie over deze waarden.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Verbinding maken

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding per [!DNL Google AdWords] account vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

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
| `auth.params.clientCustomerID` | De client-id van uw [!DNL AdWords] account. |
| `auth.params.developerToken` | De ontwikkelaarstoken van uw [!DNL AdWords] account. |
| `auth.params.refreshToken` | Het token voor vernieuwen van uw [!DNL AdWords] account. |
| `auth.params.clientID` | De client-id van uw [!DNL AdWords] account. |
| `auth.params.clientSecret` | Het clientgeheim van uw [!DNL AdWords] account. |
| `connectionSpec.id` | De id van de [!DNL Google AdWords] verbindingsspecificatie: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Google AdWords] verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze id in de volgende zelfstudie gebruiken als u wilt leren [op welke manier u advertentiesystemen kunt verkennen met behulp van de Flow Service API](../../explore/advertising.md).
