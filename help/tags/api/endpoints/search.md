---
title: Zoekeindpunt
description: Leer hoe te om vraag aan het /search eindpunt in Reactor API te maken.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Zoekeindpunt

Het `/search` -eindpunt in de Reactor-API biedt een manier om bronnen te zoeken die aan de gewenste criteria voldoen, uitgedrukt als een query.

De volgende API-middeltypen kunnen worden doorzocht, waarbij dezelfde gegevensstructuur wordt gebruikt als de op bronnen gebaseerde documenten die via de API worden geretourneerd:

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

Alle vragen zijn scoped aan uw huidige bedrijf en toegankelijke eigenschappen.

>[!IMPORTANT]
>
>De zoekfunctionaliteit heeft de volgende bedenkingen en uitzonderingen:
>* meta is niet doorzoekbaar en wordt niet geretourneerd in zoekresultaten.
>* Schemavelden voor afgevaardigden van extensiepakketten (handelingen, voorwaarden, enz.) kunnen worden doorzocht als tekst, niet als een geneste gegevensstructuur.
>* De vragen van de waaier steunen momenteel slechts gehelen.

Voor meer diepgaande informatie over hoe te om deze functionaliteit te gebruiken, verwijs naar de [ zoekgids ](../guides/search.md).

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [ Reactor API ](https://www.adobe.io/experience-platform-apis/references/reactor/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie betreffende hoe te voor authentiek te verklaren aan API.

## Een zoekopdracht uitvoeren {#perform}

U kunt een zoekopdracht uitvoeren door een POST aan te vragen.

**API formaat**

```http
POST /search
```

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `from` | Het aantal resultaten waarmee de reactie moet worden verschoven. |
| `size` | De maximale hoeveelheid resultaten die moet worden geretourneerd. De resultaten mogen niet groter zijn dan 100 items. |
| `query` | Een object dat de zoekquery vertegenwoordigt. Voor elke eigenschap in dit object moet de sleutel een veldpad vertegenwoordigen waarnaar moet worden gezocht. De waarde moet een object zijn waarvan de subeigenschappen bepalen waarvoor moet worden gezocht.<br><br> voor elk gebiedspad, kunt u de volgende sub-eigenschappen gebruiken:<ul><li>`exists`: retourneert true als het veld in de bron bestaat.</li><li>`value`: retourneert true als de waarde van het veld overeenkomt met de waarde van deze eigenschap.</li><li>`value_operator`: Booleaanse logica die wordt gebruikt om te bepalen hoe een `value` -query moet worden afgehandeld. Toegestane waarden zijn `AND` en `OR` . Wanneer deze optie is uitgesloten, wordt `AND` logic aangenomen. Zie de sectie over [ logica van de waardeexploitant ](#value-operator) voor meer informatie.</li><li>`range` Retourneert true als de waarde van het veld binnen een specifiek numeriek bereik valt. Het bereik zelf wordt bepaald door de volgende subeigenschappen:<ul><li>`gt`: groter dan de opgegeven waarde, niet-inclusief.</li><li>`gte`: groter dan of gelijk aan de opgegeven waarde.</li><li>`lt`: minder dan de opgegeven waarde, niet inclusief.</li><li>`lte`: kleiner dan of gelijk aan de opgegeven waarde.</li></ul></li></ul> |
| `sort` | Een array met objecten die de volgorde aangeeft waarin de resultaten moeten worden gesorteerd. Elk object moet één eigenschap bevatten: de sleutel staat voor het veldpad waarop moet worden gesorteerd, en de waarde vertegenwoordigt de sorteervolgorde (`asc` voor oplopend, `desc` voor aflopend). |
| `resource_types` | Een array van tekenreeksen die de specifieke brontypen aangeven waarnaar moet worden gezocht. |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie keert een lijst van passende middelen voor de vraag terug. Voor details op hoe API gelijken voor specifieke waarden bepaalt, zie de bijlage sectie op [ passende overeenkomsten ](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## Bijlage

De volgende sectie bevat aanvullende informatie over het gebruik van het `/search` eindpunt.

### Logica van operator voor waarden {#value-operator}

Zoekquerywaarden worden gesplitst in termen die overeenkomen met geïndexeerde documenten. Tussen elke term wordt een `AND` -relatie verondersteld.

Wanneer u `AND` als `value_operator` gebruikt, wordt een querywaarde van `My Rule Holiday Sale` geïnterpreteerd als documenten met een veld dat `My AND Rule AND Holiday AND Sale` bevat.

Wanneer u `OR` als `value_operator` gebruikt, wordt een querywaarde van `My Rule Holiday Sale` geïnterpreteerd als documenten met een veld dat `My OR Rule OR Holiday OR Sale` bevat. Hoe meer termen overeenkomen, hoe hoger de waarde `match_score`. Vanwege de aard van een gedeeltelijke overeenkomst van de termijn, wanneer niets dicht bij de gewenste waarde aanpast, kunt u een resultaatreeks verkrijgen waar de waarde slechts op een zeer eenvoudig niveau, zoals een paar karakters van tekst wordt aangepast.

### Overeenkomende conventies {#conventions}

De zoekopdracht heeft betrekking op het beantwoorden van de relevantie van een document voor een opgegeven zoekopdracht. De manier waarop documentgegevens worden geanalyseerd en geïndexeerd, heeft hier rechtstreeks invloed op.

In de volgende tabel worden de overeenkomende conventies voor gangbare veldtypen weergegeven:

| Veldtype | Overeenkomende conventies |
| --- | --- |
| Tekenreeksen | Tekst met een analyse op gedeeltelijke termijn, hoofdlettergevoelig |
| Enumwaarden | Exacte overeenkomst, hoofdlettergevoelig |
| Geheel getal | Exacte overeenkomst |
| Floats | Exacte overeenkomst |
| Tijdstempels | Exacte overeenkomst (DateTime-indeling) |
| Weergavenamen | Tekst met een analyse op gedeeltelijke termijn, hoofdlettergevoelig |

Er zijn aanvullende conventies voor specifieke velden die in de API worden weergegeven:

| Veld | Overeenkomende conventies |
| --- | --- |
| `id` | Exacte overeenkomst, hoofdlettergevoelig |
| `delegate_descriptor_id` | Exacte overeenkomst, hoofdlettergevoelig, met termen gesplitst op `::` |
| `name` | Exacte overeenkomst, hoofdlettergevoelig |
| `settings` | Tekst met een analyse op gedeeltelijke termijn, hoofdlettergevoelig |
| `type` | Exacte overeenkomst, hoofdlettergevoelig |
