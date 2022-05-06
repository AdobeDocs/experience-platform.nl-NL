---
keywords: Experience Platform;home;populaire onderwerpen;een object verwijderen;catalogusservice;api
solution: Experience Platform
title: Een object in de API verwijderen
topic-legacy: developer guide
description: U kunt een object Catalog verwijderen door de id ervan op te geven in het pad van een DELETE-aanvraag.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Een object in de API verwijderen

U kunt een [!DNL Catalog] -object door de id op te geven in het pad van een DELETE-aanvraag.

>[!WARNING]
>
>Wees extra voorzichtig bij het verwijderen van objecten, omdat dit niet ongedaan kan worden gemaakt en onduidelijke wijzigingen kan veroorzaken op andere plaatsen in [!DNL Experience Platform].

**API-indeling**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>De `DELETE /batches/{ID}` is afgekeurd. Als u een batch wilt verwijderen, moet u de opdracht [Batchverwerking-API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type van [!DNL Catalog] te verwijderen object. Geldige objecten zijn: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en een array met de id van de verwijderde dataset. Deze id moet overeenkomen met de id die in de aanvraag voor DELETE is verzonden. Wanneer u een GET-verzoek uitvoert op het verwijderde object, wordt HTTP-status 404 (Niet gevonden) geretourneerd, waarmee wordt bevestigd dat de gegevensset is verwijderd.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Indien niet [!DNL Catalog] objecten komen overeen met de id in uw aanvraag. Mogelijk ontvangt u nog steeds HTTP Status Code 200, maar de responsarray is leeg.
