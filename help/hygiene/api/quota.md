---
title: Quota API-eindpunt
description: Met het /quota-eindpunt in de Data Hygiene-API kunt u het gebruik van Advanced Data Lifecycle Management controleren op basis van de maandelijkse quotalimieten van uw organisatie voor elk taaktype.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 4d34ae1885f8c4b05c7bb4ff9de9c0c0e26154bd
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Quota-eindpunt

Met het `/quota` -eindpunt in de Data Hygiene-API kunt u het gebruik van Advanced Data Lifecycle Management controleren op basis van de quota van uw organisatie voor elk taaktype.

Het quotagebruik wordt bijgehouden voor elk taaktype van de Levenscyclus van Gegevens. Uw huidige quota&#39;s zijn afhankelijk van de machtigingen van uw organisatie en kunnen regelmatig worden herzien. Verlopen van gegevenssets zijn onderworpen aan een harde limiet voor het aantal taken die tegelijkertijd actief zijn.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Alvorens verder te gaan, te herzien gelieve het [ overzicht ](./overview.md) voor de volgende informatie:

* Koppelingen naar gerelateerde documentatie
* Een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document
* Belangrijke informatie over de vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API te maken

## Quoten en verwerkingstijdlijnen {#quotas}

Aanvragen voor het verwijderen van records zijn onderhevig aan quota&#39;s en verwachtingen op serviceniveau op basis van uw licentierechten. Deze limieten gelden voor verwijderingsaanvragen voor zowel de gebruikersinterface als de API.

>[!TIP]
> 
>In dit document wordt weergegeven hoe u uw gebruik kunt afstemmen op op op machtigingen gebaseerde limieten. Voor een volledige beschrijving van quotalagen, registreert schrappingsaanspraken, en het gedrag van SLA, zie [ op UI-Gebaseerd verslag schrapping ](../ui/record-delete.md#quotas) of [ op API-Gebaseerd verslag schrapt ](./workorder.md#quotas) documenten.

## Quota weergeven {#list}

U kunt de quotagegevens van uw organisatie weergeven door een GET-aanvraag in te dienen bij het `/quota` -eindpunt.

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
      "quota": 1000000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 2000000
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
| -------- | ------- |
| `quotas` | Hiermee geeft u de quotumgegevens weer voor elk taaktype van de levenscyclus van de gegevens. Elk quotaobject bevat de volgende eigenschappen:<ul><li>`name`: Het taaktype van de gegevenslevenscyclus:<ul><li>`expirationDatasetQuota`: Verlopen gegevensset</li><li>`deleteIdentityWorkOrderDatasetQuota`: record verwijdert</li></ul></li><li>`description`: Een beschrijving van het taaktype van de gegevenslevenscyclus.</li><li>`consumed`: Het aantal taken van dit type wordt uitgevoerd in de huidige periode. De objectnaam geeft de contingentperiode aan.</li><li>`quota`: De toewijzing voor dit taaktype voor uw organisatie. Voor het verwijderen en bijwerken van records geeft het quotum het aantal banen weer dat voor elke maandelijkse periode kan worden uitgevoerd. Voor gegevenssetvervaldatums, vertegenwoordigt het quotum het aantal banen die op om het even welk bepaald ogenblik gelijktijdig actief kunnen zijn.</li></ul> |
