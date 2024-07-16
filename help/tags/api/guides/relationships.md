---
title: Relaties in de Reactor-API
description: Leer hoe u bronrelaties vastlegt in de Reactor-API, inclusief de relatievereisten voor elke bron.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---

# Relaties in de Reactor-API

Bronnen in de Reactor-API zijn vaak verwant aan elkaar. Dit document biedt een overzicht van hoe de bronrelaties worden vastgelegd in de API en de relatievereisten van elk type bron.

Afhankelijk van het soort middel in kwestie, worden sommige verhoudingen vereist. Een vereiste relatie houdt in dat de bovenliggende bron niet kan bestaan zonder de relatie. Alle andere relaties zijn optioneel.

Ongeacht of ze verplicht of optioneel zijn, worden relaties automatisch door het systeem tot stand gebracht wanneer relevante bronnen worden gemaakt, of ze moeten handmatig worden gemaakt. In het geval van het manueel creëren van verhoudingen, zijn er twee mogelijke methodes afhankelijk van de betrokken bron:

* [Maken op basis van lading](#payload)
* [ creeert door URL ](#url) (voor slechts bibliotheken)

Verwijs naar de sectie over [ relatievereisten ](#requirements) voor een lijst van de compatibele verhoudingen voor elk middeltype, en de methodes die worden vereist om die verhoudingen te vestigen waar toepasselijk.

## Een relatie maken op basis van een payload {#payload}

Sommige verhoudingen moeten manueel worden gevestigd wanneer u aanvankelijk een middel creeert. Hiervoor moet u een `relationship` -object opgeven in de payload van de aanvraag wanneer u de bovenliggende bron maakt. Voorbeelden van deze relaties zijn:

* [ Creërend een gegevenselement ](../endpoints/data-elements.md#create) met de vereiste uitbreidingen
* [ Creërend een milieu ](../endpoints/environments.md#create) met de vereiste gastheerverhouding

**API formaat**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De id van de eigenschap waartoe de resource behoort. |
| `{RESOURCE_TYPE}` | Het type bron dat moet worden gemaakt. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende aanvraag wordt een nieuwe `rule_component` gemaakt die relaties tot stand brengt met `rules` en een `extension` .

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
| `relationships` | Een object dat moet worden opgegeven wanneer u relaties via een payload maakt. Elke sleutel in dit object vertegenwoordigt een specifiek relatietype. In het bovenstaande voorbeeld worden `extension` - en `rules` -relaties tot stand gebracht, die specifiek zijn voor `rule_components` . Voor meer informatie over compatibele relatietypen voor verschillende middelen, zie de sectie over [ relatievereisten door middel ](#relationship-requirements-by-resource). |
| `data` | Elk relatietype dat onder het `relationship` -object wordt opgegeven, moet een `data` -eigenschap bevatten, die verwijst naar de `id` en `type` van de bron waarmee een relatie wordt ingesteld. U kunt een relatie maken met meerdere bronnen van hetzelfde type door de eigenschap `data` op te maken als een array van objecten, waarbij elk object de `id` en `type` van een toepasselijke bron bevat. |
| `id` | De unieke id van een bron. Elke `id` moet vergezeld gaan van een eigenschap `type` sibling die het type van de bron in kwestie aangeeft. |
| `type` | Het type resource waarnaar wordt verwezen door een verwant `id` veld. Tot de toegestane waarden behoren `data_elements`, `rules`, `extensions` en `environments` . |

{style="table-layout:auto"}

## Een relatie via URL maken {#url}

In tegenstelling tot andere bronnen maken bibliotheken relaties tot stand via hun eigen toegewijde `/relationship` eindpunten. Voorbeelden zijn:

* [Extensies, gegevenselementen en regels toevoegen aan een bibliotheek](../endpoints/libraries.md#add-resources)
* [Bibliotheek toewijzen aan een omgeving](../endpoints/libraries.md#environment)

**API formaat**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De id van de eigenschap waartoe de bibliotheek behoort. |
| `{LIBRARY_ID}` | De id van de bibliotheek waarvoor u een relatie wilt maken. |
| `{RESOURCE_TYPE}` | Het type van middel de verhouding richt zich. Beschikbare waarden zijn `environment` , `data_elements` , `extensions` en `rules` . |

**Verzoek**

In het volgende verzoek wordt het eindpunt `/relationships/environment` voor een bibliotheek gebruikt om een relatie met een omgeving te maken.

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
| `data` | Een object dat verwijst naar de `id` en `type` van de doelbron voor de relatie. Wanneer u een relatie maakt met meerdere bronnen van hetzelfde type (zoals `extensions` en `rules` ), moet de eigenschap `data` worden opgemaakt als een array van objecten, waarbij elk object de `id` en `type` van een toepasselijke bron bevat. |
| `id` | De unieke id van een bron. Elke `id` moet vergezeld gaan van een eigenschap `type` sibling die het type van de bron in kwestie aangeeft. |
| `type` | Het type resource waarnaar wordt verwezen door een verwant `id` veld. Tot de toegestane waarden behoren `data_elements`, `rules`, `extensions` en `environments` . |

{style="table-layout:auto"}

## Vereisten inzake relatie per bron {#requirements}

De volgende lijsten schetsen de beschikbare verhoudingen voor elk middeltype, al dan niet die verhoudingen worden vereist, en de toegelaten methode om de verhouding manueel tot stand te brengen waar toepasselijk.

>[!NOTE]
>
>Als een relatie niet wordt vermeld als wordt gecreeerd door lading of URL, dan wordt het automatisch toegewezen door het systeem.

### Controlegebeurtenissen

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | |
| `entity` | ✓ | | |

{style="table-layout:auto"}

### Builds

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `data_elements` | | | |
| `extensions` | | | |
| `rules` | | | |
| `environment` | ✓ | | |
| `library` | ✓ | | |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Callbacks

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Bedrijven

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `properties` | | | |

{style="table-layout:auto"}

### Gegevenselementen

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ | | |
| `notes` | | | |
| `property` | ✓ | | |
| `origin` | ✓ | | |
| `extension` | ✓ | ✓ | |
| `updated_with_extension` | ✓ | | |
| `updated_with_extension_package` | ✓ | | |

{style="table-layout:auto"}

### Omgevingen

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `library` | | | |
| `builds` | | | |
| `host` | ✓ | ✓ | |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Extensies

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ | | |
| `notes` | | | |
| `property` | ✓ | | |
| `origin` | ✓ | | |
| `extension_package` | ✓ | ✓ | |
| `updated_with_extension_package` | ✓ | | |

{style="table-layout:auto"}

### Gastheren

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | |

{style="table-layout:auto"}

### Bibliotheken

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `builds` | | | |
| `environment` | | | ✓ |
| `data_elements` | | | ✓ |
| `extensions` | | | ✓ |
| `rules` | | | ✓ |
| `notes` | | | |
| `upstream_library` | ✓ | | |
| `property` | ✓ | | |
| `last_build` | | | |

{style="table-layout:auto"}

### Notities

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ | | |

{style="table-layout:auto"}

### Properties

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ | | |
| `callbacks` | | | |
| `environments` | | | |
| `libraries` | | | |
| `data_elements` | | | |
| `extensions` | | | |
| `extensions` | | | |

{style="table-layout:auto"}

### Regelcomponenten

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ | | |
| `updated_with_extension` | ✓ | | |
| `extension` | ✓ | ✓ | |
| `notes` | | | |
| `origin` | ✓ | | |
| `property` | ✓ | | |
| `rules` | ✓ | ✓ | |
| `revisions` | ✓ | | |

{style="table-layout:auto"}

### Regels

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ | | |
| `notes` | | | |
| `property` | ✓ | | |
| `origin` | ✓ | | |
| `rule_components` | | | |

### Geheimen

| Relatie | Vereist | Maken op basis van lading | Maken via URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ | | ✓ |
| `environment` | ✓ | ✓ | |

