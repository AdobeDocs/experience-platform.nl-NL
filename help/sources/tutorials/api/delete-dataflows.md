---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;API;api;delete;delete dataflows
solution: Experience Platform
title: Een DataFlow verwijderen met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u batch- en streaming-gegevensstromen verwijdert met de Flow Service API.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Een gegevensstroom verwijderen met de Flow Service API

U kunt batch- en streaming-gegevensstromen verwijderen die fouten bevatten of die verouderd zijn met de opdracht [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

In deze zelfstudie worden de stappen beschreven voor het verwijderen van gegevensstromen die zijn gemaakt met zowel batch- als streaming bronnen via [!DNL Flow Service].

## Aan de slag

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom-id hebt, selecteert u de gewenste connector in het menu [overzicht van bronnen](../../home.md) en voer de stappen uit die zijn beschreven voordat u deze zelfstudie uitvoert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

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
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst. U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan dataflow te proberen. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de gegevensstroom is verwijderd.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht [!DNL Flow Service] API om een bestaande gegevensstroom te verwijderen.

Raadpleeg de zelfstudie voor informatie over het uitvoeren van deze bewerkingen in de gebruikersinterface. [verwijderen, gegevensstromen in de gebruikersinterface](../../tutorials/ui/delete.md)
