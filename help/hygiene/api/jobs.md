---
title: Records verwijderen met de API voor gegevenshygiëne
description: Leer hoe u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch kunt corrigeren of verwijderen.
role: Developer
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Records verwijderen met de API voor gegevenshygiëne

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

Met de API voor gegevenshygiëne kunt u de opgeslagen persoonlijke gegevens van uw klanten in Adobe Experience Platform programmatisch corrigeren of verwijderen.

U kunt tot API door de zelfde wortelweg toegang hebben zoals [ Privacy Service API ](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## Aan de slag

Deze sectie verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Hygiene API van Gegevens te maken.

### Waarden verzamelen voor vereiste koppen

Om vraag aan de Hygiene API van Gegevens te maken, moet u uw authentificatiegeloofsbrieven eerst verzamelen. Dit zijn dezelfde referenties die worden gebruikt voor toegang tot de Privacy Service API. Verwijs naar het [ API overzicht ](./overview.md#getting-started) om waarden voor elk van de vereiste kopballen voor de Hygiene API van Gegevens te produceren, zoals hieronder getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

### API-voorbeeldaanroepen lezen

Dit document bevat een voorbeeld-API-aanroep om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/api-guide.md#sample-api) in de begonnen gids voor Experience Platform APIs te lezen.

## Een verwijdertaak maken

U kunt een verwijdertaak maken door een POST-aanvraag in te dienen.

**API formaat**

```http
POST /jobs
```

**Verzoek**

De verzoeklading is gestructureerd zo aan dat van a [ schrappingsverzoek in Privacy Service API ](../../privacy-service/api/privacy-jobs.md#access-delete). Deze array bevat een array `users` waarvan de objecten de gebruikers vertegenwoordigen waarvan de gegevens moeten worden verwijderd.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
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
| `companyContexts` | Een array met verificatiegegevens voor uw organisatie. Het moet één object met de volgende eigenschappen bevatten: <ul><li>`namespace` : moet worden ingesteld op `imsOrgID` .</li><li>`value`: Uw organisatie-id. Dit is dezelfde waarde die in de `x-gw-ims-org-id` header wordt opgegeven.</li></ul> |
| `users` | Een array die een verzameling van ten minste één gebruiker bevat waarvan u de gegevens wilt verwijderen. Elk gebruikersobject bevat de volgende informatie: <ul><li>`key`: Een id voor een gebruiker die wordt gebruikt om de afzonderlijke taak-id&#39;s in de reactiegegevens te kwalificeren. Het is aan te raden een unieke, gemakkelijk identificeerbare tekenreeks voor deze waarde te kiezen, zodat er later naar kan worden verwezen of deze kan worden opgezocht.</li><li>`action`: Een array met de acties die moeten worden uitgevoerd op basis van de gegevens van de gebruiker. Moet één tekenreekswaarde bevatten: `delete` .</li><li>`userIDs`: Een verzameling identiteiten voor de gebruiker. Het aantal identiteiten dat één gebruiker kan hebben, is beperkt tot negen. Elke identiteit bevat de volgende eigenschappen: <ul><li>`namespace`: De [ identiteit namespace ](../../identity-service/features/namespaces.md) verbonden aan identiteitskaart Dit kan a [ standaardnamespace ](../../privacy-service/api/appendix.md#standard-namespaces) zijn die door Experience Platform wordt erkend, of het kan een douanespatie zijn door uw organisatie wordt bepaald die. Het type van gebruikte naamruimte moet worden weerspiegeld in de eigenschap `type` .</li><li>`value`: De identiteitswaarde.</li><li>`type` - Moet worden ingesteld op `standard` als u een algemeen herkende naamruimte gebruikt, of `custom` als u een naamruimte gebruikt die door uw organisatie is gedefinieerd.</li></ul></li></ul> |

{style="table-layout:auto"}

**Reactie**

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
