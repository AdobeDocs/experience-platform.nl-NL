---
keywords: Experience Platform;home;populaire onderwerpen;een object verwijderen;catalogusservice;api
solution: Experience Platform
title: Een object in de API verwijderen
description: U kunt een object Catalog verwijderen door de id ervan op te geven in het pad van een DELETE-aanvraag.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Een object in de API verwijderen

U kunt een [!DNL Catalog] -object verwijderen door de id ervan op te geven in het pad van een DELETE-aanvraag.

>[!WARNING]
>
>Wees voorzichtig bij het verwijderen van objecten, omdat dit niet ongedaan kan worden gemaakt en onduidelijke wijzigingen elders in [!DNL Experience Platform] kan veroorzaken.

**API formaat**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Het eindpunt `DELETE /batches/{ID}` is vervangen. Om een partij te schrappen, zou u de [&#x200B; Ingestie API van de Partij moeten gebruiken &#x200B;](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden verwijderd. Geldige objecten zijn: <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

Het volgende verzoek schrapt een dataset waarvan identiteitskaart in de verzoekweg wordt gespecificeerd.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en een array met de id van de verwijderde dataset. Deze id moet overeenkomen met de id die in de aanvraag voor DELETE is verzonden. Wanneer u een GET-verzoek uitvoert op het verwijderde object, wordt HTTP-status 404 (Niet gevonden) geretourneerd, waarmee wordt bevestigd dat de gegevensset is verwijderd.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Als er geen [!DNL Catalog] -objecten overeenkomen met de id die in uw aanvraag is opgegeven, ontvangt u mogelijk nog steeds HTTP Status Code 200, maar is de responsarray leeg.
