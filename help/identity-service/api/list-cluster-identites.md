---
keywords: Experience Platform;home;populaire onderwerpen;lijstidentiteiten;lijstcluster
solution: Experience Platform
title: Alle identiteiten in een cluster weergeven
description: Identiteiten die verwant zijn in een identiteitsgrafiek, ongeacht naamruimte, worden beschouwd als onderdeel van dezelfde "cluster" in die identiteitsgrafiek. De opties hieronder verstrekken de middelen om tot alle clusterleden toegang te hebben.
exl-id: 0fb9eac9-2dc2-4881-8598-02b3053d0b31
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# Alle identiteiten in een cluster weergeven

Identiteiten die verwant zijn in een identiteitsgrafiek, ongeacht naamruimte, worden beschouwd als onderdeel van dezelfde &quot;cluster&quot; in die identiteitsgrafiek. De opties hieronder verstrekken de middelen om tot alle clusterleden toegang te hebben.

## Gekoppelde identiteiten voor één identiteit ophalen

Haal alle clusterleden op voor één identiteit.

U kunt de optionele `graph-type` parameter om de identiteitsgrafiek aan te geven waaruit de cluster moet worden opgehaald. De opties zijn:

- Geen - voer geen identiteitsstitching uit.
- Privégrafiek - Identiteitsstitching uitvoeren op basis van uw persoonlijke identiteitsgrafiek. Indien niet `graph-type` is opgegeven, is dit de standaardinstelling.

**API-indeling**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Verzoek**

Optie 1: De identiteit opgeven als naamruimte (`nsId`, op ID) en ID-waarde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 2: De identiteit opgeven als naamruimte (`ns`, op naam) en ID-waarde (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Optie 3: De identiteit opgeven als XID (`xid`). Zie de sectie over dit document voor meer informatie over het verkrijgen van de XID van een identiteit [XID ophalen voor een identiteit](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Gekoppelde identiteiten voor meerdere identiteiten ophalen

Gebruiken `POST` als equivalent van de partij `GET` hierboven beschreven methode om de identiteiten in de clusters van meerdere identiteiten te retourneren.

>[!NOTE]
>
>Het verzoek mag niet meer dan 1000 identiteiten bevatten. Verzoeken die langer zijn dan 1000 identiteiten, resulteren in 400 statuscode.

**API-indeling**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Verzoek**

Het volgende verzoek toont het verstrekken van een lijst van XIDs aan waarvoor om clusterleden terug te winnen.

**Studieverzoek**

Gebruik van `x-uis-cst-ctx: stub` header retourneert een onderbroken reactie. Dit is een tijdelijke oplossing om de snelle vooruitgang van de integratieontwikkeling te vergemakkelijken, terwijl de diensten worden voltooid. Dit wordt vervangen wanneer het niet meer nodig is.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Bellen met XID&#39;s**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}' | json_pp
```

**Aanroepen met UID&#39;s**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Antwoord**

**&#39;Stubbed&#39;-respons**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**Volledige respons**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>De reactie zal altijd één ingang voor elke XID hebben die in het verzoek wordt verstrekt ongeacht of XIDs van een verzoek tot de zelfde cluster behoren of als één of meerdere om het even welke cluster verbonden bij allen hebben.

## Volgende stappen

Ga naar de volgende zelfstudie om [lijst van de clustergeschiedenis van een identiteit](./list-cluster-history.md)
