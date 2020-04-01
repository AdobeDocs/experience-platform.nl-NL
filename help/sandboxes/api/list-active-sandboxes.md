---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Actieve sandboxen weergeven voor de huidige gebruiker
topic: developer guide
translation-type: tm+mt
source-git-commit: 982764ae7807e40cbca5ca60c70bf363a271e3c2

---


# Actieve sandboxen weergeven voor de huidige gebruiker

>[!NOTE] In tegenstelling tot andere eindpunten die in Sandbox API worden verstrekt, is dit eindpunt beschikbaar voor alle gebruikers, met inbegrip van die zonder de toegangstoestemmingen van het Beleid Sandbox.

U kunt een lijst maken van de zandbakken die voor de huidige gebruiker actief zijn door een GET verzoek aan het wortel (`/`) eindpunt te doen.

**API-indeling**

```http
GET /
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met sandboxen die actief zijn voor de huidige gebruiker, inclusief details zoals `name`, `title`, `state`en `type`.

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
    ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de sandbox. Wordt gebruikt voor opzoekdoeleinden in API-aanroepen. |
| `title` | De weergavenaam voor de sandbox. |
| `state` | De huidige verwerkingsstatus van de sandbox. De status van een sandbox kan een van de volgende zijn: <ul><li>**maken**: De sandbox is gemaakt, maar wordt nog steeds door het systeem ingericht.</li><li>**actief**: De sandbox wordt gemaakt en actief.</li><li>**mislukt**: Door een fout kon de sandbox niet door het systeem worden ingericht en is deze uitgeschakeld.</li><li>**geschrapt**: De sandbox is handmatig uitgeschakeld.</li></ul> |
| `type` | Het type sandbox, &#39;development&#39; of &#39;production&#39;. |
| `isDefault` | Een Booleaanse eigenschap die aangeeft of deze sandbox de standaardsandbox voor de organisatie is. Dit is doorgaans de productiesandbox. |
| `eTag` | Een id voor een specifieke versie van de sandbox. Deze waarde wordt gebruikt voor versiebeheer en caching-efficiëntie en wordt telkens bijgewerkt wanneer een wijziging in de sandbox wordt aangebracht. |
