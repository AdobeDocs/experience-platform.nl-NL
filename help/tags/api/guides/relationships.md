---
title: Relaties in de Reactor-API
description: Leer hoe u bronrelaties vastlegt in de Reactor-API, inclusief de relatievereisten voor elke bron.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# Relaties in de Reactor-API

Bronnen in de Reactor-API zijn vaak verwant aan elkaar. Dit document biedt een overzicht van hoe de bronrelaties worden vastgelegd in de API en de relatievereisten van elk type bron.

Afhankelijk van het soort middel in kwestie, worden sommige verhoudingen vereist. Een vereiste relatie houdt in dat de bovenliggende bron niet kan bestaan zonder de relatie. Alle andere relaties zijn optioneel.

Ongeacht of ze verplicht of optioneel zijn, worden relaties automatisch door het systeem tot stand gebracht wanneer relevante bronnen worden gemaakt, of ze moeten handmatig worden gemaakt. In het geval van het manueel creëren van verhoudingen, zijn er twee mogelijke methodes afhankelijk van de betrokken bron:

* [Maken op basis van lading](#payload)
* [Maken via URL](#url) (alleen voor bibliotheken)

Zie de sectie over [relatievereisten](#requirements) voor een lijst van de compatibele relaties voor elk middeltype, en de methodes die worden vereist om die relaties tot stand te brengen waar toepasselijk.

## Een relatie maken met een payload {#payload}

Sommige verhoudingen moeten manueel worden gevestigd wanneer u aanvankelijk een middel creeert. Hiervoor moet u een `relationship` -object in de aanvraagpayload wanneer u de bovenliggende bron voor het eerst maakt. Voorbeelden van deze relaties zijn:

* [Een gegevenselement maken](../endpoints/data-elements.md#create) met de vereiste extensies
* [Een omgeving maken](../endpoints/environments.md#create) met de vereiste gastheerverhouding

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De id van de eigenschap waartoe de resource behoort. |
| `{RESOURCE_TYPE}` | Het type bron dat moet worden gemaakt. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met de volgende aanvraag wordt een nieuwe `rule_component`, betrekkingen aan te knopen met `rules` en `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `relationships` | Een object dat moet worden opgegeven wanneer u relaties via een payload maakt. Elke sleutel in dit object vertegenwoordigt een specifiek relatietype. In het bovenstaande voorbeeld: `extension` en `rules` er relaties worden ingesteld die met name betrekking hebben op `rule_components`. Voor meer informatie over compatibele relatietypen voor verschillende middelen, zie de sectie over [relatievereisten per bron](#relationship-requirements-by-resource). |
| `data` | Elk relatietype dat onder `relationship` object moet een `data` eigenschap, die verwijst naar de `id` en `type` van de bron waarmee een relatie tot stand wordt gebracht. U kunt een relatie maken met meerdere bronnen van hetzelfde type door de `data` eigenschap als een array van objecten, waarbij elk object het `id` en `type` van een toepasselijke bron. |
| `id` | De unieke id van een bron. Elk `id` moet vergezeld gaan van een `type` eigenschap, met vermelding van het soort bron in kwestie. |
| `type` | Het type resource waarnaar wordt verwezen door een zustergebruiker `id` veld. Inclusief geaccepteerde waarden `data_elements`, `rules`, `extensions`, en `environments`. |

{style=&quot;table-layout:auto&quot;}

## Een relatie via URL maken {#url}

In tegenstelling tot andere bronnen maken bibliotheken relaties tot stand via hun eigen toegewijde `/relationship` eindpunten. Voorbeelden zijn:

* [Extensies, gegevenselementen en regels toevoegen aan een bibliotheek](../endpoints/libraries.md#add-resources)
* [Bibliotheek toewijzen aan een omgeving](../endpoints/libraries.md#environment)

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De id van de eigenschap waartoe de bibliotheek behoort. |
| `{LIBRARY_ID}` | De id van de bibliotheek waarvoor u een relatie wilt maken. |
| `{RESOURCE_TYPE}` | Het type van middel de verhouding richt zich. Beschikbare waarden zijn `environment`, `data_elements`, `extensions`, en `rules`. |

**Verzoek**

In het volgende verzoek wordt het `/relationships/environment` eindpunt voor een bibliotheek om een verhouding met een milieu tot stand te brengen.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `data` | Een object dat verwijst naar het `id` en `type` van de doelbron voor de relatie. Als u een relatie maakt met meerdere bronnen van hetzelfde type (zoals `extensions` en `rules`), de `data` eigenschap moet worden opgemaakt als een array van objecten, waarbij elk object het `id` en `type` van een toepasselijke bron. |
| `id` | De unieke id van een bron. Elk `id` moet vergezeld gaan van een `type` eigenschap, met vermelding van het soort bron in kwestie. |
| `type` | Het type resource waarnaar wordt verwezen door een zustergebruiker `id` veld. Inclusief geaccepteerde waarden `data_elements`, `rules`, `extensions`, en `environments`. |

{style=&quot;table-layout:auto&quot;}

## Vereisten inzake relatie per bron {#requirements}

De volgende lijsten schetsen de beschikbare verhoudingen voor elk middeltype, al dan niet die verhoudingen worden vereist, en de toegelaten methode om de verhouding manueel tot stand te brengen waar toepasselijk.

>[!NOTE]
>
>Als een relatie niet wordt vermeld als wordt gecreeerd door lading of URL, dan wordt het automatisch toegewezen door het systeem.

### Gebeurtenissen van Audit

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Builds

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Callbacks

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Bedrijven

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Gegevenselementen

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Omgevingen

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Extensies

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Gastheren

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Bibliotheken

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Notities

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Properties

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Regelcomponenten

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### Regels

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### Geheimen

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

