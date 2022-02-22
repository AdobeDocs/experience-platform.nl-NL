---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Verificatiespecificaties voor Bronnen SDK configureren
topic-legacy: overview
description: Dit document verstrekt een overzicht van de configuraties u moet voorbereiden om Bronnen SDK te gebruiken.
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 4c4c89ab7db7d3546163d707ac80210561c2fa02
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Bronspecificatie voor Bronnen SDK configureren

De bronspecificaties bevatten informatie specifiek voor een bron, met inbegrip van attributen betreffende de categorie van een bron, bètastatus, en cataloguspictogram. Zij bevatten ook nuttige informatie zoals parameters URL, inhoud, kopbal, en programma. De bronspecificaties beschrijven ook het schema van de parameters die worden vereist om een bronverbinding van een basisverbinding tot stand te brengen. Het schema is nodig om een bronverbinding te maken.

Zie de [aanhangsel](#source-spec) voor een voorbeeld van een volledig-bevolkte bronspecificatie.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Eigenschap | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `sourceSpec.attributes` | Bevat informatie over de bron specifiek voor UI of API. |
| `sourceSpec.attributes.uiAttributes` | Geeft informatie weer over de specifieke bron voor de gebruikersinterface. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Een booleaanse eigenschap die erop wijst of de bron meer terugkoppelt van klanten vereist om aan zijn functionaliteit toe te voegen. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definieert de categorie van de bron. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definieert het pictogram dat wordt gebruikt voor het renderen van de bron in de interface van het Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Hiermee geeft u een korte beschrijving van de bron weer. |
| `sourceSpec.attributes.uiAttributes.label` | Toont het etiket dat voor het teruggeven van de bron in Platform UI moet worden gebruikt. |
| `sourceSpec.attributes.spec.properties.urlParams` | Bevat informatie over de het middelweg URL, methode, en gesteunde vraagparameters. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Bepaalt de middelweg van waar te om de gegevens van te halen. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Bepaalt de methode van HTTP die moet worden gebruikt om het verzoek aan het middel te doen om gegevens te halen. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definieert de ondersteunde queryparameters die kunnen worden gebruikt om de bron-URL toe te voegen bij het indienen van een aanvraag om gegevens op te halen. **Opmerking**: Door de gebruiker opgegeven parameterwaarden moeten als plaatsaanduiding worden opgemaakt. Bijvoorbeeld: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` wordt toegevoegd aan de bron-URL als: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Bepaalt kopballen die in het HTTP- verzoek aan bron URL moeten worden verstrekt terwijl het halen van gegevens. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.contentPath` | Bepaalt de knoop die de lijst van punten bevat die aan Platform moeten worden opgenomen. Dit kenmerk moet een geldige JSON-padsyntaxis volgen en verwijzen naar een bepaalde array. | Zie de [aanhangsel](#content-path) voor een voorbeeld van de bron in een inhoudspad. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Het pad dat wijst naar de verzamelingsrecords die aan het Platform moeten worden toegevoegd. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Met deze eigenschap kunt u specifieke items identificeren uit de bron die is geïdentificeerd in het inhoudspad en die moeten worden uitgesloten van het opnemen van inhoud. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Met deze eigenschap kunt u expliciet de afzonderlijke kenmerken opgeven die u wilt behouden. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Met deze eigenschap kunt u de waarde van de kenmerknaam overschrijven die u hebt opgegeven in `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Met deze eigenschap kunt u twee arrays samenvoegen en de brongegevens transformeren naar een Platform-bron. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Het pad dat wijst naar de verzamelingsrecords die u wilt afvlakken. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Dit bezit staat u toe om specifieke punten van het middel te identificeren die in de entiteitweg worden geïdentificeerd die van worden uitgesloten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Met deze eigenschap kunt u expliciet de afzonderlijke kenmerken opgeven die u wilt behouden. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Met deze eigenschap kunt u de waarde van de kenmerknaam overschrijven die u hebt opgegeven in `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definieert de parameters of velden die moeten worden opgegeven voor het ophalen van een koppeling naar de volgende pagina vanuit het huidige paginaantwoord van de gebruiker, of tijdens het maken van een URL voor de volgende pagina. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Hiermee geeft u het type van het ondersteunde paginatietype voor uw bron weer. | <ul><li>`offset`: Met dit paginatype kunt u de resultaten parseren door een index op te geven vanaf waar de resulterende array moet worden gestart en een limiet op het aantal resultaten.</li><li>`pointer`: Met dit paginatype kunt u een `pointer` variabele om naar een bepaald punt te richten dat met een verzoek moet worden verzonden. Voor het paginatype aanwijzer is een pad vereist in laadpad dat naar de volgende pagina verwijst</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | De naam voor de limiet waarmee de API het aantal records kan opgeven dat op een pagina moet worden opgehaald. | `limit` of `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Het aantal records dat op een pagina moet worden opgehaald. | `limit=10` of `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | De naam van het verschuivingskenmerk. Dit is vereist als pagineringstype is ingesteld op `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | De naam van het attribuut pointer. Hiervoor is een pad nodig naar het kenmerk dat naar de volgende pagina verwijst. Dit is vereist als pagineringstype is ingesteld op `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Bevat parameters die gesteunde het plannen formaten voor uw bron bepalen. De parameters van het programma omvatten `startTime` en `endTime`, beide waarvan u toestaat om specifieke tijdintervallen voor partijlooppas te plaatsen, die dan ervoor zorgt dat de verslagen die in een vorige partijlooppas worden gehaald niet opnieuw worden gehaald. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definieert de naam van de begintijdparameter | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definieert de naam van de eindtijdparameter | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definieert de ondersteunde indeling voor de `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definieert de ondersteunde indeling voor de `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Bepaalt de user-provided parameters om middelwaarden te halen. | Zie de [aanhangsel](#user-input) voor een voorbeeld van door de gebruiker ingevoerde parameters voor `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Aanhangsel {#appendix}

### Voorbeeld van een inhoudspad {#content-path}

Hier volgt een voorbeeld van de inhoud van de `contentPath` eigenschap in een [!DNL MailChimp Campaigns] verbindingsspecificatie.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` gebruikersinvoervoorbeeld {#user-input}

Het volgende is een voorbeeld van een door de gebruiker opgegeven `spec.properties` met een [!DNL MailChimp Members] verbindingsspecificatie.

In dit voorbeeld: `listId` wordt verstrekt als onderdeel van `urlParams.path`. Als u moet terugwinnen `listId` van een klant, dan moet u het als deel van ook bepalen `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Voorbeeld van bronspecificatie {#source-spec}

Het volgende is een voltooide bronspecificatie die [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

## Volgende stappen

Met uw bevolkte bronspecificaties, kunt u te werk gaan om te vormen onderzoeken specificaties voor de bron die u aan Platform wilt integreren. Het document weergeven op [configureren, verkenningsspecificaties](./explorespec.md) voor meer informatie .
