---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;delete accounts;delete;api
solution: Experience Platform
title: Een account verwijderen met de Flow Service API
type: Tutorial
description: Leer hoe u een account verwijdert met de Flow Service API.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Een account verwijderen met de Flow Service API

U kunt bronrekeningen schrappen die fouten bevatten of verouderd zijn geworden gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Zie de volgende zelfstudie voor informatie over het verwijderen van een account met de API.

## Aan de slag

Voor deze zelfstudie moet u een geldige verbinding-id hebben. Als u geen geldige verbindingsidentiteitskaart hebt, selecteer uw schakelaar van keus van het [ overzicht van bronnen ](../../home.md) en volg de stappen die alvorens dit leerprogramma te proberen worden geschetst.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).

## Account verwijderen

>[!TIP]
>
>Voordat u de bronaccount verwijdert, moet u eerst bestaande gegevensstromen verwijderen die aan de bronaccount zijn gekoppeld. Om bestaande dataflows te schrappen, verwijs naar het leerprogramma bij [ het schrappen van brondataflows ](./delete-dataflows.md).

Als u een account wilt verwijderen, vraagt u een DELETE aan op de [!DNL Flow Service] API terwijl u de basis-verbindings-id opgeeft die overeenkomt met het account dat u wilt verwijderen.

**API formaat**

```http
DELETE /connections/{BASE_CONNECTION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbindings-id van het bronaccount dat u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan de verbinding te proberen.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de API van [!DNL Flow Service] gebruikt om bestaande accounts te verwijderen.

Voor stappen op hoe te om deze verrichtingen uit te voeren die het gebruikersinterface gebruiken, gelieve te verwijzen naar het leerprogramma op [ het schrappen van rekeningen in UI ](../../tutorials/ui/delete-accounts.md).
