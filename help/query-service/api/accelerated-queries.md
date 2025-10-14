---
title: Eindpunt van versnelde query's
description: Leer hoe te om tot vraag versnelde opslag op een stateless manier toegang te hebben om resultaten snel terug te keren die op bijeengevoegde gegevens worden gebaseerd. Dit document verstrekt een verzoek en een antwoord van steekproefHTTP voor het versnelde-vragen van de Dienst van de Vraag eindpunt.
role: Developer
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Versnelde vragen eindpunt

Als deel van Gegevens Distiller SKU, staat de [&#x200B; Dienst API van de Vraag &#x200B;](https://developer.adobe.com/experience-platform-apis/references/query-service/) u toe om stateless vragen aan de versnelde opslag te maken. De geretourneerde resultaten zijn gebaseerd op geaggregeerde gegevens. Door de afgenomen latentie van de resultaten is een meer interactieve uitwisseling van informatie mogelijk. Versnelde vragen APIs wordt ook gebruikt aan macht [&#x200B; user-defined dashboards &#x200B;](../../dashboards/standard-dashboards.md).

Alvorens met deze gids verder te gaan, zorg ervoor dat u de [&#x200B; gids van de Dienst API van de Vraag &#x200B;](./getting-started.md) gelezen en begrepen hebt om de Dienst API van de Vraag met succes te gebruiken.

## Aan de slag

De gegevens Distiller SKU wordt vereist om de vraag versnelde opslag te gebruiken. Gelieve te zien het [&#x200B; verpakken &#x200B;](../packaging.md) en [&#x200B; guardrails &#x200B;](../guardrails.md#query-accelerated-store), en [&#x200B; verlenen van vergunningen &#x200B;](../data-distiller/license-usage.md) documentatie die op het SKU van Gegevens Distiller betrekking heeft. Als u geen gegevens hebt Distiller SKU gelieve uw vertegenwoordiger van de klantendienst van de Adobe voor meer informatie te contacteren.

In de volgende secties worden de API-aanroepen beschreven die nodig zijn om de versnelde opslag zonder status te openen via de API voor Query-service. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

## Een versnelde query uitvoeren {#run-accelerated-query}

Maak een verzoek van de POST aan het `/accelerated-queries` eindpunt om een versnelde vraag in werking te stellen. De vraag is of bevat direct in de verzoeklading of van verwijzingen voorzien met een malplaatjeidentiteitskaart

**API formaat**

```shell
POST /accelerated-queries
```

### Verzoek

>[!IMPORTANT]
>
>Voor aanvragen naar het eindpunt van `/accelerated-queries` is een SQL-instructie OF een sjabloon-id vereist, maar niet beide. Als u beide bestanden in een aanvraag indient, treedt er een fout op.

Het volgende verzoek legt een SQL vraag in het verzoeklichaam aan de versnelde opslag voor.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

Dit afwisselende verzoek legt een malplaatjeidentiteitskaart in het verzoeklichaam aan de versnelde opslag voor. SQL van het overeenkomstige malplaatje wordt gebruikt om de versnelde opslag te vragen.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/accelerated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| Eigenschap | Beschrijving |
|---|---|
| `dbName` | De naam van de database waarnaar u een versnelde query uitvoert. De waarde voor `dbName` moet de notatie `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}` hebben. De opgegeven database moet aanwezig zijn in de versnelde opslag, anders leidt de aanvraag tot een fout. U moet er ook voor zorgen dat de naam van de `x-sandbox-name` -header en -sandbox in `dbName` naar dezelfde sandbox verwijst. |
| `sql` | Een SQL-instructiereeks. De maximale toegestane grootte is 1000000 tekens. |
| `templateId` | De unieke id van een query die is gemaakt en opgeslagen als een sjabloon wanneer een aanvraag voor een POST wordt ingediend bij het `/templates` -eindpunt. |
| `name` | Een optionele, beschrijvende naam voor de versnelde query. |
| `description` | Een optionele opmerking over de intentie van de query om andere gebruikers te helpen bij het begrijpen van het doel ervan. De maximale toegestane grootte is 1000 bytes. |

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 met het ad-hocschema dat door de query is gemaakt.

>[!NOTE]
>
>De volgende reactie is afgebroken voor de beknoptheid.

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| Eigenschap | Beschrijving |
|---|---|
| `queryId` | De id-waarde van de gemaakte query. |
| `resultsMeta` | Dit object bevat de metagegevens voor elke kolom die in de resultaten wordt geretourneerd, zodat gebruikers de naam en het type van elke kolom weten. |
| `resultsMeta._adhoc` | Een ad-hoc schema van de Gegevens van de Ervaring Model (XDM) met gebieden die namespaced voor gebruik slechts door één enkele dataset zijn. |
| `resultsMeta._adhoc.type` | Het gegevenstype van het ad-hocschema. |
| `resultsMeta._adhoc.meta:xdmType` | Dit is een systeemgegenereerde waarde voor het XDM-veldtype. Voor meer informatie over de beschikbare types zie de documentatie over [&#x200B; beschikbare types XDM &#x200B;](../../xdm/tutorials/custom-fields-api.md). |
| `resultsMeta._adhoc.properties` | Dit zijn de kolomnamen van de gevraagde dataset. |
| `resultsMeta._adhoc.results` | Dit zijn de rijnamen van de gevraagde dataset. Ze weerspiegelen elk van de geretourneerde kolommen. |
