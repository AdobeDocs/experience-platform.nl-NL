---
keywords: Experience Platform;thuis;populaire onderwerpen;identiteit;Identiteit
solution: Experience Platform
title: Identiteitskoppelingen weergeven
description: Een toewijzing is een verzameling van alle identiteiten in een cluster, voor een opgegeven naamruimte.
role: Developer
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Identiteitskaarten weergeven

Een toewijzing is een verzameling van alle identiteiten in een cluster, voor een opgegeven naamruimte.

## Een identiteitstoewijzing voor één identiteit ophalen

Als u een identiteit opgeeft, haalt u alle verwante identiteiten op uit dezelfde naamruimte als de identiteit in het verzoek.

**API formaat**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Verzoek**

Optie 1: Verstrek de identiteit als namespace (`nsId`, door identiteitskaart) en waarde van identiteitskaart (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 2: Verstrek de identiteit als namespace (`ns`, door naam) en waarde van identiteitskaart (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 3: Geef de identiteit op als XID (`xid`). Voor meer op hoe te om XID van een identiteit te verkrijgen, zie de sectie van dit document die [&#x200B; behandelt die XID voor een identiteit &#x200B;](./list-native-id.md) krijgen.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Identiteitskaarten ophalen voor meerdere identiteiten

Gebruik de methode `POST` als een batchequivalent van de hierboven beschreven methode `GET` om toewijzingen voor meerdere identiteiten op te halen.

>[!NOTE]
>
>Het verzoek mag niet meer dan 1000 identiteiten bevatten. Verzoeken die langer zijn dan 1000 identiteiten, resulteren in 400 statuscode.

**API formaat**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**het lichaam van het Verzoek**

Optie 1: Geef een lijst op met XID&#39;s waarvoor u toewijzingen wilt ophalen.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Optie 2: Geef een lijst met identiteiten op als samengestelde id&#39;s, waarbij elke naam de ID-waarde en naamruimte bevat via naamruimte-id. In dit voorbeeld wordt het gebruik van deze methode getoond terwijl de standaardwaarde `graph-type` van &quot;Privégrafiek&quot; wordt overschreven.

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

**Gebruikend XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Gebruikend UIDs**

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

Als er geen verwante identiteiten zijn gevonden met de opgegeven invoer, wordt een `HTTP 204` -antwoordcode zonder inhoud geretourneerd.

**Reactie**

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

- `lastAssociationTime`: De tijdstempel op het moment dat de invoeridentiteit voor het laatst aan deze identiteit is gekoppeld.
- `regions` - Geeft de `regionId` en `lastAssociationTime` aan waar de identiteit werd gezien.

## Volgende stappen

Ga aan het volgende leerprogramma te werk aan [&#x200B; lijst beschikbare namespaces &#x200B;](./list-namespaces.md).
