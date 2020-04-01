---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Identiteitskaarten weergeven
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Identiteitskaarten weergeven

Een toewijzing is een verzameling van alle identiteiten in een cluster, voor een opgegeven naamruimte.

## Een identiteitstoewijzing voor één identiteit ophalen

Als u een identiteit opgeeft, haalt u alle verwante identiteiten op uit dezelfde naamruimte als de identiteit in het verzoek.

**API-indeling**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Verzoek**

Optie 1: Geef de identiteit op als naamruimte (`nsId`, op ID) en als waarde voor ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 2: Geef de identiteit op als naamruimte (`ns`, op naam) en als id-waarde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 3: Geef de identiteit op als XID (`xid`). Zie de sectie van dit document over het ophalen van de XID voor een identiteit voor meer informatie over het ophalen van de XID [voor een identiteit](./list-native-id.md)van een identiteit.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Identiteitskaarten ophalen voor meerdere identiteiten

Gebruik de `POST` methode als een batchequivalent van de hierboven beschreven `GET` methode om toewijzingen voor meerdere identiteiten op te halen.

>[!NOTE] Het verzoek mag niet meer dan 1000 identiteiten bevatten. Verzoeken die langer zijn dan 1000 identiteiten, resulteren in 400 statuscode.

**API-indeling**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Aanvragingsinstantie**

Optie 1: Geef een lijst op met XID&#39;s waarvoor toewijzingen moeten worden opgehaald.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Optie 2: Geef een lijst met identiteiten op als samengestelde id&#39;s, waarbij elke naam de id-waarde en naamruimte bevat via naamruimte-id. In dit voorbeeld wordt het gebruik van deze methode getoond terwijl de standaardinstelling `graph-type` &quot;Privégrafiek&quot; wordt overschreven.

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**Verzoek**

**XID&#39;s gebruiken**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**UID&#39;s gebruiken**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
            "compositeXids": [{
                    "nsid": 411,
                    "id": "WRbM7AAAAJ_PBZHl"
                },
                {
                    "nsid": 411,
                    "id": "WY-RNgAAArI4rGBo"
                }
            ],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

Als er geen verwante identiteiten zijn gevonden met de opgegeven invoer, wordt een `HTTP 204` antwoordcode geretourneerd zonder inhoud.

**Antwoord**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: De tijdstempel wanneer de invoeridentiteit voor het laatst aan deze identiteit is gekoppeld.
- `regions`: Verstrekt `regionId` en `lastAssociationTime` voor waar de identiteit werd gezien.

## Volgende stappen

Ga naar de volgende zelfstudie om beschikbare naamruimten [weer te geven](./list-namespaces.md).
