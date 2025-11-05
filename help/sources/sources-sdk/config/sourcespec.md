---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
title: Bronspecificaties configureren voor Self-Serve Sources (Batch SDK)
description: Dit document biedt een overzicht van de configuraties die u moet voorbereiden voor het gebruik van Self-Serve Sources (Batch SDK).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 2ff70ee6e4aa7fd723293e66000ccb161d61ab6a
workflow-type: tm+mt
source-wordcount: '2107'
ht-degree: 0%

---

# Bronspecificatie configureren voor Self-Serve Sources (Batch SDK)

Source-specificaties bevatten specifieke informatie over een bron, waaronder kenmerken die betrekking hebben op de categorie van een bron, de bètastatus en het cataloguspictogram. Zij bevatten ook nuttige informatie zoals parameters URL, inhoud, kopbal, en programma. Source-specificaties beschrijven ook het schema met de parameters die nodig zijn om een bronverbinding te maken via een basisverbinding. Het schema is nodig om een bronverbinding te maken.

Zie [ bijlage ](#source-spec) voor een voorbeeld van een volledig-bevolkte bronspecificatie.


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
| `sourceSpec.attributes` | Bevat informatie over de bron specifiek voor UI of API. |  |
| `sourceSpec.attributes.uiAttributes` | Geeft informatie weer over de specifieke bron voor de gebruikersinterface. |  |
| `sourceSpec.attributes.uiAttributes.isPreview` | Een Booleaanse eigenschap die aangeeft of de bron wordt weergegeven als een voorvertoning (niet voor productie/algemene beschikbaarheid). | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.isBeta` | Een Booleaans kenmerk dat aangeeft of de bron meer feedback van klanten vereist om aan de functionaliteit toe te voegen. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definieert de categorie van de bron. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definieert het pictogram dat wordt gebruikt voor het renderen van de bron in de gebruikersinterface van Experience Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Geeft een korte beschrijving van de bron weer. |  |
| `sourceSpec.attributes.uiAttributes.label` | Geeft het label weer dat moet worden gebruikt voor het renderen van de bron in de gebruikersinterface van Experience Platform. |  |
| `sourceSpec.attributes.spec.properties.urlParams` | Bevat informatie over de het middelweg URL, methode, en gesteunde vraagparameters. |  |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Bepaalt de middelweg van waar te om de gegevens van te halen. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Bepaalt de methode van HTTP die moet worden gebruikt om het verzoek aan het middel te doen om gegevens te halen. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definieert de ondersteunde queryparameters die kunnen worden gebruikt om de bron-URL toe te voegen bij het indienen van een aanvraag om gegevens op te halen. **Nota**: Om het even welke user-provided parameterwaarde moet als placeholder worden geformatteerd. Bijvoorbeeld: `${USER_PARAMETER}` . | `"queryParams" : {"key" : "value", "key1" : "value1"}` wordt als volgt aan de bron-URL toegevoegd: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Bepaalt kopballen die in het HTTP- verzoek aan bron URL moeten worden verstrekt terwijl het halen van gegevens. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Dit attribuut kan worden gevormd om het lichaam van HTTP door een POST- verzoek te verzenden. |  |
| `sourceSpec.attributes.spec.properties.contentPath` | Definieert het knooppunt dat de lijst bevat met items die moeten worden opgenomen in Experience Platform. Dit kenmerk moet een geldige JSON-padsyntaxis volgen en verwijzen naar een bepaalde array. | Bekijk de [ extra middelensectie ](#content-path) voor een voorbeeld van het middel bevat binnen een inhoudsweg. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Het pad dat wijst naar de verzamelingsrecords die moeten worden ingevoegd in Experience Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Met deze eigenschap kunt u specifieke items identificeren uit de bron die is geïdentificeerd in het inhoudspad en die moeten worden uitgesloten van het opnemen van inhoud. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Met deze eigenschap kunt u expliciet de afzonderlijke kenmerken opgeven die u wilt behouden. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Met deze eigenschap kunt u de waarde overschrijven van de kenmerknaam die u in `contentPath` hebt opgegeven. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Met deze eigenschap kunt u twee arrays samenvoegen en de brongegevens transformeren naar de Experience Platform-resource. |  |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Het pad dat wijst naar de verzamelingsrecords die u wilt afvlakken. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Dit bezit staat u toe om specifieke punten van het middel te identificeren die in de entiteitweg worden geïdentificeerd die van worden uitgesloten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Met deze eigenschap kunt u expliciet de afzonderlijke kenmerken opgeven die u wilt behouden. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Met deze eigenschap kunt u de waarde overschrijven van de kenmerknaam die u in `explodeEntityPath` hebt opgegeven. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definieert de parameters of velden die moeten worden opgegeven voor het ophalen van een koppeling naar de volgende pagina vanuit het huidige paginaantwoord van de gebruiker, of tijdens het maken van een URL voor de volgende pagina. |  |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Hiermee geeft u het type van het ondersteunde paginatietype voor uw bron weer. | <ul><li>`OFFSET`: Met dit paginatype kunt u de resultaten parseren door een index op te geven vanaf waar de resulterende array moet worden gestart en een limiet op het aantal resultaten.</li><li>`POINTER`: Met dit paginatype kunt u een `pointer` -variabele gebruiken om te wijzen naar een bepaald item dat met een aanvraag moet worden verzonden. Voor het pagineren van het type aanwijzer is een pad vereist voor de nuttige lading van dat punt naar de volgende pagina.</li><li>`CONTINUATION_TOKEN`: Met dit paginatype kunt u de query- of headerparameters toevoegen met een continutoken om de resterende retourgegevens van uw bron op te halen. Deze gegevens zijn oorspronkelijk niet geretourneerd vanwege een vooraf bepaald maximum.</li><li>`PAGE`: Met dit pagineringstype kunt u uw queryparameter toevoegen met een pagineringsparameter om gegevens per pagina te doorlopen, te beginnen bij pagina nul.</li><li>`NONE`: dit pagineringstype kan worden gebruikt voor bronnen die geen van de beschikbare pagineringstypen ondersteunen. Paginatype `NONE` retourneert de volledige reactiegegevens na een aanvraag.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | De naam voor de limiet waarmee de API het aantal records kan opgeven dat op een pagina moet worden opgehaald. | `limit` of `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Het aantal records dat op een pagina moet worden opgehaald. | `limit=10` of `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | De naam van het verschuivingskenmerk. Dit is vereist als het paginatype is ingesteld op `offset` . | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | De naam van het attribuut pointer. Hiervoor is een pad nodig naar het kenmerk dat naar de volgende pagina verwijst. Dit is vereist als het paginatype is ingesteld op `pointer` . | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Bevat parameters die gesteunde het plannen formaten voor uw bron bepalen. De parameters van het programma omvatten `startTime` en `endTime`, allebei waarvan u toestaan om specifieke tijdintervallen voor partijlooppas te plaatsen, die dan ervoor zorgt dat de verslagen die in een vorige partijlooppas worden gehaald niet opnieuw worden gehaald. |  |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definieert de naam van de begintijdparameter | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definieert de naam van de eindtijdparameter | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definieert de ondersteunde indeling voor de `scheduleStartParamName` . | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definieert de ondersteunde indeling voor de `scheduleEndParamName` . | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Bepaalt de user-provided parameters om middelwaarden te halen. | Zie de [ extra middelen ](#user-input) voor een voorbeeld user-inputted parameters voor `spec.properties`. |

{style="table-layout:auto"}

## Aanvullende bronnen {#appendix}

De volgende secties verstrekken informatie over extra configuraties u aan uw `sourceSpec` kunt maken, met inbegrip van geavanceerde het plannen en douaneschema&#39;s.

### Voorbeeld van een inhoudspad {#content-path}

Hieronder ziet u een voorbeeld van de inhoud van de eigenschap `contentPath` in een [!DNL MailChimp Members] -verbindingsspecificatie.

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

Hieronder ziet u een voorbeeld van een door de gebruiker opgegeven `spec.properties` met behulp van een [!DNL MailChimp Members] -verbindingsspecificatie.

In dit voorbeeld wordt `listId` opgegeven als onderdeel van `urlParams.path` . Als u `listId` van een klant moet terugwinnen, dan moet u het ook als deel van `spec.properties` bepalen.


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

### Source-specificatievoorbeeld {#source-spec}

Hier volgt een voltooide bronspecificatie met [!DNL MailChimp Members]:

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

>[!BEGINTABS]

>[!TAB  Verschuiving ]

Met dit paginatype kunt u de resultaten parseren door een index op te geven vanaf waar de resulterende array moet worden gestart en een limiet op het aantal resultaten. Bijvoorbeeld:

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `type` | Het type paginering waarmee gegevens worden geretourneerd. |
| `limitName` | De naam voor de limiet waarmee de API het aantal records kan opgeven dat op een pagina moet worden opgehaald. |
| `limitValue` | Het aantal records dat op een pagina moet worden opgehaald. |
| `offSetName` | De naam van het verschuivingskenmerk. Dit is vereist als het paginatype is ingesteld op `offset` . |
| `endConditionName` | Een door de gebruiker gedefinieerde waarde die aangeeft aan welke voorwaarde de pagineringslus in de volgende HTTP-aanvraag wordt beëindigd. U moet de kenmerknaam opgeven waarop u de eindvoorwaarde wilt plaatsen. |
| `endConditionValue` | De kenmerkwaarde waarop u de eindvoorwaarde wilt plaatsen. |

>[!TAB  Aanwijzer ]

Met dit pagineringstype kunt u een variabele `pointer` gebruiken om naar een bepaald item te wijzen dat met een aanvraag moet worden verzonden. Voor het pagineren van het type aanwijzer is een pad vereist voor de nuttige lading van dat punt naar de volgende pagina. Bijvoorbeeld:

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `type` | Het type paginering waarmee gegevens worden geretourneerd. |
| `limitName` | De naam voor de limiet waarmee de API het aantal records kan opgeven dat op een pagina moet worden opgehaald. |
| `limitValue` | Het aantal records dat op een pagina moet worden opgehaald. |
| `pointerPath` | De naam van het attribuut pointer. Hiervoor is een pad nodig naar het kenmerk dat naar de volgende pagina verwijst. |

>[!TAB  het teken van de Voortgang ]

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
| `type` | Het type paginering waarmee gegevens worden geretourneerd. |
| `continuationTokenPath` | De waarde die aan de vraagparams moet worden toegevoegd om naar de volgende pagina van de teruggekeerde resultaten te bewegen. |
| `parameterType` | De eigenschap `parameterType` definieert waar de `parameterName` moet worden toegevoegd. Met het type `QUERYPARAM` kunt u de query toevoegen met de `parameterName` . Met `HEADERPARAM` kunt u uw `parameterName` toevoegen aan uw headeraanvraag. |
| `parameterName` | De naam van de parameter die wordt gebruikt om het voortzetteken op te nemen. De notatie is als volgt: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | Met de eigenschap `delayRequestMillis` in paginering kunt u de snelheid bepalen van de aanvragen die aan de bron worden gedaan. Sommige bronnen kunnen een limiet hebben voor het aantal aanvragen dat u per minuut kunt indienen. [!DNL Zendesk] heeft bijvoorbeeld een limiet van 100 verzoeken per minuut en als u `delayRequestMillis` to `850` definieert, kunt u de bron zo configureren dat deze aanroepen uitvoert met ongeveer 80 verzoeken per minuut, ruim onder de drempel van 100 aanvragen per minuut. |

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

>[!TAB  Pagina ]

Met het paginatype `PAGE` kunt u de retourgegevens doorlopen op het aantal pagina&#39;s, beginnend bij nul. Wanneer u `PAGE` typepaginatie gebruikt, moet u het aantal records opgeven dat op één pagina wordt gegeven.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `type` | Het type paginering waarmee gegevens worden geretourneerd. |
| `limitName` | De naam voor de limiet waarmee de API het aantal records kan opgeven dat op een pagina moet worden opgehaald. |
| `limitValue` | Het aantal records dat op een pagina moet worden opgehaald. |
| `initialPageIndex` | (Optioneel) De eerste pagina-index definieert het paginanummer van waaruit de paginering begint. Dit veld kan worden gebruikt voor bronnen waarvan de paginering niet begint bij 0. Als deze optie niet is opgegeven, wordt de index van de eerste pagina standaard ingesteld op 0. Dit veld verwacht een geheel getal. |
| `endPageIndex` | (Optioneel) Met de index van de eindpagina kunt u een eindvoorwaarde instellen en de paginering stoppen. Dit veld kan worden gebruikt als de standaardeindvoorwaarden voor het stoppen van paginering niet beschikbaar zijn. Dit veld kan ook worden gebruikt als het aantal pagina&#39;s dat moet worden ingevoerd of het laatste paginanummer via de antwoordkop wordt opgegeven. Dit is gebruikelijk bij het gebruik van de paginering van `PAGE` typen. De waarde voor de index van de eindpagina kan het laatste paginanummer zijn of een expressiewaarde van het type tekenreeks in de reactiekop. Met `headers.x-pagecount` kunt u bijvoorbeeld de index van de eindpagina toewijzen aan de waarde `x-pagecount` in de reactiekoppen. **Nota**: `x-pagecount` is een verplichte antwoordkopbal voor sommige bronnen en houdt het waardeaantal pagina&#39;s dat moet worden opgenomen. |
| `pageParamName` | De naam van de parameter die u aan vraagparameters moet toevoegen om door verschillende pagina&#39;s van de terugkeergegevens te oversteken. `https://abc.com?pageIndex=1` retourneert bijvoorbeeld de tweede pagina van de retourlading van een API. |
| `maximumRequest` | Het maximumaantal verzoeken een bron voor een bepaalde stijgende looppas kan maken. De huidige standaardlimiet is 10000. |

{style="table-layout:auto"}


>[!TAB  niets ]

Het paginatietype `NONE` kan worden gebruikt voor bronnen die geen van de beschikbare paginatypen ondersteunen. De bronnen die het pagineringstype van `NONE` gebruiken keren eenvoudig alle terugwinnbare verslagen terug wanneer een GET verzoek wordt gemaakt.

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### Geavanceerde planning voor Self-Serve Bronnen (Batch SDK)

Vorm incrementele en backfill planning van uw bron gebruikend geavanceerde het plannen. Met de eigenschap `incremental` kunt u een schema configureren waarin uw bron alleen nieuwe of gewijzigde records opneemt, terwijl u met de eigenschap `backfill` een schema kunt maken voor het opnemen van historische gegevens.

Met geavanceerde het plannen, kunt u uitdrukkingen en functies gebruiken specifiek voor uw bron om stijgende en backfill programma&#39;s te vormen. In het onderstaande voorbeeld vereist de [!DNL Zendesk] -bron dat het incrementele schema wordt opgemaakt als `type:user updated > {START_TIME} updated < {END_TIME}` en dat de backfill als `type:user updated < {END_TIME}` wordt opgemaakt.

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
| `scheduleParams.type` | Het type van het plannen van uw bron zal gebruiken. Stel deze waarde in op `ADVANCE` als u het geavanceerde planningstype wilt gebruiken. |
| `scheduleParams.paramFormat` | De gedefinieerde indeling van uw planningsparameter. Deze waarde kan gelijk zijn aan de waarden `scheduleStartParamFormat` en `scheduleEndParamFormat` van de bron. |
| `scheduleParams.incremental` | De incrementele query van uw bron. Incrementeel verwijst naar een innamemethode waarbij alleen nieuwe of gewijzigde gegevens worden opgenomen. |
| `scheduleParams.backfill` | De backfill-query van uw bron. Backfill verwijst naar een innamemethode waarbij historische gegevens worden ingesloten. |

Zodra u uw geavanceerde planning vormt, moet u dan naar uw `scheduleParams` in de sectie van URL, het lichaam, of kopbalparams verwijzen, afhankelijk van wat uw bepaalde bron steunt. In het onderstaande voorbeeld is `{SCHEDULE_QUERY}` een tijdelijke aanduiding die wordt gebruikt om op te geven waar de incrementele en backfill-planningsexpressies worden gebruikt. In het geval van een [!DNL Zendesk] bron wordt `query` gebruikt in `queryParams` om geavanceerde planning op te geven.

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

U kunt een aangepast schema aan uw `sourceSpec` opnemen om alle kenmerken te definiëren die nodig zijn voor uw bron, inclusief alle dynamische kenmerken die u nodig hebt. U kunt de bijbehorende verbindingsspecificatie van uw bron bijwerken door een PUT-aanvraag in te dienen bij het `/connectionSpecs` -eindpunt van de [!DNL Flow Service] API en het aangepaste schema op te geven in de sectie `sourceSpec` van uw verbindingsspecificatie.

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

Met uw bevolkte bronspecificaties, kunt u te werk gaan om de verkennende specificaties voor de bron te vormen die u aan Experience Platform wilt integreren. Zie het document bij [ het vormen onderzoeken specificaties ](./explorespec.md) voor meer informatie.
