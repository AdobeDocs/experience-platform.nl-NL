---
title: Quota API-eindpunt
description: Met het /quota-eindpunt in de Data Hygiene-API kunt u het gebruik van Advanced Data Lifecycle Management controleren op basis van de maandelijkse quotalimieten van uw organisatie voor elk taaktype.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---

# Quota-eindpunt

Gebruik het `/quota` eindpunt in de API van de Hygiëne van Gegevens om het huidige gebruik en de grenzen van uw organisatie te controleren. De quota variëren op basis van rechten, zoals privacy en beveiligingsschild of gezondheidsschild.

Controleer uw huidige quotagebruik om naleving van organisatorische grenzen voor elk baantype te verzekeren.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Alvorens verder te gaan, te herzien gelieve het [ overzicht ](./overview.md) voor de volgende informatie:

* Gerelateerde documentatiekoppelingen
* Hoe te om steekproefAPI vraag te lezen
* Vereiste headers voor Experience Platform API-aanroepen

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

>[!NOTE]
>
>Het verbruik van de quota stelt dagelijks en maandelijks op de eerste van elke maand bij 00 :00 GMT terug.
>
>Alleen geaccepteerde aanvragen tellen mee voor uw quota. Geweigerde werkorders verlagen uw quota niet.

| Parameter | Beschrijving |
| --- | --- |
| `{QUOTA_TYPE}` | Een optionele queryparameter die het type quota opgeeft dat moet worden opgehaald. Als er geen parameter `quotaType` is opgegeven, worden alle quotumwaarden geretourneerd in de API-reactie. Tot de geaccepteerde waarden behoren:<ul><li>`datasetExpirationQuota`: Het aantal actieve gegevenssetvervaldatums en uw totale toegestane aantal.</li><li>`dailyConsumerDeleteIdentitiesQuota`: Het aantal records dat u vandaag verwijdert en uw dagelijkse quota.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: Deze maand en uw maandquotum worden verwijderd door het aantal records.</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| Eigenschap | Beschrijving |
| -------- | ------- |
| `quotas` | Hiermee geeft u de quotumgegevens weer voor elk taaktype van de levenscyclus van de gegevens. Elk quotaobject bevat de volgende eigenschappen:<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | De id voor het contingenttype. |
| `description` | Een beschrijving van de grenzen van dit contingent. |
| `consumed` | De hoeveelheid quota die momenteel wordt verbruikt. De verbruikte hoeveelheid stelt op de eerste van de maand bij 00 :00 GMT en 00 :00 GMT voor dagelijkse quota terug. |
| `quota` | De maximale toewijzing van dit contingenttype voor uw organisatie. |
