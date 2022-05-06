---
title: Data Hygiene API (alfa)
description: Leer hoe u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch kunt corrigeren of verwijderen.
hide: true
hidefromtoc: true
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Data Hygiene API (alfa)

>[!IMPORTANT]
>
>De API voor gegevenshygiëne bevindt zich momenteel in alfa en uw organisatie heeft mogelijk nog geen toegang tot deze API. De functionaliteit die in dit document wordt beschreven, kan worden gewijzigd.

Met de API voor gegevenshygiëne kunt u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch corrigeren of verwijderen. In tegenstelling tot de Privacy Service-API hoeven deze bewerkingen niet te worden gekoppeld aan wettelijke privacyregels en kunnen ze alleen worden gebruikt om uw gegevens schoon en nauwkeurig te houden.

U hebt toegang tot de API via het volgende hoofdpad: `https://platform.adobe.io/data/core/hygiene/`

## Aan de slag

Deze sectie verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Hygiene API van Gegevens te maken.

### Waarden verzamelen voor vereiste koppen

Om vraag aan de Hygiene API van Gegevens te maken, moet u uw authentificatiegeloofsbrieven eerst verzamelen. Dit zijn dezelfde referenties die worden gebruikt voor toegang tot de Privacy Service-API. Volg de [gids Aan de slag](./api/getting-started.md) voor Privacy Service API om waarden voor elk van de vereiste kopballen voor de API van de Hygiëne van Gegevens te produceren, zoals hieronder getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

### API-voorbeeldaanroepen lezen

Dit document bevat een voorbeeld-API-aanroep om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../landing/api-guide.md#sample-api) in de gids Aan de slag voor Experience Platform APIs.

## Een verwijdertaak maken

U kunt een verwijdertaak maken door een POST aan te vragen.

**API-indeling**

```http
POST /jobs
```

**Verzoek**

De payload van het verzoek heeft een vergelijkbare structuur als een [aanvraag verwijderen in de Privacy Service-API](./api/privacy-jobs.md#access-delete). Het omvat een `users` array waarvan de objecten de gebruikers vertegenwoordigen waarvan de gegevens moeten worden verwijderd.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `companyContexts` | Een array met verificatiegegevens voor uw organisatie. Het moet één object met de volgende eigenschappen bevatten: <ul><li>`namespace`: Moet worden ingesteld op `imsOrgID`.</li><li>`value`: Uw IMS-organisatie-id. Dit is dezelfde waarde als in het dialoogvenster `x-gw-ims-org-id` header.</li></ul> |
| `users` | Een array met een verzameling van ten minste één gebruiker waarvan u de gegevens wilt verwijderen. Elk gebruikersobject bevat de volgende informatie: <ul><li>`key`: Een id voor een gebruiker die wordt gebruikt om de afzonderlijke taak-id&#39;s in de reactiegegevens te kwalificeren. Het is aan te raden een unieke, gemakkelijk identificeerbare tekenreeks voor deze waarde te kiezen, zodat er later naar kan worden verwezen of deze kan worden opgezocht.</li><li>`action`: Een array met de acties die moeten worden uitgevoerd op basis van de gegevens van de gebruiker. Moet één tekenreekswaarde bevatten: `delete`.</li><li>`userIDs`: Een verzameling identiteiten voor de gebruiker. Het aantal identiteiten dat één gebruiker kan hebben, is beperkt tot negen. Elke identiteit bevat de volgende eigenschappen: <ul><li>`namespace`: De [naamruimte identity](../identity-service/namespaces.md) is gekoppeld aan de id. Dit kan een [standaardnaamruimte](./api/appendix.md#standard-namespaces) herkend door Platform, of het kan een aangepaste naamruimte zijn die door uw organisatie wordt gedefinieerd. Het type gebruikte naamruimte moet worden weerspiegeld in het dialoogvenster `type` eigenschap.</li><li>`value`: De identiteitswaarde.</li><li>`type`: Moet worden ingesteld op `standard` als een algemeen erkende naamruimte wordt gebruikt, of `custom` als u een naamruimte gebruikt die door uw organisatie is gedefinieerd.</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvol antwoord geeft de details van de gecreëerde banen terug.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
