---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;API;api;delete;delete doelgegevens verwijderen
solution: Experience Platform
title: Een doelgegevensstroom verwijderen met de Flow Service API
type: Tutorial
description: Leer hoe te om dataflows aan partij en het stromen bestemmingen te schrappen gebruikend de Dienst API van de Stroom.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Een doelgegevensstroom verwijderen met de Flow Service API

U kunt dataflows schrappen die fouten bevatten of verouderd zijn geworden gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

In deze zelfstudie worden de stappen beschreven voor het verwijderen van gegevensstromen naar zowel batchbestemmingen als streamingdoelen met [!DNL Flow Service] .

## Aan de slag {#get-started}

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom identiteitskaart hebt, selecteer uw bestemming van keus van de [ bestemmingscatalogus ](../catalog/overview.md) en volg de stappen die aan [ worden geschetst verbinden met de bestemming ](../ui/connect-destination.md) en [ activeren gegevens ](../ui/activation-overview.md) alvorens dit leerprogramma te proberen.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Doelen ](../home.md): [!DNL Destinations] zijn pre-gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.
* [ Sandboxen ](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een gegevensstroom met de API [!DNL Flow Service] te kunnen verwijderen.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Om vraag aan [!DNL Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Als de header `x-sandbox-name` niet is opgegeven, worden aanvragen opgelost onder de sandbox `prod` .

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Doelgegevens verwijderen {#delete-destination-dataflow}

Met een bestaande stroom-id kunt u een doelgegevensstroom verwijderen door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API.

**API formaat**

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

**Reactie**

Een geslaagde reactie retourneert HTTP-status 202 (Geen inhoud) en een lege hoofdtekst. U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan dataflow te proberen. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de gegevensstroom is verwijderd.

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het API-foutbericht voor Experience Platforms. Verwijs naar [ API statuscodes ](/help/landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](/help/landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform voor meer informatie bij het interpreteren van foutenreacties.

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u de [!DNL Flow Service] API gebruikt om een bestaande gegevensstroom naar een doel te verwijderen.

Voor stappen op hoe te om deze verrichtingen uit te voeren die het gebruikersinterface gebruiken, gelieve te verwijzen naar het leerprogramma op [ het schrappen van dataflows in UI ](../ui/delete-destinations.md).

U kunt nu op gaan en [ bestemmingsrekeningen ](/help/destinations/api/delete-destination-account.md) schrappen gebruikend [!DNL Flow Service] API.
