---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Clustergeschiedenis van een identiteit ophalen
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# De clustergeschiedenis van een identiteit ophalen

Identiteiten kunnen clusters bewegen tijdens de uitvoering van verschillende apparaatgrafieken. De Dienst van de identiteit verstrekt zicht in de clusterverenigingen van een bepaalde identiteit in tijd.

Gebruik optionele `graph-type` parameter om het uitvoertype aan te geven waaruit de cluster moet worden opgehaald. De opties zijn:

- `None` - Geen identiteitsstitching uitvoeren.
- `Private Graph` - Identiteitsstitching uitvoeren op basis van uw persoonlijke identiteitsgrafiek. Als er geen `graph-type` is opgegeven, is dit de standaardinstelling.

## De clustergeschiedenis van één identiteit ophalen

**API-indeling**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Verzoek**

Optie 1: Geef de identiteit op als naamruimte (`nsId`, op ID) en als waarde voor ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 2: Geef de identiteit op als naamruimte (`ns`, op naam) en als id-waarde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 3: Geef de identiteit op als XID (`xid`). Zie de sectie van dit document over het ophalen van de XID voor een identiteit voor meer informatie over het ophalen van de XID [voor een identiteit](./list-native-id.md)van een identiteit.

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## De clustergeschiedenis van meerdere identiteiten ophalen

Gebruik de `POST` methode als een batchequivalent van de hierboven beschreven `GET` methode om de clusterhistorie van meerdere identiteiten te retourneren.

>[!NOTE] Het verzoek mag niet meer dan 1000 identiteiten bevatten. Verzoeken die langer zijn dan 1000 identiteiten, resulteren in 400 statuscode.

**API-indeling**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Aanvragingsinstantie**

Optie 1: Geef een lijst op met XID&#39;s waarvoor clusterleden moeten worden opgehaald.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Optie 2: Geef een lijst met identiteiten op als samengestelde id&#39;s, waarbij elke naam de ID-waarde en naamruimte bevat via naamruimtecode.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**Verzoek**

**Studieverzoek**

Het gebruik van `x-uis-cst-ctx: stub` koptekst retourneert een onderbroken reactie. Dit is een tijdelijke oplossing om de snelle vooruitgang van de integratieontwikkeling te vergemakkelijken, terwijl de diensten worden voltooid. Dit wordt vervangen wanneer het niet meer nodig is.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**XID&#39;s gebruiken**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**UID&#39;s gebruiken**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
        "graph-type": "Private Graph"
      }' | json_pp
```

**Respompen**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE] De reactie zal altijd één ingang voor elke XID hebben die in het verzoek wordt verstrekt ongeacht of XIDs van een verzoek tot de zelfde cluster behoren of als één of meerdere om het even welke cluster verbonden bij allen hebben.

## Volgende stappen

Ga naar de volgende zelfstudie om [een lijst met identiteitstoewijzingen weer te geven](./list-identity-mappings.md)