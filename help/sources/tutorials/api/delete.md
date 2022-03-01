---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;delete accounts;delete;api
solution: Experience Platform
title: Een account verwijderen met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u een account verwijdert met de Flow Service API.
exl-id: 3d07ab7d-c012-472e-8db4-b19e3936dcba
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# Een account verwijderen met de Flow Service API

U kunt bronrekeningen schrappen die fouten bevatten of verouderd zijn geworden gebruikend [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Zie de volgende zelfstudie voor informatie over het verwijderen van een account met de API.

## Aan de slag

Voor deze zelfstudie moet u een geldige verbinding-id hebben. Als u geen geldige verbinding-id hebt, selecteert u de gewenste connector in het menu [overzicht van bronnen](../../home.md) en voer de stappen uit die zijn beschreven voordat u deze zelfstudie uitvoert.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

## Account verwijderen

>[!TIP]
>
>Voordat u de bronaccount verwijdert, moet u eerst bestaande gegevensstromen verwijderen die aan de bronaccount zijn gekoppeld. Raadpleeg de zelfstudie over het verwijderen van bestaande gegevensstromen [gegevensstroom bronnen verwijderen](./delete-dataflows.md).

Als u een account wilt verwijderen, vraagt u een DELETE aan de [!DNL Flow Service] API terwijl het verstrekken van de identiteitskaart van de basisverbinding die met de rekening beantwoordt die u wilt schrappen.

**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en een lege hoofdtekst.

U kunt de schrapping bevestigen door een raadpleging (GET) verzoek aan de verbinding te proberen.

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de opdracht [!DNL Flow Service] API om bestaande accounts te verwijderen.

Raadpleeg de zelfstudie voor informatie over het uitvoeren van deze bewerkingen in de gebruikersinterface. [accounts verwijderen in de gebruikersinterface](../../tutorials/ui/delete-accounts.md).
