---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;verwijder doelaccounts;delete;api
solution: Experience Platform
title: Een doelaccount verwijderen met de Flow Service API
type: Tutorial
description: Leer hoe u een doelaccount kunt verwijderen met de Flow Service API.
source-git-commit: df89f8ce8050b26068e0ab7aa01f1c964f5d2422
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Een doelaccount verwijderen met de Flow Service API

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

Voordat u gegevens kunt activeren, moet u verbinding maken met de bestemming door eerst een doelaccount in te stellen. Deze zelfstudie behandelt de stappen voor het verwijderen van bestemmingsaccounts die niet meer nodig zijn via het dialoogvenster [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Het verwijderen van doelaccounts wordt momenteel alleen ondersteund in de Flow Service API. Doelaccounts kunnen niet worden verwijderd met de gebruikersinterface van het Experience Platform.

## Aan de slag {#get-started}

Voor deze zelfstudie moet u een geldige verbinding-id hebben. De verbinding-id vertegenwoordigt de accountverbinding met het doel. Als u geen geldige verbinding-id hebt, selecteert u het gewenste doel in het menu [doelcatalogus](../catalog/overview.md) en voert u de volgende stappen uit: [verbinden met de bestemming](../ui/connect-destination.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Doelen](../home.md): [!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om een doelaccount te kunnen verwijderen met de opdracht [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Als de `x-sandbox-name` header is niet opgegeven, aanvragen worden opgelost onder de `prod` sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## De verbinding-id zoeken van de doelaccount die u wilt verwijderen {#find-connection-id}

>[!NOTE]
>Deze zelfstudie gebruikt de [Luchtvaartbestemming](../catalog/mobile-engagement/airship-attributes.md) als voorbeeld, maar de beschreven stappen zijn van toepassing op om het even welk van [beschikbare bestemmingen](../catalog/overview.md).

De eerste stap bij het verwijderen van een doelaccount is om de verbinding-id te achterhalen die overeenkomt met de doelaccount die u wilt verwijderen.

Blader in de gebruikersinterface van het Experience Platform naar **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** en selecteer de account die u wilt verwijderen door het nummer in het dialoogvenster **[!UICONTROL Destinations]** kolom.

![Doelaccount selecteren om te verwijderen](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Vervolgens kunt u de verbinding-id van het doelaccount ophalen via de URL in uw browser.

![Verbindings-id ophalen van URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "imsOrgId": "{IMS_ORG}",
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
>Als u bestaande gegevensstromen wilt verwijderen, raadpleegt u de volgende pagina&#39;s:
>* [De gebruikersinterface van het Experience Platform gebruiken](../ui/delete-destinations.md) bestaande gegevensstromen te verwijderen;
>* [De Flow Service-API gebruiken](delete-destination-dataflow.md) om bestaande gegevensstromen te schrappen.


Zodra u een verbindings identiteitskaart hebt en ervoor gezorgd dat geen dataflows aan de bestemmingsrekening bestaan, voer een verzoek van DELETE aan [!DNL Flow Service] API.

**API-indeling**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De unieke `id` waarde voor de verbinding u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst. U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan de verbinding te proberen. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de doelaccount is verwijderd.

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het API-foutbericht voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht [!DNL Flow Service] API om bestaande doelaccounts te verwijderen.
