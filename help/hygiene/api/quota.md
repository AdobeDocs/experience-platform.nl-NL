---
title: Quota API-eindpunt
description: Het /quota eindpunt in de Hygiene API van Gegevens staat u toe om uw gebruik van de gegevenshygiëne tegen de maandelijkse quotagrenzen van uw organisatie voor elk baantype te controleren.
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 1%

---

# Quota-eindpunt

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die deze producten hebben aangeschaft **Adobe Healthcare Shield** of **Adobe Privacy- en beveiligingsschild**.

De `/quota` Het eindpunt in de Hygiene API van Gegevens staat u toe om uw gebruik van de gegevenshygiëne tegen de quotagrenzen van uw organisatie voor elk baantype te controleren.

Voor elk taaktype voor gegevenshygiëne worden de quota op de volgende manieren gehandhaafd:

* Verwijderen en bijwerken van records is beperkt tot een bepaald aantal aanvragen per maand.
* Dataset-vervaldatums hebben een vaste limiet voor het aantal taken die tegelijkertijd actief zijn, ongeacht wanneer de vervaldatums worden uitgevoerd.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Controleer voordat je doorgaat de [overzicht](./overview.md) voor de volgende informatie:

* Koppelingen naar gerelateerde documentatie
* Een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document
* Belangrijke informatie over vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken

## Quota weergeven {#list}

U kunt de quotumgegevens van uw organisatie bekijken door een verzoek van de GET te richten aan `/quota` eindpunt.

**API-indeling**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUOTA_TYPE}` | Een optionele queryparameter die het type quota opgeeft dat moet worden opgehaald. Indien niet `quotaType` opgegeven, worden alle quota-waarden geretourneerd in de API-reactie. Tot de toegestane tekstwaarden behoren:<ul><li>`expirationDatasetQuota`: Verlopen gegevensset</li><li>`deleteIdentityWorkOrderDatasetQuota`: Opnemen wordt verwijderd</li><li>`fieldUpdateWorkOrderDatasetQuota`: Updates opnemen</li></ul> |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Antwoord**

Als u met succes reageert, worden de details van uw quota voor gegevenshygiëne geretourneerd.

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `quotas` | Hier worden de quota-gegevens voor elk taaktype voor gegevenshygiëne weergegeven. Elk quotaobject bevat de volgende eigenschappen:<ul><li>`name`: Het taaktype voor gegevenshygiëne:<ul><li>`expirationDatasetQuota`: Verlopen gegevensset</li><li>`deleteIdentityWorkOrderDatasetQuota`: Opnemen wordt verwijderd</li></ul></li><li>`description`: Een beschrijving van het taaktype voor gegevenshygiëne.</li><li>`consumed`: Het aantal banen van dit type loopt in de huidige maandelijkse periode.</li><li>`quota`: De quota voor dit taaktype. Voor het verwijderen en bijwerken van records geeft dit het aantal taken aan dat voor elke maandelijkse periode kan worden uitgevoerd. Voor gegevenssetvervaldatums, vertegenwoordigt dit het aantal banen die op om het even welk bepaald ogenblik gelijktijdig actief kunnen zijn.</li></ul> |

{style=&quot;table-layout:auto&quot;}
