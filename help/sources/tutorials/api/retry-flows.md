---
title: Start gegevensstroom opnieuw mislukt
description: Leer hoe u mislukte dataflow-uitvoering opnieuw kunt proberen met de Flow Service API.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Opnieuw mislukte gegevensstroomuitvoering

>[!IMPORTANT]
>
>Ondersteuning voor het opnieuw proberen van mislukte dataflow-run is beschikbaar voor batchbronnen. U kunt alleen dataflow-runtime opnieuw proberen als deze is mislukt.

Dit leerprogramma behandelt stappen op hoe te om ontbroken dataflow looppas opnieuw te proberen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).

## Een mislukte gegevensstroomuitvoering opnieuw proberen

Als u een mislukte gegevensstroomuitvoering opnieuw wilt proberen, vraagt u een POST naar het `/runs` -eindpunt terwijl u de runtime-id van de gegevensstroom en de `re-trigger` -bewerking opgeeft als onderdeel van de queryparameters.

**API formaat**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Parameter | Beschrijving |
| --- | --- |
| `{RUN_ID}` | De runtime-id die overeenkomt met de dataflow-run die u opnieuw wilt proberen. |
| `op` | Een bewerking die de uit te voeren actie bepaalt. Als u een mislukte gegevensstroomuitvoering opnieuw wilt proberen, moet u `re-trigger` opgeven als uw bewerking. |

**Verzoek**

>[!NOTE]
>
>U kunt de `re-trigger` verrichting gebruiken om succesvolle dataflow looppas ook opnieuw te proberen, aangezien de succesvolle dataflow looppas nul ingebed verslagen heeft.

Met de volgende aanvraag wordt de uitvoering van de gegevensstroom voor de uitvoerings-id `4fb0418e-1804-45d6-8d56-dd51f05c0baf` opnieuw uitgevoerd.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Reactie**

Een geslaagde reactie retourneert een nieuw gemaakte flow-id en de bijbehorende etag-versie.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
