---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een object verwijderen
topic: developer guide
translation-type: tm+mt
source-git-commit: 85b497d87fcfb54f390302036ce24c98c6dba6ff

---


# Een object verwijderen

U kunt een Catalog-object verwijderen door de id ervan op te geven in het pad van een DELETE-aanvraag.

>[!WARNING] Wees extra voorzichtig wanneer u objecten verwijdert, omdat dit niet ongedaan kan worden gemaakt en elders in het Experience Platform doorbraakwijzigingen kan veroorzaken.

**API-indeling**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden verwijderd. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

Het volgende verzoek schrapt een dataset waarvan identiteitskaart in de verzoekweg wordt gespecificeerd.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en een array met de id van de verwijderde dataset. Deze id moet overeenkomen met de id die in de DELETE-aanvraag is verzonden. Wanneer u een GET-aanvraag uitvoert voor het verwijderde object, wordt HTTP-status 404 (Niet gevonden) geretourneerd, waarmee wordt bevestigd dat de gegevensset is verwijderd.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] Als geen voorwerpen van de Catalogus identiteitskaart aanpassen die in uw verzoek wordt verstrekt, kunt u nog een Code 200 van de Status van HTTP ontvangen, maar de reactierearray zal leeg zijn.
