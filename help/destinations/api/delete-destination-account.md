---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;delete doelaccounts;delete;api
solution: Experience Platform
title: Een doelaccount verwijderen met de Flow Service API
type: Tutorial
description: Leer hoe u een doelaccount kunt verwijderen met de Flow Service API.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 9%

---

# Een doelaccount verwijderen met de Flow Service API

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

Voordat u gegevens kunt activeren, moet u verbinding maken met de bestemming door eerst een doelaccount in te stellen. Dit leerprogramma behandelt de stappen om bestemmingsrekeningen te schrappen die niet meer nodig zijn door [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/) te gebruiken.

>[!NOTE]
>
>Het verwijderen van doelaccounts wordt momenteel alleen ondersteund in de Flow Service API. Bestemmingsaccounts kunnen niet worden verwijderd met de gebruikersinterface van Experience Platform.

## Aan de slag {#get-started}

Voor deze zelfstudie moet u een geldige verbinding-id hebben. De verbindings-id vertegenwoordigt de accountverbinding met de bestemming. Als u geen geldige verbindingsidentiteitskaart hebt, selecteer uw bestemming van keus van de [&#x200B; bestemmingscatalogus &#x200B;](../catalog/overview.md) en volg de stappen die aan [&#x200B; worden geschetst verbinden met de bestemming &#x200B;](../ui/connect-destination.md) alvorens dit leerprogramma te proberen.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Doelen &#x200B;](../home.md): [!DNL Destinations] zijn pre-gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.
* [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een doelaccount met de [!DNL Flow Service] API te kunnen verwijderen.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Als de header `x-sandbox-name` niet is opgegeven, worden aanvragen opgelost onder de sandbox `prod` .

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* `Content-Type: application/json`

## De verbinding-id zoeken van de doelaccount die u wilt verwijderen {#find-connection-id}

>[!NOTE]
>Dit leerprogramma gebruikt de [&#x200B; bestemming van het Luchtschip &#x200B;](../catalog/mobile-engagement/airship-attributes.md) als voorbeeld, maar de stappen die worden geschetst zijn op om het even welke [&#x200B; beschikbare bestemmingen &#x200B;](../catalog/overview.md) van toepassing.

De eerste stap bij het verwijderen van een doelaccount is om de verbinding-id te achterhalen die overeenkomt met de doelaccount die u wilt verwijderen.

Blader in de gebruikersinterface van Experience Platform naar **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** en selecteer de account die u wilt verwijderen door het nummer in de kolom **[!UICONTROL Destinations]** te selecteren.

![&#x200B; Uitgezochte bestemmingsrekening om te schrappen &#x200B;](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Vervolgens kunt u de verbinding-id van het doelaccount ophalen via de URL in uw browser.

![&#x200B; wint verbindingsidentiteitskaart van URL &#x200B;](/help/destinations/assets/api/delete-destination-account/find-connection-id.png) terug

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## Verbinding verwijderen {#delete-connection}

>[!IMPORTANT]
>
>Voordat u de doelaccount verwijdert, moet u bestaande gegevensstromen naar de doelaccount verwijderen.
>&#x200B;>Als u bestaande gegevensstromen wilt verwijderen, raadpleegt u de volgende pagina&#39;s:
>
>* [&#x200B; gebruik Experience Platform UI &#x200B;](../ui/delete-destinations.md) om bestaande dataflows te schrappen;
>* [&#x200B; Gebruik de Dienst API van de Stroom &#x200B;](delete-destination-dataflow.md) om bestaande dataflows te schrappen.

Zodra u een verbindings-id hebt en ervoor hebt gezorgd dat er geen gegevensstromen naar de doelaccount bestaan, voert u een DELETE-aanvraag uit naar de [!DNL Flow Service] API.

**API formaat**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` -waarde voor de verbinding die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst. U kunt de verwijdering bevestigen door een opzoekverzoek (GET) in te dienen bij de verbinding. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de doelaccount is verwijderd.

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het Experience Platform API-foutbericht. Verwijs naar [&#x200B; API statuscodes &#x200B;](../../landing/troubleshooting.md#api-status-codes) en [&#x200B; de fouten van de verzoekkopbal &#x200B;](../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de [!DNL Flow Service] API gebruikt om bestaande doelaccounts te verwijderen. Voor meer informatie bij het gebruiken van bestemmingen, verwijs naar het [&#x200B; overzicht van bestemmingen &#x200B;](/help/destinations/home.md).