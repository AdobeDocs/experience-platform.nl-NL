---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;API;api;delete;delete dataflows
solution: Experience Platform
title: Een DataFlow verwijderen met de Flow Service API
type: Tutorial
description: Leer hoe u batch- en streaming-gegevensstromen verwijdert met de Flow Service API.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Een gegevensstroom verwijderen met de Flow Service API

U kunt partij en het stromen dataflows schrappen die fouten bevatten of verouderd zijn geworden gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

In deze zelfstudie worden de stappen beschreven voor het verwijderen van gegevensstromen die met [!DNL Flow Service] zijn gemaakt voor zowel batchbronnen als streamingbronnen.

## Aan de slag

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom identiteitskaart hebt, selecteer uw schakelaar van keus van het [ overzicht van bronnen ](../../home.md) en volg de stappen die vóór het proberen van dit leerprogramma worden geschetst.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../landing/api-guide.md).

## Een gegevensstroom verwijderen

Met een bestaande flow-id kunt u een gegevensstroom verwijderen door een DELETE-aanvraag uit te voeren naar de [!DNL Flow Service] API.

**API formaat**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de gegevensstroom die u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst. U kunt de verwijdering bevestigen door een opzoekverzoek (GET) in te dienen bij de gegevensstroom. De API retourneert een HTTP 404 (Not Found)-fout die aangeeft dat de gegevensstroom is verwijderd.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de [!DNL Flow Service] API gebruikt om een bestaande gegevensstroom te verwijderen.

Voor stappen op hoe te om deze verrichtingen uit te voeren die het gebruikersinterface gebruiken, gelieve te verwijzen naar het leerprogramma op [ het schrappen van dataflows in UI ](../../tutorials/ui/delete.md)
