---
title: Notitie-eindpunt
description: Leer hoe te om vraag aan het /notes eindpunt in Reactor API te maken.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 1%

---

# Notitie-eindpunt

In de Reactor-API zijn notities tekstuele annotaties die u aan bepaalde bronnen kunt toevoegen. Notities zijn hoofdzakelijk opmerkingen over hun respectieve middelen. De inhoud van notities is niet van invloed op het gedrag van bronnen en kan worden gebruikt voor verschillende gebruiksgevallen, zoals:

* Achtergrondinformatie opgeven
* Werken als-do lijsten
* Advies voor hulpbronnengebruik doorgeven
* Instructies geven aan andere teamleden
* Historische context opnemen

De `/notes` Het eindpunt in Reactor API staat u toe om deze nota&#39;s programmatically te beheren.

De nota&#39;s kunnen de volgende middelen worden toegepast:

* [Gegevenselementen](./data-elements.md)
* [Extensies](./extensions.md)
* [Bibliotheken](./libraries.md)
* [Properties](./properties.md)
* [Regelcomponenten](./rule-components.md)
* [Regels](./rules.md)
* [Geheimen](./secrets.md)

Deze zes types zijn collectief gekend als &quot;opmerkelijke&quot;middelen. Wanneer een opmerkelijke bron wordt verwijderd, worden de bijbehorende notities ook verwijderd.

>[!NOTE]
>
>Voor middelen die veelvoudige herzieningen kunnen hebben, moeten om het even welke nota&#39;s op de huidige (hoofd) revisie worden gecreeerd. Zij mogen niet bij andere herzieningen worden gevoegd.
>
>Notities kunnen echter nog steeds uit herzieningen worden gelezen. In dergelijke gevallen retourneert de API alleen de notities die bestonden voordat de revisie werd gemaakt. Ze bieden een momentopname van de annotaties zoals ze waren toen de revisie werd geknipt. Bij het lezen van notities uit de huidige (hoofd)revisie worden daarentegen alle notities geretourneerd.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Controleer voordat je doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe te voor authentiek te verklaren aan API.

## Een lijst met notities ophalen {#list}

U kunt een lijst met notities voor een bron ophalen door deze toe te voegen `/notes` op het pad van een GET-verzoek om de betrokken bron.

**API-indeling**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beschrijving |
| --- | --- |
| `RESOURCE_TYPE` | Het type bron waarvoor u notities ophaalt. Moet een van de volgende waarden zijn: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | De `id` van de specifieke bron waarvan u de notities wilt weergeven. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

In het volgende verzoek worden de notities weergegeven die aan een bibliotheek zijn gekoppeld.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert een lijst van nota&#39;s terug in bijlage aan het gespecificeerde middel.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Een notitie opzoeken {#lookup}

U kunt een nota opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET te verstrekken.

**API-indeling**

```http
GET /notes/{NOTE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `NOTE_ID` | De `id` van de notitie die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Als de reactie succesvol was, worden de details van de notitie geretourneerd.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## Een notitie maken {#create}

>[!WARNING]
>
>Voordat u een nieuwe notitie maakt, moet u er rekening mee houden dat notities niet bewerkbaar zijn. U kunt ze alleen verwijderen door de bijbehorende bron te verwijderen.

U kunt een nieuwe notitie maken door deze toe te voegen `/notes` op het pad van een POST-aanvraag voor de betrokken bron.

**API-indeling**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parameter | Beschrijving |
| --- | --- |
| `RESOURCE_TYPE` | Het type bron waarvoor u een notitie maakt. Moet een van de volgende waarden zijn: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | De `id` van de specifieke bron waarvoor u een notitie wilt maken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een nieuwe notitie voor een eigenschap gemaakt.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `type` | **(Vereist)** Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde zijn `notes`. |
| `attributes.text` | **(Vereist)** De tekst die de notitie bevat. Elke notitie is beperkt tot 512 Unicode-tekens. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe notitie.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
