---
keywords: Experience Platform;thuis;populaire onderwerpen;de stroomdienst;
title: Start gegevensstroom opnieuw mislukt
description: Deze zelfstudie behandelt stappen voor het opnieuw proberen van mislukte dataflow-uitvoering met behulp van de Flow Service API
source-git-commit: dfb95f457d7ddb730950159165ed85b2f532f9ab
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Opnieuw mislukte gegevensstroomuitvoering

>[!IMPORTANT]
>
>Ondersteuning voor het opnieuw proberen van mislukte dataflow-run is beschikbaar voor batchbronnen. U kunt alleen dataflow-runtime opnieuw proberen als deze is mislukt.

In deze zelfstudie worden de stappen beschreven voor het opnieuw proberen van mislukte dataflow-uitvoering met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

## Een mislukte gegevensstroomuitvoering opnieuw proberen

Als u een mislukte gegevensstroomuitvoering opnieuw wilt proberen, vraagt u een POST aan de `/runs` eindpunt terwijl het verstrekken van runtime identiteitskaart van uw gegevensstroom en `re-trigger` verrichting als deel van uw vraagparameters.

**API-indeling**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parameter | Beschrijving |
| --- | --- |
| `{RUN_ID}` | De runtime-id die overeenkomt met de dataflow-run die u opnieuw wilt proberen. |
| `op` | Een bewerking die de uit te voeren actie bepaalt. Als u een mislukte gegevensstroomuitvoering opnieuw wilt proberen, moet u `re-trigger` als uw bewerking. |

**Verzoek**

De volgende aanvraag probeert de dataflow-run voor de runtime-id opnieuw uit te voeren `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Antwoord**

Een geslaagde reactie retourneert een nieuw gemaakte flow-id en de bijbehorende etag-versie.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
