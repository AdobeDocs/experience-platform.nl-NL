---
description: Gebruik de inhoud op deze pagina samen met de rest configuratieopties voor partnerbestemmingen. Deze pagina richt het overseinenformaat van gegevens die van Adobe Experience Platform aan bestemmingen worden uitgevoerd, terwijl de andere pagina specifiek over het verbinden en het voor authentiek verklaren aan uw bestemming richt.
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: Berichtindeling
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 63fe3b7cc429a1c18cebe998bc82fdea99a6679b
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 1%

---

# Berichtindeling

## Voorwaarden - Adobe Experience Platform-concepten {#prerequisites}

Om het proces aan de kant van de Adobe te begrijpen, gelieve zich met de volgende concepten van het Experience Platform vertrouwd te maken:

* **Experience Data Model (XDM)**. [XDM ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=nl) overviewand   [How to create an XDM schema in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Klasse**. [Maak en bewerk klassen in de gebruikersinterface](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **Veldgroep**. [Veldgroepdefinitie ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#field-group) en  [meer informatie over veldgroepen](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#field-group).
* **IdentityMap**. Het identiteitsoverzicht is een kaart van alle eindgebruikersidentiteiten in Adobe Experience Platform. Raadpleeg `xdm:identityMap` in het [XDM-veldwoordenboek](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. Het [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM attribuut deelt welke segmenten een profiel een lid van is. Voor de drie verschillende waarden op het `status` gebied, lees de documentatie op [het schemagroep van de Details van het Lidmaatschap van het Segment ](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Overzicht {#overview}

Gebruik de inhoud op deze pagina samen met de rest van [configuratieopties voor partnerbestemmingen](./configuration-options.md). Deze pagina richt het overseinenformaat van gegevens die van Adobe Experience Platform aan bestemmingen worden uitgevoerd, terwijl de andere pagina specifiek over het verbinden en het voor authentiek verklaren aan uw bestemming richt.

Adobe Experience Platform exporteert gegevens naar een aanzienlijk aantal bestemmingen, in verschillende gegevensindelingen. Voorbeelden van doelsoorten zijn reclameplatforms (Google), sociale netwerken (Facebook), cloudopslaglocaties (Amazon S3, Azure Event Hubs).

Experience Platform kan de geëxporteerde berichtindeling aanpassen aan de verwachte indeling aan uw zijde. Om deze aanpassing te begrijpen, zijn de volgende concepten belangrijk:
* Het XDM-bronschema (1) en het XDM-doelschema (2) in Adobe Experience Platform
* Het berichtformaat aan de partnerkant (3), en
* De transformatielaag tussen twee, die u kunt bepalen door een [berichttransformatiesjabloon](./message-format.md#using-templating) te creëren.

![Transformatie schema naar JSON](./assets/transformations-3-steps.png)

Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven.

De gebruikers die gegevens aan uw bestemming willen activeren moeten de gebieden in kaart brengen die zij voor hun datasets in Experience Platform aan een schema gebruiken dat aan het verwachte formaat van uw bestemming vertaalt. Adobe zal een groep van het douanegebied voor uw bedrijf tot stand brengen om aan het doelschema toe te voegen. De velden in de veldgroep zijn afhankelijk van de profielkenmerkvelden die u kunt ontvangen.

**Bron-XDM-schema (1)**: Dit verwijst naar het schema dat een klant in Experience Platform gebruikt. In Experience Platform, in [toewijzingsstap](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) van het activerende bestemmingswerkschema, zouden de klanten gebieden van hun bronschema aan het doelschema van uw bestemming in kaart brengen (2).

**Doel XDM-schema (2)**: Gebaseerd op het JSON standaardschema (3) dat u met Adobe deelt, zal het team bij Adobe een douaneschema voor uw bestemming tot stand brengen. Merk op dat in een [toekomstige fase van het project](./overview.md#phased-approach), u het douaneschema voor uw bestemming op uw kunt tot stand brengen.

**JSON-standaardschema van uw kenmerken van het doelprofiel (3)**: Deel met ons een  [JSON-](https://json-schema.org/learn/miscellaneous-examples.html) schema met alle profielkenmerken die uw platform ondersteunt en de typen kenmerken ervan (bijvoorbeeld: object, tekenreeks, array). Voorbeelden van velden die uw doel kan ondersteunen, zijn `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` enzovoort.

Gebaseerd op de hierboven beschreven schematransformaties, is hier hoe de structuur van een bericht tussen het bronXDM schema en het steekproefschema op de partnerkant verandert:

![Voorbeeld van transformatieberichten](./assets/transformations-with-examples.png)

<br> 


## Aan de slag - drie basiskenmerken transformeren {#getting-started}

In het onderstaande voorbeeld worden drie algemene profielkenmerken in Adobe Experience Platform gebruikt om het transformatieproces te demonstreren: **voornaam**, **achternaam** en **e-mailadres**.

>[!NOTE]
>
>De klant wijst de attributen van het bronXDM schema aan het partnerXDM schema in Adobe Experience Platform UI, in **Toewijzing** stap van [activeert bestemmingswerkschema](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate-destinations.html#mapping) in kaart.

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

Deze sectie verstrekt verscheidene voorbeelden van hoe deze transformaties, van het inputXDM schema, door het malplaatje worden gemaakt, en uitvoer in ladingsformaten die door uw bestemming worden goedgekeurd. De onderstaande voorbeelden worden als volgt gesorteerd op toenemende complexiteit:

1. Eenvoudige transformatievoorbeelden. Leer hoe sjablonen werken met eenvoudige transformaties voor [Profielkenmerken](./message-format.md#attributes), [Segmentlidmaatschap](./message-format.md#segment-membership) en [Identiteitsvelden](./message-format.md#identities).
2. Eenvoudigere voorbeelden van sjablonen waarin bovenstaande velden worden gecombineerd: [Maak een sjabloon voor het verzenden van segmenten en identiteiten](./message-format.md#segments-and-identities) en [Maak een sjabloon voor het verzenden van segmenten, identiteiten en profielkenmerken](./message-format.md#segments-identities-attributes).
3. Sjablonen bevatten de aggregatietoets. Wanneer u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) in de bestemmingsconfiguratie gebruikt, groepeert het Experience Platform de profielen die aan uw bestemming worden uitgevoerd die op criteria zoals segment ID, segmentstatus, of identiteitsnamespaces wordt gebaseerd.

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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

### Een aggregatietoets opnemen in uw sjabloon om geëxporteerde profielen te groeperen op basis van verschillende criteria {#template-aggregation-key}

Wanneer u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) in de bestemmingsconfiguratie gebruikt, kunt u het malplaatje van de berichttransformatie uitgeven om de profielen te groeperen die naar uw bestemming op criteria zoals segmentidentiteitskaart, segmentalias, segmentlidmaatschap, of identiteitsnamespaces worden uitgevoerd, zoals aangetoond in de hieronder voorbeelden.

#### Voorbeeld van het gebruik van de segment-ID-aggregatietoets in de sjabloon {#aggregation-key-segment-id}

Als u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) gebruikt en `includeSegmentId` aan waar plaatst, kunt u `segmentId` in het malplaatje aan groepsprofielen in de berichten van HTTP gebruiken die aan uw bestemming worden uitgevoerd:

**Invoer**

Denk aan de vier onderstaande profielen, waarbij de eerste twee deel uitmaken van het segment met de segment-id `788d8874-8007-4253-92b7-ee6b6c20c6f3` en de andere twee deel uitmaken van het segment met de segment-id `8f812592-3f06-416b-bd50-e7831848a31a`.

Profiel 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      },
      "birthDate":{
         
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
      },
      "birthDate":{
         "value":"1980/07/31"
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
      },
      "birthDate":{
         
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
      },
      "birthDate":{
         "value":"1940/01/01"
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

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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
    "audienceId": "{{input.aggregationKey.segmentId}}"
}
```

**Resultaat**

Als de profielen naar uw bestemming worden geëxporteerd, worden ze in twee groepen gesplitst op basis van hun segment-id.

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
    ],
    "audienceId": "788d8874-8007-4253-92b7-ee6b6c20c6f3"
}
```

```json
{
    "profiles": [
        {
            "firstName": "Tom",
            "birthDate": null
        },
        {
            "firstName": "Jerry",
            "birthDate": "1940/01/01"
        }
    ],
    "audienceId": "8f812592-3f06-416b-bd50-e7831848a31a"
}
```

#### Voorbeeld van het gebruik van de samenvoegingssleutel van segmenten in de sjabloon {#aggregation-key-segment-alias}

Als u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) en reeks `includeSegmentId` aan waar gebruikt, kunt u segmentalias in het malplaatje aan groepsprofielen in de berichten van HTTP gebruiken die aan uw bestemming worden uitgevoerd.

Voeg de onderstaande regel aan de sjabloon toe om geëxporteerde profielen te groeperen op basis van de segmentalias.

```python
"customerList={{input.aggregationKey.segmentAlias}}"
```

#### Voorbeeld van het gebruik van de samenvoegingssleutel voor de segmentstatus in de sjabloon {#aggregation-key-segment-status}

Als u [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) gebruikt en `includeSegmentId` en `includeSegmentStatus` aan waar plaatst, kunt u de segmentstatus in het malplaatje aan groepsprofielen in de HTTP- berichten gebruiken die aan uw bestemming worden uitgevoerd op of de profielen zouden moeten worden toegevoegd of uit segmenten worden verwijderd.

Mogelijke waarden zijn:

* gereed
* bestaand
* verlaten

Voeg op basis van bovenstaande waarden de onderstaande regel toe aan de sjabloon om profielen toe te voegen aan of te verwijderen uit segmenten.:

```python
"action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}"
```

#### Voorbeeld van het gebruik van aggregatietoets voor naamruimte in de sjabloon {#aggregation-key-identity}

Hieronder ziet u een voorbeeld waarin de [configureerbare samenvoeging](./destination-configuration.md#configurable-aggregation) in de doelconfiguratie is ingesteld op het samenvoegen van geëxporteerde profielen via naamruimten, in de notatie `"identityNamespaces": ["email", "phone"]`

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
      ]
   }
}
```

**Sjabloon**

>[!IMPORTANT]
>
>Voor alle sjablonen die u gebruikt, moet u de ongeldige tekens, zoals dubbele aanhalingstekens `""`, weglaten voordat u de sjabloon invoegt in de configuratie [doelserver](./server-and-template-configuration.md#template-specs). Voor meer informatie over het ontsnappen van dubbele citaten, zie Hoofdstuk 9 in [JSON norm](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

In de onderstaande `json` worden de gegevens weergegeven die uit Adobe Experience Platform zijn geëxporteerd.

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

#### Voorbeeld van het gebruik van de samenvoegingssleutel in een URL-sjabloon

Afhankelijk van het gebruik dat u gebruikt, kunt u ook de hier in een URL beschreven aggregatietoetsen gebruiken, zoals hieronder wordt getoond:

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
