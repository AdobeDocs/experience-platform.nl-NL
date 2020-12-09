---
keywords: Experience Platform;home;popular topics;flow service;API;api;delete;delete dataflows
solution: Experience Platform
title: Een gegevensstroom verwijderen met de Flow Service API
topic: overview
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het verwijderen van batch- en streaming-gegevensstromen met behulp van de Flow Service API.
translation-type: tm+mt
source-git-commit: b63b17f2a7271fc673abc8245a4917c0daca4ef3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# Een gegevensstroom verwijderen met de Flow Service API

U kunt batch- en streaming-gegevensstromen verwijderen die fouten bevatten of die verouderd zijn met de [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

In deze zelfstudie worden de stappen beschreven voor het verwijderen van gegevensstromen die zijn gemaakt met zowel batchbronnen als streamingbronnen [!DNL Flow Service].

## Aan de slag

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom-id hebt, selecteert u de gewenste connector in het [bronoverzicht](../../home.md) en volgt u de stappen die worden beschreven voordat u deze zelfstudie gaat uitvoeren.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een gegevensstroom met de [!DNL Flow Service] API te kunnen verwijderen.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Een gegevensstroom verwijderen

Met een bestaande stroom-id kunt u een gegevensstroom verwijderen door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API.

**API-indeling**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` waarde voor de gegevensstroom u wilt schrappen. |

**Verzoek**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst. U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan dataflow te proberen. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de gegevensstroom is verwijderd.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de [!DNL Flow Service] API gebruikt om een bestaande gegevensstroom te verwijderen.

Raadpleeg de zelfstudie over het [verwijderen van gegevensstromen in de gebruikersinterface voor informatie over het uitvoeren van deze bewerkingen in de gebruikersinterface.](../../tutorials/ui/delete.md)
