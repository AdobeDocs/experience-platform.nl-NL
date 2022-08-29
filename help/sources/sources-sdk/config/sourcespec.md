---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Bronspecificaties configureren voor Self-Serve Sources (Batch SDK)
topic-legacy: overview
description: Dit document biedt een overzicht van de configuraties die u moet voorbereiden om Self-Serve Sources (Batch SDK) te kunnen gebruiken.
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: adaa0e1a63536bc1fdf751eec477e5cda9fd20ae
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 0%

---

# Bronspecificatie voor Self-Serve Bronnen (Batch SDK) configureren

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
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
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
            "host",
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
| `sourceSpec.attributes.spec.properties.bodyParams` | Dit attribuut kan worden gevormd om het lichaam van HTTP door een verzoek van de POST te verzenden. |
| `sourceSpec.attributes.spec.properties.contentPath` | Bepaalt de knoop die de lijst van punten bevat die aan Platform moeten worden opgenomen. Dit kenmerk moet een geldige JSON-padsyntaxis volgen en verwijzen naar een bepaalde array. | De weergave van [sectie aanvullende bronnen](#content-path) voor een voorbeeld van de bron in een inhoudspad. |
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
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Hiermee geeft u het type van het ondersteunde paginatietype voor uw bron weer. | <ul><li>`OFFSET`: Met dit paginatype kunt u de resultaten parseren door een index op te geven vanaf waar de resulterende array moet worden gestart en een limiet op het aantal resultaten.</li><li>`POINTER`: Met dit paginatype kunt u een `pointer` variabele om naar een bepaald punt te richten dat met een verzoek moet worden verzonden. Voor het pagineren van het type aanwijzer is een pad vereist voor de nuttige lading van dat punt naar de volgende pagina.</li><li>`CONTINUATION_TOKEN`: Dit pagineringstype staat u toe om uw vraag of kopbalparameters met een voortzetteken toe te voegen om resterende terugkeergegevens van uw bron terug te winnen, die aanvankelijk niet wegens een vooraf bepaald maximum werd teruggekeerd.</li><li>`PAGE`: Met dit pagineringstype kunt u de queryparameter toevoegen met een pagineringsparameter om gegevens per pagina te doorlopen, te beginnen bij pagina nul.</li><li>`NONE`: Dit pagineringstype kan voor bronnen worden gebruikt die geen van de beschikbare pagineringstypen ondersteunen. Paginatype `NONE` retourneert de volledige reactiegegevens na een aanvraag.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | De naam voor de limiet waarmee de API het aantal records kan opgeven dat op een pagina moet worden opgehaald. | `limit` of `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Het aantal records dat op een pagina moet worden opgehaald. | `limit=10` of `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | De naam van het verschuivingskenmerk. Dit is vereist als pagineringstype is ingesteld op `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | De naam van het attribuut pointer. Hiervoor is een pad nodig naar het kenmerk dat naar de volgende pagina verwijst. Dit is vereist als pagineringstype is ingesteld op `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Bevat parameters die gesteunde het plannen formaten voor uw bron bepalen. De parameters van het programma omvatten `startTime` en `endTime`, beide waarvan u toestaat om specifieke tijdintervallen voor partijlooppas te plaatsen, die dan ervoor zorgt dat de verslagen die in een vorige partijlooppas worden gehaald niet opnieuw worden gehaald. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definieert de naam van de begintijdparameter | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definieert de naam van de eindtijdparameter | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definieert de ondersteunde indeling voor de `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definieert de ondersteunde indeling voor de `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Bepaalt de user-provided parameters om middelwaarden te halen. | Zie de [extra middelen](#user-input) voor een voorbeeld van door de gebruiker ingevoerde parameters voor `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Aanvullende bronnen {#appendix}

In de volgende secties vindt u informatie over extra configuraties die u aan uw `sourceSpec`, inclusief geavanceerde planning en aangepaste schema&#39;s.

### Voorbeeld van een inhoudspad {#content-path}

Hier volgt een voorbeeld van de inhoud van de `contentPath` eigenschap in een [!DNL MailChimp Members] verbindingsspecificatie.

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
        "host": "https://{domain}.api.mailchimp.com",
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

### Verschillende paginatypen voor uw bron configureren {#pagination}

Hieronder volgen voorbeelden van andere paginatietypen die worden ondersteund door Self-Serve Sources (Batch SDK):

#### `CONTINUATION_TOKEN`

Een voortzetteken type van paginering keert een koordteken terug dat het bestaan van meer punten aangeeft die niet konden worden teruggekeerd, wegens een vooraf bepaald maximumaantal punten die in één enkele reactie kunnen worden teruggekeerd.

Een bron die het type van voortzetteken van paginering steunt kan een pagineringsparameter gelijkend op hebben:

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `type` | Het type paginering dat wordt gebruikt om gegevens te retourneren. |
| `continuationTokenPath` | De waarde die aan de vraagparams moet worden toegevoegd om naar de volgende pagina van de teruggekeerde resultaten te bewegen. |
| `parameterType` | De `parameterType` eigenschap bepaalt waar de `parameterName` moet worden toegevoegd. De `QUERYPARAM` het type staat u toe om uw vraag met toe te voegen `parameterName`. De `HEADERPARAM` staat u toe om uw `parameterName` naar uw headerverzoek. |
| `parameterName` | De naam van de parameter die wordt gebruikt om het voortzetteken op te nemen. De indeling is als volgt: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | De `delayRequestMillis` bezit in paginering staat u toe om het tarief van verzoeken te controleren die aan uw bron worden gemaakt. Sommige bronnen kunnen een limiet hebben voor het aantal aanvragen dat u per minuut kunt indienen. Bijvoorbeeld: [!DNL Zendesk] heeft een limiet van 100 verzoeken per minuut en definieert  `delayRequestMillis` tot `850` staat u toe om de bron te vormen om vraag bij enkel rond 80 verzoeken per minuut, goed onder het 100 verzoek per minieme drempel te maken. |

Hieronder ziet u een voorbeeld van een reactie die wordt geretourneerd met het tokentype voor voortzetting van de paginering:

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

De `PAGE` Door het type paginering kunt u terugkerende gegevens doorlopen op het aantal pagina&#39;s, beginnend bij nul. Wanneer u `PAGE` Typ paginering, u moet het aantal records opgeven dat op één pagina wordt opgegeven.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `type` | Het type paginering dat wordt gebruikt om gegevens te retourneren. |
| `limitName` | De naam voor de limiet waarmee de API het aantal records kan opgeven dat op een pagina moet worden opgehaald. |
| `limitValue` | Het aantal records dat op een pagina moet worden opgehaald. |
| `pageParamName` | De naam van de parameter die u aan vraagparameters moet toevoegen om door verschillende pagina&#39;s van de terugkeergegevens te oversteken. Bijvoorbeeld: `https://abc.com?pageIndex=1` retourneert de tweede pagina van de retourlading van een API. |
| `maximumRequest` | Het maximumaantal verzoeken een bron voor een bepaalde stijgende looppas kan maken. De huidige standaardlimiet is 10000. |

#### `NONE`

De `NONE` pagineringstype kan voor bronnen worden gebruikt die geen van de beschikbare pagineringstypen ondersteunen. Bronnen die het pagineringstype van `NONE` keer eenvoudig alle terugwinnbare verslagen terug wanneer een verzoek van de GET wordt gedaan.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Geavanceerde planning voor Self-Serve Bronnen (Batch SDK)

Vorm incrementele en backfill planning van uw bron gebruikend geavanceerde het plannen. De `incremental` bezit staat u toe om een programma te vormen waarin uw bron slechts nieuwe of gewijzigde verslagen zal opnemen, terwijl het `backfill` Met deze eigenschap kunt u een schema voor het invoeren van historische gegevens maken.

Met geavanceerde het plannen, kunt u uitdrukkingen en functies gebruiken specifiek voor uw bron om stijgende en backfill programma&#39;s te vormen. In het onderstaande voorbeeld wordt [!DNL Zendesk] bron vereist dat het incrementele schema wordt opgemaakt als `type:user updated > {START_TIME} updated < {END_TIME}` en herstellen als `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| Eigenschap | Beschrijving |
| --- | --- |
| `scheduleParams.type` | Het type van het plannen van uw bron zal gebruiken. Deze waarde instellen op `ADVANCE` om het geavanceerde het plannen type te gebruiken. |
| `scheduleParams.paramFormat` | De gedefinieerde indeling van uw planningsparameter. Deze waarde kan gelijk zijn aan de waarde van uw bron `scheduleStartParamFormat` en `scheduleEndParamFormat` waarden. |
| `scheduleParams.incremental` | De incrementele query van uw bron. Incrementeel verwijst naar een innamemethode waarbij alleen nieuwe of gewijzigde gegevens worden opgenomen. |
| `scheduleParams.backfill` | De backfill-query van uw bron. Backfill verwijst naar een innamemethode waarbij historische gegevens worden ingesloten. |

Zodra u uw geavanceerde planning vormt, moet u dan naar uw verwijzen `scheduleParams` in de sectie URL, tekst of koptekstparams, afhankelijk van wat uw specifieke bron ondersteunt. In het onderstaande voorbeeld: `{SCHEDULE_QUERY}` is een placeholder die wordt gebruikt om te specificeren waar de stijgende en backfill het plannen uitdrukkingen zullen worden gebruikt. In het geval van een [!DNL Zendesk] bron, `query` wordt gebruikt in de `queryParams` om geavanceerde planning op te geven.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### Een aangepast schema toevoegen om de dynamische kenmerken van uw bron te definiëren

U kunt een aangepast schema aan uw `sourceSpec` om alle kenmerken te definiëren die nodig zijn voor de bron, inclusief alle dynamische kenmerken die u nodig hebt. U kunt de overeenkomstige verbindingsspecificatie van uw bron bijwerken door een PUT aan te vragen bij de `/connectionSpecs` van het [!DNL Flow Service] API, terwijl het verstrekken van uw douaneschema in `sourceSpec` van uw verbindingsspecificatie.

Hieronder ziet u een voorbeeld van een aangepast schema dat u kunt toevoegen aan de verbindingsspecificatie van uw bron:

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## Volgende stappen

Met uw bevolkte bronspecificaties, kunt u te werk gaan om te vormen onderzoeken specificaties voor de bron die u aan Platform wilt integreren. Het document weergeven op [configureren, verkenningsspecificaties](./explorespec.md) voor meer informatie .
