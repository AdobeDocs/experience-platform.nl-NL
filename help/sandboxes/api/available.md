---
keywords: Experience Platform;home;populaire onderwerpen;lijst beschikbare sandboxen;lijst sandboxen
solution: Experience Platform
title: Beschikbaar API-eindpunt voor sandboxen
topic-legacy: developer guide
description: U kunt een lijst maken van de sandboxen die beschikbaar zijn voor de huidige gebruiker door een GET-aanvraag in te dienen bij het beschikbare sandboxeindpunt.
exl-id: 9b0719af-c1ca-439a-9c8b-86c7fa26a3b8
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Beschikbaar sandboxeindpunt

>[!NOTE]
>
>In tegenstelling tot andere eindpunten die in Sandbox API worden verstrekt, is dit eindpunt beschikbaar voor alle gebruikers, met inbegrip van die zonder de toegangstoestemmingen van het Beleid Sandbox.

U kunt een lijst maken van de sandboxen die beschikbaar zijn voor de huidige gebruiker door een GET-aanvraag in te dienen bij het beschikbare sandboxeindpunt.

**API-indeling**

```http
GET /{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Optionele queryparameters om resultaten te filteren op. Zie [appendix document](./appendix.md#query) voor een lijst van beschikbare parameters. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/?&limit=3&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een succesvol antwoord retourneert een lijst met sandboxen die beschikbaar zijn voor de huidige gebruiker, inclusief details zoals `name`, `title`, `state` en `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 3,
        "count": 1
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/?limit={limit}&offset={offset}",
            "templated": true
        }
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de sandbox. Wordt gebruikt voor opzoekdoeleinden in API-aanroepen. |
| `title` | De weergavenaam voor de sandbox. |
| `state` | De huidige verwerkingsstatus van de sandbox. De status van een sandbox kan een van de volgende zijn: <ul><li>`creating`: De sandbox is gemaakt, maar wordt nog steeds door het systeem ingericht.</li><li>`active`: De sandbox wordt gemaakt en actief.</li><li>`failed`: Door een fout kon de sandbox niet door het systeem worden ingericht en is deze uitgeschakeld.</li><li>`deleted`: De sandbox is handmatig uitgeschakeld.</li></ul> |
| `type` | Het type sandbox, &#39;development&#39; of &#39;production&#39;. |
| `isDefault` | Een Booleaanse eigenschap die aangeeft of deze sandbox de standaardproductiesandbox voor de organisatie is. |
| `eTag` | Een id voor een specifieke versie van de sandbox. Deze waarde wordt gebruikt voor versiebeheer en caching-efficiëntie en wordt telkens bijgewerkt wanneer een wijziging in de sandbox wordt aangebracht. |
