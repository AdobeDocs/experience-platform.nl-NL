---
description: Deze pagina is gericht op de berichtindeling en de profieltransformatie in gegevens die van Adobe Experience Platform naar bestemmingen worden geëxporteerd.
title: Berichtindeling
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 485c1359f8ef5fef0c5aa324cd08de00b0b4bb2f
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---

# Berichtindeling

## Voorwaarden - Adobe Experience Platform-concepten {#prerequisites}

Om het berichtformaat en het proces van de profielconfiguratie en transformatie aan de kant van de Adobe te begrijpen, gelieve zich met de volgende concepten van het Experience Platform vertrouwd te maken:

* **Experience Data Model (XDM)**. [XDM ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl) overviewand   [How to create an XDM schema in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Klasse**. [Maak en bewerk klassen in de gebruikersinterface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **IdentityMap**. Het identiteitsoverzicht is een kaart van alle eindgebruikersidentiteiten in Adobe Experience Platform. Raadpleeg `xdm:identityMap` in het [XDM-veldwoordenboek](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. Het [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM attribuut deelt welke segmenten een profiel een lid van is. Voor de drie verschillende waarden op het `status` gebied, lees de documentatie op [het schemagroep van de Details van het Lidmaatschap van het Segment ](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Overzicht {#overview}

Gebruik de inhoud op deze pagina samen met de rest van [configuratieopties voor partnerbestemmingen](./configuration-options.md). Deze pagina is gericht op de berichtindeling en de profieltransformatie in gegevens die van Adobe Experience Platform naar bestemmingen worden geëxporteerd. De andere pagina adressen specificeert over het verbinden en het voor authentiek verklaren aan uw bestemming.

Adobe Experience Platform exporteert gegevens naar een aanzienlijk aantal bestemmingen, in verschillende gegevensindelingen. Voorbeelden van bestemmingstypen zijn advertentieplatforms (Google), sociale netwerken (Facebook) en cloudopslaglocaties (Amazon S3, Azure Event Hubs).

Experience Platform kan de berichtindeling van geëxporteerde profielen aanpassen aan de verwachte indeling aan uw zijde. Om deze aanpassing te begrijpen, zijn de volgende concepten belangrijk:
* Het XDM-bronschema (1) en het XDM-doelschema (2) in Adobe Experience Platform
* Het verwachte berichtformaat aan de partnerkant (3), en
* De transformatielaag tussen XDM-schema en de verwachte berichtindeling, die u kunt definiëren door een [berichttransformatiesjabloon](./message-format.md#using-templating) te maken.

![Transformatie schema naar JSON](./assets/transformations-3-steps.png)

Experience Platform gebruikt XDM-schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Bron-XDM-schema (1)**: Dit punt verwijst naar het schema dat de klanten in Experience Platform gebruiken. In Experience Platform, in [toewijzingsstap](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) van het activerende bestemmingswerkschema, zouden de klanten gebieden van hun bronschema aan het doelschema van uw bestemming in kaart brengen (2).

**Doel XDM-schema (2)**: Op basis van het JSON-standaardschema (3) van de verwachte indeling van uw bestemming kunt u profielkenmerken en identiteiten definiëren in uw doel-XDM-schema. U kunt dit in de bestemmingsconfiguratie, in [schemaConfig](./destination-configuration.md#schema-configuration) en [identityNamespaces](./destination-configuration.md#identities-and-attributes) voorwerpen doen.

**JSON-standaardschema van uw kenmerken van het doelprofiel (3)**: Dit item vertegenwoordigt een  [JSON-](https://json-schema.org/learn/miscellaneous-examples.html) schema van alle profielkenmerken die uw platform ondersteunt en de typen kenmerken ervan (bijvoorbeeld: object, tekenreeks, array). Voorbeelden van velden die uw doel kan ondersteunen, zijn `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` enzovoort. U hebt een [berichttransformatiesjabloon](./message-format.md#using-templating) nodig om de gegevens die uit het Experience Platform zijn geëxporteerd, af te stemmen op de verwachte indeling.

Gebaseerd op de hierboven beschreven schematransformaties, is hier hoe een profielconfiguratie tussen het bronXDM schema en een steekproefschema op de partnerkant verandert:

![Voorbeeld van transformatieberichten](./assets/transformations-with-examples.png)

<br> 


## Aan de slag - drie basiskenmerken transformeren {#getting-started}

In het onderstaande voorbeeld worden drie veelvoorkomende profielkenmerken in Adobe Experience Platform gebruikt om het profieltransformatieproces te demonstreren: **voornaam**, **achternaam** en **e-mailadres**.

>[!NOTE]
>
>De klant wijst de attributen van het bronXDM schema aan het partnerXDM schema in Adobe Experience Platform UI, in **Toewijzing** stap van [activeert bestemmingswerkschema](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) in kaart.

Stel dat uw platform een berichtindeling kan ontvangen zoals:

```curl
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

| Attribuut in partnerXDM schema op de Adobe kant | Transformatie | Kenmerk in HTTP-bericht aan uw zijde |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

## Een sjabloontaal gebruiken voor de transformaties voor identiteit, kenmerken en segmentlidmaatschap {#using-templating}

Adobe gebruikt een malplaatjetaal gelijkend op [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) om de gebieden van het schema XDM in een formaat om te zetten dat door uw bestemming wordt gesteund.

Deze sectie verstrekt verscheidene voorbeelden van hoe deze transformaties worden gemaakt - van het inputXDM schema, door het malplaatje, en output in ladingsformaten die door uw bestemming worden goedgekeurd. De onderstaande voorbeelden worden als volgt weergegeven door de toenemende complexiteit:

1. Eenvoudige transformatievoorbeelden. Leer hoe sjablonen werken met eenvoudige transformaties voor [Profielkenmerken](./message-format.md#attributes), [Segmentlidmaatschap](./message-format.md#segment-membership) en [Identiteitsvelden](./message-format.md#identities).
2. Eenvoudigere voorbeelden van sjablonen waarin bovenstaande velden worden gecombineerd: [Maak een sjabloon voor het verzenden van segmenten en identiteiten](./message-format.md#segments-and-identities) en [Maak een sjabloon voor het verzenden van segmenten, identiteiten en profielkenmerken](./message-format.md#segments-identities-attributes).
3. Sjablonen die de aggregatietoets bevatten. Wanneer u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) in de bestemmingsconfiguratie gebruikt, groepeert het Experience Platform de profielen die aan uw bestemming worden uitgevoerd die op criteria zoals segment ID, segmentstatus, of identiteitsnamespaces wordt gebaseerd.

### Profielkenmerken {#attributes}

Als u de profielkenmerken die naar uw doel zijn geëxporteerd, wilt transformeren, raadpleegt u de JSON en de codevoorbeelden hieronder.

>[!IMPORTANT]
>
>Zie [XDM-veldwoordenboek](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) voor een lijst met alle beschikbare profielkenmerken in Adobe Experience Platform.


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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Segmentlidmaatschap {#segment-membership}

Het [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM attribuut deelt welke segmenten een profiel een lid van is.
Voor de drie verschillende waarden op het `status` gebied, lees de documentatie op [het schemagroep van de Details van het Lidmaatschap van het Segment ](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

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
        "status": "existing"
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
        "status": "existing"
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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

Voor informatie over identiteiten in Experience Platform, zie [Naamruimte overzicht](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=nl).

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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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


### Een sjabloon maken die segmenten en identiteiten verstuurt {#segments-and-identities}

Deze sectie verstrekt een voorbeeld van een algemeen gebruikte transformatie tussen het schema van Adobe XDM en het schema van de partnerbestemming.
In het onderstaande voorbeeld ziet u hoe u de indeling voor segmentlidmaatschap en identiteiten transformeert en uitvoert naar uw bestemming.

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
              "status": "existing"
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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                    {# Alternative syntax for filtering segments by status: #}
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

In de onderstaande `json` worden de gegevens weergegeven die uit Adobe Experience Platform zijn geëxporteerd.

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

Een ander veelvoorkomend gebruiksgeval is het uitvoeren van gegevens die segmentlidmaatschap, identiteiten (bijvoorbeeld: e-mailadres, telefoonnummer, advertentie-ID) en profielkenmerken. Als u gegevens op deze manier wilt exporteren, raadpleegt u het onderstaande voorbeeld:

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
              "status": "existing"
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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering segments by status: #}
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

In de onderstaande `json` worden de gegevens weergegeven die uit Adobe Experience Platform zijn geëxporteerd.

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

Wanneer u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) in de bestemmingsconfiguratie gebruikt, kunt u de profielen groeperen die naar uw bestemming op criteria zoals segmentidentiteitskaart, segmentalias, segmentlidmaatschap, of identiteitsnamespaces worden uitgevoerd.

In het malplaatje van de berichttransformatie, kunt u tot de bovengenoemde samenvoegingssleutels toegang hebben, zoals aangetoond in de voorbeelden in de volgende secties. Gebruik aggregatietoetsen om het uit Experience Platform geëxporteerde HTTP-bericht te structureren, zodat dit overeenkomt met de notatie- en tarieflimieten die door de bestemming worden verwacht.

#### Segment-id-aggregatietoets gebruiken in de sjabloon {#aggregation-key-segment-id}

Als u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) en reeks `includeSegmentId` aan waar gebruikt, worden de profielen in de HTTP- berichten die naar uw bestemming worden uitgevoerd gegroepeerd door segmentidentiteitskaart. Zie hieronder hoe u tot segmentidentiteitskaart in het malplaatje kunt toegang hebben.

**Invoer**

Bekijk de vier onderstaande profielen, waarbij:
* de eerste twee maken deel uit van het segment met segmentidentiteitskaart `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* het derde profiel maakt deel uit van het segment met segment-id `8f812592-3f06-416b-bd50-e7831848a31a`
* het vierde profiel maakt deel uit van beide segmenten hierboven .

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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
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
            "status":"existing"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Hieronder ziet u hoe `audienceId` in de sjabloon wordt gebruikt om toegang te krijgen tot segment-id&#39;s. In dit voorbeeld wordt ervan uitgegaan dat u `audienceId` gebruikt voor segmentlidmaatschap in uw doeltaxonomie. U kunt in plaats daarvan elke andere veldnaam gebruiken, afhankelijk van uw eigen taxonomie.

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

Als de profielen naar uw bestemming worden geëxporteerd, worden ze in twee groepen gesplitst op basis van hun segment-id.

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

#### Segmentaliasaggregatietoets gebruiken in de sjabloon {#aggregation-key-segment-alias}

Als u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) en reeks `includeSegmentId` aan waar gebruikt, kunt u tot segment alias in het malplaatje ook toegang hebben.

Voeg de onderstaande regel toe aan de sjabloon voor toegang tot de geëxporteerde profielen die zijn gegroepeerd op segmentalias.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### De aggregatietoets voor de segmentstatus in de sjabloon gebruiken {#aggregation-key-segment-status}

Als u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) gebruikt en `includeSegmentId` en `includeSegmentStatus` aan waar plaatst, kunt u tot de segmentstatus in het malplaatje toegang hebben. Op deze manier kunt u profielen groeperen in de HTTP-berichten die naar uw bestemming worden geëxporteerd, op basis van het feit of de profielen moeten worden toegevoegd of verwijderd uit segmenten.

Mogelijke waarden zijn:

* gereed
* bestaand
* verlaten

Voeg op basis van de bovenstaande waarden de onderstaande regel toe aan de sjabloon om profielen toe te voegen aan of te verwijderen uit segmenten:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Naamruimteaggregatietoets gebruiken in de sjabloon {#aggregation-key-identity}

Hieronder ziet u een voorbeeld waarin de [configureerbare aggregatie](./destination-configuration.md#configurable-aggregation) in de doelconfiguratie is ingesteld op het samenvoegen van geëxporteerde profielen via naamruimten, in de notatie `"namespaces": ["email", "phone"]` en `"namespaces": ["GAID", "IDFA"]`. Raadpleeg de parameter `groups` in de [API referentie voor doelconfiguratie](./destination-configuration-api.md) voor meer informatie over deze groepering.

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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

In de onderstaande sjabloon wordt `input.aggregationKey.identityNamespaces` gebruikt

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

De context die aan het malplaatje wordt verstrekt bevat `input` (de profielen/de gegevens die in deze vraag worden uitgevoerd) en `destination` (gegevens over de bestemming die Adobe gegevens naar verzendt, geldig voor alle profielen).

De onderstaande tabel bevat een beschrijving van de functies in de bovenstaande voorbeelden.

| -functie | Beschrijving |
|---------|----------|
| `input.profile` | Het profiel, vertegenwoordigd als [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Volgt het partnerXDM schema dat hierboven verder op deze pagina wordt vermeld. |
| `destination.segmentAliases` | Kaart van segment IDs in Adobe Experience Platform namespace aan segmentaliassen in het systeem van de partner. |
| `destination.segmentNames` | Wijs van segmentnamen in Adobe Experience Platform namespace aan segmentnamen in het systeem van de partner toe. |
| `addedSegments(listOfSegments)` | Retourneert alleen de segmenten met status `realized` of `existing`. |
| `removedSegments(listOfSegments)` | Retourneert alleen de segmenten met status `exited`. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
