---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een schakelaar HubSpot gebruikend de Dienst API van de Stroom
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---


# Een [!DNL HubSpot] aansluiting maken met de [!DNL Flow Service] API

>[!NOTE]
>De [!DNL HubSpot] connector is in bèta. Zie het [Bronoverzicht](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

[!DNL Flow Service] wordt gebruikt om klantgegevens van diverse verschillende bronnen binnen Adobe Experience Platform te verzamelen en te centraliseren. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om u door de stappen te laten lopen waarmee u verbinding [!DNL Experience Platform] kunt maken [!DNL HubSpot].

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL HubSpot] [!DNL Flow Service] de API.

### Vereiste referenties verzamelen

Als u verbinding wilt [!DNL Flow Service] maken met [!DNL HubSpot], moet u de volgende verbindingseigenschappen opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Client-id | De client-id die aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| Toegangstoken | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| Token vernieuwen | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| Verbindingsspecificatie-id | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL HubSpot] is: `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Voor meer informatie over begonnen worden, verwijs naar dit [document](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)HubSpot.

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

Een verbinding specificeert een bron en bevat uw geloofsbrieven voor die bron. Er is slechts één verbinding per [!DNL HubSpot] account vereist, omdat deze kan worden gebruikt om meerdere bronconnectors te maken voor het inbrengen van verschillende gegevens.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Om een [!DNL HubSpot] verbinding tot stand te brengen, moet zijn unieke identiteitskaart van de verbindingsspecificatie als deel van het verzoek van de POST worden verstrekt. De verbindingsspecificatie-id voor [!DNL HubSpot] is `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.clientId` | De client-id die aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL HubSpot] toepassing is gekoppeld. |
| `auth.params.accessToken` | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `auth.params.refreshToken` | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |

**Antwoord**

Een geslaagde reactie retourneert details van de zojuist gemaakte verbinding voor de API, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Als u deze zelfstudie volgt, hebt u een [!DNL HubSpot] verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsID in de volgende zelfstudie gebruiken aangezien u leert hoe te om marketing automatiseringssystemen te [onderzoeken gebruikend de Dienst API](../../explore/marketing-automation.md)van de Stroom.