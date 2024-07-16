---
title: Quota API-eindpunt
description: Met het /quota-eindpunt in de Data Hygiene-API kunt u het gebruik van Advanced Data Lifecycle Management controleren op basis van de maandelijkse quotalimieten van uw organisatie voor elk taaktype.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Quota-eindpunt

Met het `/quota` -eindpunt in de Data Hygiene-API kunt u het gebruik van Advanced Data Lifecycle Management controleren op basis van de quota van uw organisatie voor elk taaktype.

De quota&#39;s worden afgedwongen voor elk baantype van de Levenscyclus van Gegevens op de volgende manieren:

* Verwijderen en bijwerken van records is beperkt tot een bepaald aantal aanvragen per maand.
* Dataset-vervaldatums hebben een vaste limiet voor het aantal taken die tegelijkertijd actief zijn, ongeacht wanneer de vervaldatums worden uitgevoerd.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Alvorens verder te gaan, te herzien gelieve het [ overzicht ](./overview.md) voor de volgende informatie:

* Koppelingen naar gerelateerde documentatie
* Een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document
* Belangrijke informatie over de vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API te maken

## Quota weergeven {#list}

U kunt de quotainformatie van uw organisatie bekijken door een verzoek van de GET tot het `/quota` eindpunt te richten.

**API formaat**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUOTA_TYPE}` | Een optionele queryparameter die het type quota opgeeft dat moet worden opgehaald. Als er geen parameter `quotaType` is opgegeven, worden alle quotumwaarden geretourneerd in de API-reactie. Tot de toegestane tekstwaarden behoren:<ul><li>`datasetExpirationQuota`: Dit voorwerp toont het aantal gelijktijdig actieve datasettermijnen voor uw organisatie, en uw totale toelage van verlopen. </li><li>`dailyConsumerDeleteIdentitiesQuota`: Dit object toont het totale aantal verzoeken om record te verwijderen dat uw organisatie vandaag heeft ingediend en uw totale dagvergoeding.<br> Nota: Slechts worden de toegelaten verzoeken geteld. Als een werkorder wordt geweigerd omdat de validatie is mislukt, tellen deze identiteitsverwijderingen niet mee voor uw quota.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: Dit object toont het totale aantal verzoeken om het verwijderen van records dat uw organisatie deze maand heeft ingediend en uw totale maandelijkse toelage.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: Dit object toont het totale aantal aanvragen voor updates van records dat uw organisatie deze maand heeft ingediend en uw totale maandelijkse toelage.</li></ul> |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**Reactie**

Als u met succes reageert, worden de details van de levenscyclusquota van uw gegevens geretourneerd.

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `quotas` | Hiermee geeft u de quotumgegevens weer voor elk taaktype van de levenscyclus van de gegevens. Elk quotaobject bevat de volgende eigenschappen:<ul><li>`name`: Het taaktype van de gegevenslevenscyclus:<ul><li>`expirationDatasetQuota`: Verlopen gegevensset</li><li>`deleteIdentityWorkOrderDatasetQuota`: record verwijdert</li></ul></li><li>`description`: Een beschrijving van het taaktype van de gegevenslevenscyclus.</li><li>`consumed`: Het aantal taken van dit type wordt uitgevoerd in de huidige periode. De objectnaam geeft de contingentperiode aan.</li><li>`quota`: De toewijzing voor dit taaktype voor uw organisatie. Voor het verwijderen en bijwerken van records geeft het quotum het aantal banen weer dat voor elke maandelijkse periode kan worden uitgevoerd. Voor gegevenssetvervaldatums, vertegenwoordigt het quotum het aantal banen die op om het even welk bepaald ogenblik gelijktijdig actief kunnen zijn.</li></ul> |

{style="table-layout:auto"}
