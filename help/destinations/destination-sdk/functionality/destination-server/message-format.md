---
description: Deze pagina is gericht op de berichtindeling en de profieltransformatie in gegevens die van Adobe Experience Platform naar bestemmingen worden geëxporteerd.
title: Berichtindeling
exl-id: ab05d34e-530f-456c-b78a-7f3389733d35
source-git-commit: b42ef11681bb50141c7f3dc76d8c79d71e55e73c
workflow-type: tm+mt
source-wordcount: '2502'
ht-degree: 0%

---

# Berichtindeling

## Voorwaarden - Adobe Experience Platform-concepten {#prerequisites}

Om het berichtformaat en profielconfiguratie en transformatieproces op de kant van de Adobe te begrijpen, gelieve zich met de volgende concepten van het Experience Platform vertrouwd te maken:

* **Experience Data Model (XDM)**. [XDM-overzicht](../../../../xdm/home.md) en  [Een XDM-schema maken in Adobe Experience Platform](../../../../xdm/tutorials/create-schema-ui.md).
* **Klasse**. [Klassen maken en bewerken in de gebruikersinterface](../../../../xdm/ui/resources/classes.md).
* **IdentityMap**. Het identiteitsoverzicht is een kaart van alle eindgebruikersidentiteiten in Adobe Experience Platform. Zie `xdm:identityMap` in de [XDM-veldwoordenboek](../../../../xdm/schema/field-dictionary.md).
* **SegmentLidmaatschap**. De [segmentLidmaatschap](../../../../xdm/schema/field-dictionary.md) XDM-kenmerk geeft aan welk publiek een profiel lid is van. Voor de drie verschillende waarden in de `status` veld, lees de documentatie op [Publiek Lidmaatschap Details schema groep](../../../../xdm/field-groups/profile/segmentation.md).

>[!IMPORTANT]
>
>Alle parameternamen en -waarden die door Destination SDK worden ondersteund, zijn **hoofdlettergevoelig**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Ondersteunde integratietypen {#supported-integration-types}

Raadpleeg de onderstaande tabel voor meer informatie over de integratietypen die de op deze pagina beschreven functionaliteit ondersteunen.

| Type integratie | Ondersteunt functionaliteit |
|---|---|
| Integraties in realtime (streaming) | Ja |
| Op bestanden gebaseerde (batch) integratie | Ja (alleen de stappen 1 en 2 in het onderstaande diagram) |

## Overzicht {#overview}

Deze pagina is gericht op de berichtindeling en de profieltransformatie in gegevens die van Adobe Experience Platform naar bestemmingen worden geëxporteerd.

Adobe Experience Platform exporteert gegevens naar een aanzienlijk aantal bestemmingen, in verschillende gegevensindelingen. Voorbeelden van bestemmingstypen zijn advertentieplatforms (Google), sociale netwerken (Facebook) en cloudopslaglocaties (Amazon S3, Azure Event Hubs).

Experience Platform kan de berichtindeling van geëxporteerde profielen aanpassen aan de verwachte indeling aan uw zijde. Om deze aanpassing te begrijpen, zijn de volgende concepten belangrijk:

* Het XDM-bronschema (1) en doel (2) in Adobe Experience Platform
* Het verwachte berichtformaat aan de partnerkant (3), en
* De transformatielaag tussen XDM-schema en de verwachte berichtindeling, die u kunt definiëren door een [berichttransformatiesjabloon](#using-templating).

![Transformatie schema naar JSON](../../assets/functionality/destination-server/transformations-3-steps.png)

Experience Platform gebruikt XDM-schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Bron-XDM-schema (1)**: Dit punt verwijst naar het schema dat de klanten in Experience Platform gebruiken. In Experience Platform, in de [toewijzingsstap](../../../ui/activate-segment-streaming-destinations.md#mapping) van het activerende bestemmingswerkschema, wijzen de klanten gebieden van hun XDM schema aan het het doelschema van uw bestemming (2) in kaart.

**Doel-XDM-schema (2)**: Gebaseerd op het JSON standaardschema (3) van het verwachte formaat van uw bestemming en de attributen die uw bestemming kan interpreteren, kunt u profielattributen en identiteiten in uw doelXDM schema bepalen. U kunt dit in de bestemmingsconfiguratie, in [schemaConfig](../../functionality/destination-configuration/schema-configuration.md) en [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md) objecten.

**JSON-standaardschema van uw kenmerken van het doelprofiel (3)**: Dit voorbeeld vertegenwoordigt een [JSON-schema](https://json-schema.org/learn/miscellaneous-examples.html) van alle profielkenmerken die uw platform ondersteunt en de typen kenmerken ervan (bijvoorbeeld: object, tekenreeks, array). Voorbeelden van velden die uw doel kan ondersteunen, zijn `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`, enzovoort. U hebt een [berichttransformatiesjabloon](#using-templating) om de gegevens die uit Experience Platform worden geëxporteerd af te stemmen op de gewenste indeling.

Gebaseerd op de hierboven beschreven schematransformaties, is hier hoe een profielconfiguratie tussen het bronXDM schema en een steekproefschema op de partnerkant verandert:

![Voorbeeld van transformatieberichten](../../assets/functionality/destination-server/transformations-with-examples.png)

## Aan de slag - drie basiskenmerken transformeren {#getting-started}

In het onderstaande voorbeeld worden drie veelvoorkomende profielkenmerken in Adobe Experience Platform gebruikt om het profieltransformatieproces te demonstreren: **voornaam**, **achternaam**, en **mailadres**.

>[!NOTE]
>
>De klant wijst de attributen van het bronXDM schema aan het partnerXDM schema in Adobe Experience Platform UI, in toe **Toewijzing** van de [doelworkflow activeren](../../../ui/activate-segment-streaming-destinations.md#mapping).

Stel dat uw platform een berichtindeling kan ontvangen zoals:

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

Gezien het berichtformaat, zijn de overeenkomstige transformaties als volgt:

| Attribuut in partnerXDM schema op de kant van de Adobe | Transformatie | Kenmerk in HTTP-bericht aan uw zijde |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Profielstructuur in Experience Platform {#profile-structure}

Om de voorbeelden verder hieronder op de pagina te begrijpen, is het belangrijk om de structuur van een profiel in Experience Platform te kennen.

Profielen hebben drie secties:

* `segmentMembership` (altijd aanwezig in een profiel)
   * deze sectie bevat alle soorten publiek die in het profiel aanwezig zijn. Het publiek kan een van twee statussen hebben: `realized` of `exited`.
* `identityMap` (altijd aanwezig in een profiel)
   * deze sectie bevat alle identiteiten die in het profiel aanwezig zijn (e-mail, Google GAID, Apple IDFA, enzovoort) en die de gebruiker in kaart heeft gebracht voor exporteren in de activeringsworkflow.
* attributen (afhankelijk van de bestemmingsconfiguratie, zouden deze op het profiel aanwezig kunnen zijn). Er is ook een klein verschil tussen vooraf gedefinieerde kenmerken en vrije-vormkenmerken:
   * for *vrijevormkenmerken* bevatten `.value` pad als het kenmerk aanwezig is in het profiel (zie `lastName` kenmerk uit voorbeeld 1). Als ze niet aanwezig zijn in het profiel, bevatten ze geen `.value` pad (zie `firstName` kenmerk uit voorbeeld 1).
   * for *vooraf gedefinieerde kenmerken*, bevatten geen `.value` pad. Alle toegewezen kenmerken die aanwezig zijn in een profiel, worden weergegeven in de kenmerkenkaart. De niet-bestaande versies zullen niet aanwezig zijn (zie Voorbeeld 2 - de `firstName` (bestaat niet in het profiel).

Zie twee voorbeelden van profielen in Experience Platform:

### Voorbeeld 1 met `segmentMembership`, `identityMap` en kenmerken voor vrije-vormkenmerken {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### Voorbeeld 2 met `segmentMembership`, `identityMap` en kenmerken voor vooraf gedefinieerde kenmerken {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en publieksleiding {#using-templating}

Adobe gebruikt [Teersjablonen](https://pebbletemplates.io/), een sjabloontaal die lijkt op [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), om de gebieden van het Experience Platform XDM schema in een formaat om te zetten dat door uw bestemming wordt gesteund.

Deze sectie verstrekt verscheidene voorbeelden van hoe deze transformaties worden gemaakt - van het inputXDM schema, door het malplaatje, en output in ladingsformaten die door uw bestemming worden goedgekeurd. De onderstaande voorbeelden worden als volgt weergegeven door de toenemende complexiteit:

1. Eenvoudige transformatievoorbeelden. Leer hoe sjablonen werken met eenvoudige transformaties voor [Profielkenmerken](#attributes), [Publiek lidmaatschap](#segment-membership), en [Identiteit](#identities) velden.
2. Eenvoudigere voorbeelden van sjablonen waarin bovenstaande velden worden gecombineerd: [Een sjabloon maken die het publiek en de identiteiten verstuurt](./message-format.md#segments-and-identities) en [Een sjabloon maken die segmenten, identiteiten en profielkenmerken verstuurt](#segments-identities-attributes).
3. Sjablonen die de aggregatietoets bevatten. Wanneer u [configureerbare samenvoeging](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) in de bestemmingsconfiguratie, groepeert het Experience Platform de profielen die naar uw bestemming worden uitgevoerd die op criteria zoals publiek-identiteitskaart, publieksstatus, of identiteitsnamespaces worden gebaseerd.

### Profielkenmerken {#attributes}

Als u de profielkenmerken die naar uw doel zijn geëxporteerd, wilt transformeren, raadpleegt u de JSON en de codevoorbeelden hieronder.

>[!IMPORTANT]
>
>Voor een lijst met alle beschikbare profielkenmerken in Adobe Experience Platform raadpleegt u de [XDM-veldwoordenboek](../../../../xdm/schema/field-dictionary.md).


**Invoer**

Profiel 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

Profiel 2:

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens zoals dubbele aanhalingstekens verwijderen `""` voordat u het [template](../../functionality/destination-server/templating-specs.md) in de [doelserverconfiguratie](../../authoring-api/destination-server/create-destination-server.md). Voor meer informatie over het ontsnappen van dubbele aanhalingstekens, zie Hoofdstuk 9 in [JSON-standaard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultaat**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### Publiek lidmaatschap {#audience-membership}

De [segmentLidmaatschap](../../../../xdm/schema/field-dictionary.md) XDM-kenmerk geeft aan welk publiek een profiel lid is van.
Voor de drie verschillende waarden in de `status` veld, lees de documentatie op [Publiek Lidmaatschap Details schema groep](../../../../xdm/field-groups/profile/segmentation.md).

**Invoer**

Profiel 1:

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

Profiel 2:

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens zoals dubbele aanhalingstekens verwijderen `""` voordat u het [template](../../functionality/destination-server/templating-specs.md) in de [doelserverconfiguratie](../../authoring-api/destination-server/create-destination-server.md). Voor meer informatie over het ontsnappen van dubbele aanhalingstekens, zie Hoofdstuk 9 in [JSON-standaard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).


```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultaat**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### Identiteiten {#identities}

Voor informatie over identiteiten in Experience Platform, zie [Overzicht naamruimte identiteit](../../../../identity-service/namespaces.md).

**Invoer**

Profiel 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

Profiel 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens zoals dubbele aanhalingstekens verwijderen `""` voordat u het [template](../../functionality/destination-server/templating-specs.md) in de [doelserverconfiguratie](../../authoring-api/destination-server/create-destination-server.md). Voor meer informatie over het ontsnappen van dubbele aanhalingstekens, zie Hoofdstuk 9 in [JSON-standaard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultaat**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### Een sjabloon maken die het publiek en de identiteiten verstuurt {#segments-and-identities}

Deze sectie verstrekt een voorbeeld van een algemeen gebruikte transformatie tussen het schema van Adobe XDM en het schema van de partnerbestemming.
In het onderstaande voorbeeld ziet u hoe u de indeling voor het publiekslidmaatschap en de identiteiten transformeert en uitvoert naar uw bestemming.

**Invoer**

Profiel 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profiel 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens zoals dubbele aanhalingstekens verwijderen `""` voordat u het [template](../../functionality/destination-server/templating-specs.md) in de [doelserverconfiguratie](../../authoring-api/destination-server/create-destination-server.md). Voor meer informatie over het ontsnappen van dubbele aanhalingstekens, zie Hoofdstuk 9 in [JSON-standaard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering audiences by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultaat**

De `json` hieronder worden de gegevens weergegeven die uit Adobe Experience Platform zijn geëxporteerd.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Een sjabloon maken die segmenten, identiteiten en profielkenmerken verstuurt {#segments-identities-attributes}

Deze sectie verstrekt een voorbeeld van een algemeen gebruikte transformatie tussen het schema van Adobe XDM en het schema van de partnerbestemming.

Een ander veelvoorkomend geval van gebruik is het uitvoeren van gegevens die publieksleden, identiteiten (bijvoorbeeld: e-mailadres, telefoonaantal, reclame-id), en profielattributen bevatten. Als u gegevens op deze manier wilt exporteren, raadpleegt u het onderstaande voorbeeld:

**Invoer**

Profiel 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profiel 2:

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens zoals dubbele aanhalingstekens verwijderen `""` voordat u het [template](../../functionality/destination-server/templating-specs.md) in de [doelserverconfiguratie](../../authoring-api/destination-server/create-destination-server.md). Voor meer informatie over het ontsnappen van dubbele aanhalingstekens, zie Hoofdstuk 9 in [JSON-standaard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering audiences by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**Resultaat**

De `json` hieronder worden de gegevens weergegeven die uit Adobe Experience Platform zijn geëxporteerd.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### De samenvoegingssleutel in de sjabloon opnemen voor toegang tot geëxporteerde profielen die op verschillende criteria zijn gegroepeerd {#template-aggregation-key}

Wanneer u [configureerbare samenvoeging](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) in de bestemmingsconfiguratie, kunt u de profielen groeperen die naar uw bestemming worden uitgevoerd op criteria zoals publieksidentiteitskaart, publieksalias, publiekslidmaatschap, of identiteitsnamespaces worden gebaseerd.

In het malplaatje van de berichttransformatie, kunt u tot de bovengenoemde samenvoegingssleutels toegang hebben, zoals aangetoond in de voorbeelden in de volgende secties. Gebruik aggregatietoetsen om het uit Experience Platform geëxporteerde HTTP-bericht te structureren, zodat dit overeenkomt met de notatie- en tarieflimieten die door de bestemming worden verwacht.

#### Code voor publiek-id in de sjabloon gebruiken {#aggregation-key-segment-id}

Als u [configureerbare samenvoeging](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) en instellen `includeSegmentId` naar true, worden de profielen in de HTTP-berichten die naar uw bestemming worden geëxporteerd, gegroepeerd op gebruikers-id. Hieronder ziet u hoe u toegang krijgt tot de gebruikers-id in de sjabloon.

**Invoer**

Houd rekening met de vier onderstaande profielen, waarbij:

* de eerste twee maken deel uit van het publiek met de publiek-id `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* het derde profiel maakt deel uit van het publiek met de gebruikers-id `8f812592-3f06-416b-bd50-e7831848a31a`
* het vierde profiel maakt deel uit van beide bovengenoemde doelgroepen .

Profiel 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profiel 2:

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profiel 3:

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

Profiel 4:

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens zoals dubbele aanhalingstekens verwijderen `""` voordat u het [template](../../functionality/destination-server/templating-specs.md) in de [doelserverconfiguratie](../../authoring-api/destination-server/create-destination-server.md). Voor meer informatie over het ontsnappen van dubbele aanhalingstekens, zie Hoofdstuk 9 in [JSON-standaard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Hieronder ziet u hoe `audienceId` wordt gebruikt in het malplaatje om tot publiek IDs toegang te hebben. In dit voorbeeld wordt ervan uitgegaan dat u `audienceId` voor het lidmaatschap van het publiek in uw bestemmingtaxonomie. U kunt in plaats daarvan elke andere veldnaam gebruiken, afhankelijk van uw eigen taxonomie.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Resultaat**

Als de profielen naar uw bestemming worden geëxporteerd, worden ze in twee groepen gesplitst op basis van hun gebruikers-id.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### Aliasaggregatietoets voor het publiek gebruiken in de sjabloon {#aggregation-key-segment-alias}

Als u [configureerbare samenvoeging](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) en instellen `includeSegmentId` naar waar (true), hebt u ook toegang tot publiekalias in de sjabloon.

Voeg de onderstaande regel toe aan de sjabloon voor toegang tot de geëxporteerde profielen die zijn gegroepeerd op publieksalias.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### De aggregatietoets voor de status van het publiek gebruiken in de sjabloon {#aggregation-key-segment-status}

Als u [configureerbare samenvoeging](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) en instellen `includeSegmentId` en `includeSegmentStatus` naar waar (true), hebt u toegang tot de publieksstatus in de sjabloon. Op deze manier kunt u profielen groeperen in de HTTP-berichten die naar uw bestemming worden geëxporteerd, op basis van het feit of de profielen moeten worden toegevoegd of verwijderd uit segmenten.

Mogelijke waarden zijn:

* gereed
* bestaand
* verlaten

Voeg op basis van de bovenstaande waarden de onderstaande regel toe aan de sjabloon om profielen toe te voegen aan of te verwijderen uit segmenten:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Naamruimteaggregatietoets gebruiken in de sjabloon {#aggregation-key-identity}

Hieronder ziet u een voorbeeld waarin de [configureerbare samenvoeging](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) in de doelconfiguratie is ingesteld op het samenvoegen van geëxporteerde profielen op basis van naamruimten, in het formulier `"namespaces": ["email", "phone"]` en `"namespaces": ["GAID", "IDFA"]`. Zie de `groups` in de [doelconfiguratie maken](../../authoring-api/destination-configuration/create-destination-configuration.md) documentatie voor meer informatie over groeperen.

**Invoer**

Profiel 1:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

Profiel 2:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens zoals dubbele aanhalingstekens verwijderen `""` voordat u het [template](../../functionality/destination-server/templating-specs.md) in de [doelserverconfiguratie](../../authoring-api/destination-server/create-destination-server.md). Voor meer informatie over het ontsnappen van dubbele aanhalingstekens, zie Hoofdstuk 9 in [JSON-standaard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Let op: `input.aggregationKey.identityNamespaces` wordt gebruikt in de onderstaande template

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**Resultaat**

Als de profielen naar uw bestemming worden geëxporteerd, worden ze in twee groepen gesplitst op basis van hun naamruimten. E-mail en telefoon zijn in één groep, terwijl GAID en IDFA in een andere zijn.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### De aggregatietoets in een URL-sjabloon gebruiken {#aggregation-key-url-template}

Afhankelijk van het gebruik kunt u ook de hier in een URL beschreven aggregatietoetsen gebruiken, zoals hieronder wordt getoond:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Referentie: Context en functies die worden gebruikt in de transformatiesjablonen {#reference}

De context die aan de sjabloon wordt gegeven, bevat `input`  (de profielen/gegevens die in deze vraag worden uitgevoerd) en `destination` (gegevens over het doel waarnaar de Adobe gegevens verzendt, geldig voor alle profielen).

In de onderstaande tabel vindt u een beschrijving van de functies in de bovenstaande voorbeelden.

| -functie | Beschrijving | Voorbeeld |
|---------|----------|----------|
| `input.profile` | Het profiel, weergegeven als een [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Volgt het partnerXDM schema dat hierboven verder op deze pagina wordt vermeld. |
| `hasSegments` | Deze functie neemt een kaart van namespace publiek IDs als parameter. De functie retourneert `true` als er minstens één publiek op de kaart staat (ongeacht zijn status), en `false` anders. U kunt deze functie gebruiken om te beslissen of u een overzicht van het publiek doorloopt of niet. | `hasSegments(input.profile.segmentMembership)` |
| `destination.namespaceSegmentAliases` | Wijs van publiek-id&#39;s in een specifieke Adobe Experience Platform-naamruimte toe aan publiekalias in het systeem van de partner. | `destination.namespaceSegmentAliases["ups"]["seg-id-1"]` |
| `destination.namespaceSegmentNames` | Wijs van publieksnamen in specifieke Adobe Experience Platform namespaces aan publieksnamen in het systeem van de partner toe. | `destination.namespaceSegmentNames["ups"]["seg-name-1"]` |
| `destination.namespaceSegmentTimestamps` | Retourneert de tijd waarop een publiek in UNIX-tijdstempelindeling is gemaakt, bijgewerkt of geactiveerd. | <ul><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].createdAt`: retourneert de tijd waarop het segment met de id `seg-id-1`van de `ups` naamruimte, gemaakt in UNIX-tijdstempelindeling.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].updatedAt`: retourneert de tijd waarop het publiek de id gebruikt `seg-id-1`van de `ups` naamruimte, is bijgewerkt in UNIX-tijdstempelindeling.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingCreatedAt`: retourneert de tijd waarop het publiek de id gebruikt `seg-id-1`van de `ups` naamruimte, is geactiveerd naar de bestemming, in UNIX-tijdstempelindeling.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingUpdatedAt`: retourneert de tijd waarop de publieksactivering op de bestemming is bijgewerkt, in UNIX-tijdstempelindeling.</li></ul> |
| `addedSegments(mapOfNamespacedSegmentIds)` | Retourneert alleen het publiek dat de status heeft `realized`, in alle naamruimten. | `addedSegments(input.profile.segmentMembership)` |
| `removedSegments(mapOfNamespacedSegmentIds)` | Retourneert alleen het publiek dat de status heeft `exited`, in alle naamruimten. | `removedSegments(input.profile.segmentMembership)` |
| `destination.segmentAliases` | **Afgeschaft. Vervangen door`destination.namespaceSegmentAliases`** <br><br> Wijs van publiek IDs in Adobe Experience Platform namespace aan publiekalias in het systeem van de partner toe. | `destination.segmentAliases["seg-id-1"]` |
| `destination.segmentNames` | **Afgeschaft. Vervangen door`destination.namespaceSegmentNames`** <br><br>  Wijs van publieksnamen in Adobe Experience Platform namespace aan publieksnamen in het systeem van de partner toe. | `destination.segmentNames["seg-name-1"]` |
| `destination.segmentTimestamps` | **Afgeschaft. Vervangen door`destination.namespaceSegmentTimestamps`** <br><br> Retourneert de tijd waarop een publiek in UNIX-tijdstempelindeling is gemaakt, bijgewerkt of geactiveerd. | <ul><li>`destination.segmentTimestamps["seg-id-1"].createdAt`: retourneert de tijd waarop het publiek de id gebruikt `seg-id-1` is gemaakt in UNIX-tijdstempelindeling.</li><li>`destination.segmentTimestamps["seg-id-1"].updatedAt`: retourneert de tijd waarop het publiek de id gebruikt `seg-id-1` is bijgewerkt, in UNIX-tijdstempelindeling.</li><li>`destination.segmentTimestamps["seg-id-1"].mappingCreatedAt`: retourneert de tijd waarop het publiek de id gebruikt `seg-id-1` is geactiveerd naar de bestemming, in UNIX-tijdstempelindeling.</li><li>`destination.segmentTimestamps["seg-id-1"].mappingUpdatedAt`: retourneert de tijd waarop de publieksactivering op de bestemming is bijgewerkt, in UNIX-tijdstempelindeling.</li></ul> |

{style="table-layout:auto"}

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe gegevens die uit het Experience Platform zijn geëxporteerd, worden getransformeerd. Lees vervolgens de volgende pagina&#39;s om uw kennis over het maken van sjablonen voor berichttransformatie voor uw doel te voltooien:

* [Een sjabloon voor berichttransformatie maken en testen](../../testing-api/streaming-destinations/create-template.md)
* [API-bewerkingen voor sjablonen renderen](../../testing-api/streaming-destinations/render-template-api.md)
* [Ondersteunde transformatiefuncties in Destination SDK](../destination-server/supported-functions.md)

Raadpleeg de volgende artikelen voor meer informatie over de andere componenten van de doelserver:

* [Server specs voor bestemmingen die met Destination SDK worden gecreeerd](server-specs.md)
* [Sjabloonspecificaties](templating-specs.md)
* [Configuratie bestandsindeling](file-formatting.md)
