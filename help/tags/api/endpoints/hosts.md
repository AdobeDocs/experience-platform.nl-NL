---
title: Het eindpunt van hosts
description: Leer hoe te om vraag aan het /hosts eindpunt in Reactor API te maken.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 1%

---

# Het eindpunt van hosts

>[!NOTE]
>
>In dit document wordt beschreven hoe u hosts in de Reactor-API beheert. Voor meer algemene informatie over gastheren voor markeringen, zie de gids op [gastheren overzicht](../../ui/publishing/hosts/hosts-overview.md) in de het publiceren documentatie.

In de Reactor-API definieert een host een bestemming waar een [build](./builds.md) kan worden geleverd.

Wanneer een gebruiker van tags in Adobe Experience Platform een build aanvraagt, controleert het systeem de Library om te bepalen naar welke [omgeving](./environments.md) de bibliotheek moet worden gebouwd. Elke omgeving heeft een relatie met een host die aangeeft waar de build moet worden geleverd.

Een gastheer behoort tot precies één [bezit](./properties.md), terwijl een bezit vele gastheren kan hebben. Een eigenschap moet ten minste één host hebben voordat u deze kunt publiceren.

Een host kan door meerdere omgevingen binnen een eigenschap worden gebruikt. Het is gemeenschappelijk om één enkele gastheer op een bezit te hebben, en alle milieu&#39;s op dat bezit te hebben gebruiken de zelfde gastheer.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Lees voordat u doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe u de API kunt verifiëren.

## Een lijst met hosts ophalen {#list}

U kunt een lijst van gastheren voor een bezit terugwinnen door identiteitskaart van het bezit in de weg van een verzoek van de GET te omvatten.

**API-indeling**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de eigenschap die eigenaar is van de hosts. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Gebruikend vraagparameters, kunnen de vermelde gastheren worden gefiltreerd gebaseerd op de volgende attributen:<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>Zie de gids op [het filtreren reacties](../guides/filtering.md) voor meer informatie.

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert een lijst van gastheren voor het gespecificeerde bezit terug.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## Een gastheer opzoeken {#lookup}

U kunt een gastheer opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET te verstrekken.

**API-indeling**

```http
GET /hosts/{HOST_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `HOST_ID` | De `id` van de host die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de host.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## Een host maken {#create}

U kunt een nieuwe gastheer tot stand brengen door een verzoek van de POST te doen.

**API-indeling**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| Parameter | Beschrijving |
| --- | --- |
| `PROPERTY_ID` | De `id` van de [eigenschap](./properties.md) die u onder de host definieert. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt een nieuwe host voor de opgegeven eigenschap gemaakt. De vraag associeert ook de gastheer met een bestaande uitbreiding door het `relationships` bezit. Zie de gids op [relaties](../guides/relationships.md) voor meer informatie.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes.name` | **(Vereist)** Een leesbare naam voor de host. |
| `attributes.type_of` | **(Vereist)** Het type host. U kunt uit twee opties kiezen: <ul><li>`akamai` voor  [door Adobe beheerde hosts](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` voor  [SFTP-hosts](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | Een optionele persoonlijke sleutel die moet worden gebruikt voor hostverificatie. |
| `attributes.path` | Het pad dat moet worden toegevoegd aan de URL `server`. |
| `attributes.port` | Een geheel getal dat de specifieke serverpoort aangeeft die moet worden gebruikt. |
| `attributes.server` | De host-URL voor de server. |
| `attributes.username` | Een optionele gebruikersnaam voor verificatie. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde `hosts` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de zojuist gemaakte host.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## Een host bijwerken {#update}

>[!NOTE]
>
>Alleen SFTP-hosts kunnen worden bijgewerkt.

U kunt een gastheer bijwerken door zijn identiteitskaart in de weg van een verzoek van de PATCH te omvatten.

**API-indeling**

```http
PATCH /hosts/{HOST_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `HOST_ID` | De `id` van de host die u wilt bijwerken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt `name` voor een bestaande host bijgewerkt.

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | Een object waarvan de eigenschappen de kenmerken vertegenwoordigen die voor de host moeten worden bijgewerkt. De volgende kenmerken kunnen voor een host worden bijgewerkt: <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | De `id` van de host die u wilt bijwerken. Dit zou de `{HOST_ID}` waarde moeten aanpassen die in de verzoekweg wordt verstrekt. |
| `type` | Het type resource dat wordt bijgewerkt. Voor dit eindpunt, moet de waarde `hosts` zijn. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de bijgewerkte host.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## Een host verwijderen

U kunt een gastheer schrappen door zijn identiteitskaart in de weg van een verzoek van de DELETE op te nemen.

**API-indeling**

```http
DELETE /hosts/{HOST_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `HOST_ID` | De `id` van de host die u wilt verwijderen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder antwoord, wat aangeeft dat de host is verwijderd.

## Verwante bronnen voor een host ophalen {#related}

De volgende vraag toont aan hoe te om de verwante middelen voor een gastheer terug te winnen. Als [een host](#lookup) opzoekt, worden deze relaties vermeld onder de eigenschap `relationships`.

Zie de [relatiehandleiding](../guides/relationships.md) voor meer informatie over relaties in de Reactor-API.

### De verwante eigenschap voor een host opzoeken {#property}

U kunt het bezit opzoeken dat een gastheer bezit door `/property` aan de weg van een raadplegingsverzoek toe te voegen.

**API-indeling**

```http
GET /hosts/{HOST_ID}/property
```

| Parameter | Beschrijving |
| --- | --- |
| `{HOST_ID}` | De `id` van de host waarvan u de eigenschap wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert de details van het gespecificeerde bezit van de gastheer terug.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
