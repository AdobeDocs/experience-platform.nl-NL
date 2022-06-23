---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;API;api;delete;delete doelgegevens verwijderen
solution: Experience Platform
title: Een doelgegevensstroom verwijderen met de Flow Service API
type: Tutorial
description: Leer hoe te om dataflows aan partij en het stromen bestemmingen te schrappen gebruikend de Dienst API van de Stroom.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Een doelgegevensstroom verwijderen met de Flow Service API

U kunt dataflows verwijderen die fouten bevatten of die verouderd zijn met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Deze zelfstudie behandelt de stappen voor het verwijderen van gegevensstromen naar zowel batch- als streaming doelen met behulp van [!DNL Flow Service].

## Aan de slag {#get-started}

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom-id hebt, selecteert u het gewenste doel in het menu [doelcatalogus](../catalog/overview.md) en voert u de volgende stappen uit: [verbinden met de bestemming](../ui/connect-destination.md) en [gegevens activeren](../ui/activation-overview.md) voordat u deze zelfstudie probeert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Doelen](../home.md): [!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om een gegevensstroom met succes te kunnen verwijderen met de opdracht [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Als de `x-sandbox-name` header is niet opgegeven, aanvragen worden opgelost onder de `prod` sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Doelgegevens verwijderen {#delete-destination-dataflow}

Met een bestaande stroom-id kunt u een doelgegevensstroom verwijderen door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API.

**API-indeling**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de doelgegevensstroom die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 202 (Geen inhoud) en een lege hoofdtekst. U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan dataflow te proberen. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de gegevensstroom is verwijderd.

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het API-foutbericht voor Experience Platforms. Zie [API-statuscodes](/help/landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](/help/landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van de Platform voor meer informatie over het interpreteren van foutenreacties.

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u de opdracht [!DNL Flow Service] API om een bestaande gegevensstroom naar een bestemming te verwijderen.

Raadpleeg de zelfstudie voor informatie over het uitvoeren van deze bewerkingen in de gebruikersinterface. [verwijderen, gegevensstromen in de gebruikersinterface](../ui/delete-destinations.md).

Je kunt nu doorgaan en [doelaccounts verwijderen](/help/destinations/api/delete-destination-account.md) met de [!DNL Flow Service] API.
