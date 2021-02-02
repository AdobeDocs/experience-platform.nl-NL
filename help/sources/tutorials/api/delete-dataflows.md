---
keywords: Experience Platform;home;populaire onderwerpen;flowservice;API;api;delete;delete dataflows
solution: Experience Platform
title: Een gegevensstroom verwijderen met de Flow Service API
topic: overview
type: Tutorial
description: In deze zelfstudie worden de stappen beschreven voor het verwijderen van batch- en streaming-gegevensstromen met behulp van de Flow Service API.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# Een gegevensstroom verwijderen met de Flow Service API

U kunt batch- en streaming gegevensstromen verwijderen die fouten bevatten of die verouderd zijn met de [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

In deze zelfstudie worden de stappen beschreven voor het verwijderen van gegevensstromen die met [!DNL Flow Service] zijn gemaakt voor zowel batchbronnen als streamingbronnen.

## Aan de slag

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom identiteitskaart hebt, selecteer uw schakelaar van keus van [bronnen overzicht](../../home.md) en volg de stappen die alvorens dit leerprogramma te proberen worden geschetst.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om een gegevensstroom met succes te schrappen gebruikend [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Een gegevensstroom verwijderen

Met een bestaande stroom-id kunt u een gegevensstroom verwijderen door een DELETE-verzoek uit te voeren naar de [!DNL Flow Service]-API.

**API-indeling**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id`-waarde voor de gegevensstroom die u wilt verwijderen. |

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

Door deze zelfstudie te volgen, hebt u met succes de [!DNL Flow Service] API gebruikt om een bestaande gegevensstroom te schrappen.

Voor stappen over hoe te om deze verrichtingen uit te voeren gebruikend het gebruikersinterface, gelieve te verwijzen naar het leerprogramma op [het schrappen van gegevensstromen in UI](../../tutorials/ui/delete.md)
