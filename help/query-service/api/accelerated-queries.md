---
title: Eindpunt van versnelde query's
description: Leer hoe te om tot vraag versnelde opslag op een stateless manier toegang te hebben om resultaten snel terug te keren die op bijeengevoegde gegevens worden gebaseerd. Dit document verstrekt een verzoek en een antwoord van steekproefHTTP voor het versnelde-vragen van de Dienst van de Vraag eindpunt.
source-git-commit: 2a9d40fc783feb78a1d5ad7eb615ceb40097eb89
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Versnelde vragen eindpunt

Als onderdeel van de Data Distiller SKU [Query Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/) staat u toe om stateless vragen aan de versnelde opslag te maken. De geretourneerde resultaten zijn gebaseerd op geaggregeerde gegevens. Door de afgenomen latentie van de resultaten is een meer interactieve uitwisseling van informatie mogelijk. De API&#39;s voor versnelde query&#39;s worden ook gebruikt om [door de gebruiker gedefinieerde dashboards](../../dashboards/user-defined-dashboards.md).

Voordat u verdergaat met deze handleiding, moet u controleren of u de [API-handleiding voor query-service](./getting-started.md) om de API van de Query-service met succes te kunnen gebruiken.

## Aan de slag

De gegevens Distiller SKU wordt vereist om de vraag versnelde opslag te gebruiken. Zie de [verpakking](../packages.md), [guardrails](../guardrails.md#query-accelerated-store), en [licenties](../data-distiller/licence-usage.md) documentatie die betrekking heeft op de gegevens Distiller SKU. Als u geen gegevens Distiller SKU hebt, kunt u voor meer informatie contact opnemen met een medewerker van de klantenservice van de Adobe.

In de volgende secties worden de API-aanroepen beschreven die nodig zijn om de versnelde opslag zonder status te openen via de API voor Query-service. Elke vraag omvat het algemene API formaat, een steekproefverzoek die vereiste kopballen toont, en een steekproefreactie.

## Een versnelde query uitvoeren {#run-accelerated-query}

Voer een verzoek van de POST in aan de `/accelerated-queries` eindpunt om een versnelde vraag in werking te stellen. De vraag is of bevat direct in de verzoeklading of van verwijzingen voorzien met een malplaatjeidentiteitskaart

**API-indeling**

```shell
POST /accelerated-queries
```

### Verzoek

>[!IMPORTANT]
>
>Verzoeken aan de `/accelerated-queries` voor het eindpunt is een SQL-instructie OF een sjabloon-id vereist, maar niet beide. Als u beide bestanden in een aanvraag indient, treedt er een fout op.

Het volgende verzoek legt een SQL vraag in het verzoeklichaam aan de versnelde opslag voor.

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
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
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
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
| `dbName` | De naam van de database waarnaar u een versnelde query uitvoert. De waarde voor `dbName` moet het formaat van `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. De opgegeven database moet aanwezig zijn in de versnelde opslag, anders leidt de aanvraag tot een fout. U moet er ook voor zorgen dat de `x-sandbox-name` naam van kop- en sandbox in `dbName` verwijzen naar dezelfde sandbox. |
| `sql` | Een SQL-instructiereeks. De maximale toegestane grootte is 1000000 tekens. |
| `templateId` | De unieke id van een query die is gemaakt en opgeslagen als een sjabloon wanneer een aanvraag voor een POST wordt ingediend bij de `/templates` eindpunt. |
| `name` | Een optionele, beschrijvende naam voor de versnelde query. |
| `description` | Een optionele opmerking over de intentie van de query om andere gebruikers te helpen bij het begrijpen van het doel ervan. De maximale toegestane grootte is 1000 bytes. |

**Antwoord**

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
| `resultsMeta._adhoc.meta:xdmType` | Dit is een door het systeem gegenereerde waarde voor het XDM-veldtype. Raadpleeg de documentatie over de beschikbare typen voor meer informatie over de beschikbare typen [beschikbare XDM-typen](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html). |
| `resultsMeta._adhoc.properties` | Dit zijn de kolomnamen van de gevraagde dataset. |
| `resultsMeta._adhoc.results` | Dit zijn de rijnamen van de gevraagde dataset. Ze weerspiegelen elk van de geretourneerde kolommen. |

