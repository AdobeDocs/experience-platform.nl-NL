---
title: Start gegevensstroom opnieuw mislukt
description: Leer hoe u mislukte dataflow-uitvoering opnieuw kunt proberen met de Flow Service API.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---

# Opnieuw mislukte gegevensstroomuitvoering

>[!IMPORTANT]
>
>Ondersteuning voor het opnieuw proberen van mislukte dataflow-run is beschikbaar voor batchbronnen. U kunt alleen dataflow-runtime opnieuw proberen als deze is mislukt.

In deze zelfstudie worden de stappen beschreven voor het opnieuw proberen van mislukte dataflow-uitvoering met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../landing/api-guide.md).

## Een mislukte gegevensstroomuitvoering opnieuw proberen

Als u een mislukte gegevensstroomuitvoering opnieuw wilt proberen, vraagt u een POST aan de `/runs` eindpunt terwijl het verstrekken van runtime identiteitskaart van uw gegevensstroom en `re-trigger` bewerking als onderdeel van uw queryparameters.

**API-indeling**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parameter | Beschrijving |
| --- | --- |
| `{RUN_ID}` | De runtime-id die overeenkomt met de dataflow-run die u opnieuw wilt proberen. |
| `op` | Een bewerking die de uit te voeren actie bepaalt. Als u een mislukte gegevensstroomuitvoering opnieuw wilt proberen, moet u `re-trigger` als uw bewerking. |

**Verzoek**

>[!NOTE]
>
>U kunt de `re-trigger` De verrichting om succesvolle dataflow opnieuw te proberen loopt eveneens, gegeven dat de succesvolle dataflow looppas nul ingebed verslagen heeft.

De volgende aanvraag probeert de dataflow-run opnieuw voor de runtime-id `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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
