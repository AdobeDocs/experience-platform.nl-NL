---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Hoe te om een Berekend Veld van Attributen te vormen
topic-legacy: guide
type: Documentation
description: Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit gebied kan worden gecreeerd gebruikend de Registratie API van het Schema om een schema en een groep van het douanegebied te bepalen die het gegevens verwerkte attributengebied zal houden.
exl-id: 91c5d125-8ab5-4291-a974-48dd44c68a13
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# (Alpha) vorm een gegevens verwerkt attributengebied gebruikend de Registratie API van het Schema

>[!IMPORTANT]
>
>De functie voor berekende kenmerken bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit gebied kan worden gecreeerd gebruikend de Registratie API van het Schema om een schema en een groep van het douaneschemagebied te bepalen die het gegevens verwerkte attributengebied zal houden. Het wordt aanbevolen een apart schema en een veldgroep met &quot;berekende kenmerken&quot; te maken waarin uw organisatie alle kenmerken kan toevoegen die als berekende kenmerken moeten worden gebruikt. Dit laat uw organisatie toe om het gegevens verwerkte attributenschema van andere schema&#39;s schoon te scheiden die voor gegevensopname worden gebruikt.

De workflow in dit document schetst hoe u de API voor het schemaregister kunt gebruiken om een profiel-ingeschakeld schema &quot;Berekend kenmerk&quot; te maken dat verwijst naar een aangepaste veldgroep. Dit document bevat voorbeeldcode die specifiek is voor berekende kenmerken, maar raadpleeg de [Handleiding voor schemaregistratie-API](../../xdm/api/overview.md) voor gedetailleerde informatie over het definiëren van veldgroepen en schema&#39;s met behulp van de API.

## Een veldgroep met berekende kenmerken maken

Om een gebiedsgroep tot stand te brengen die de Registratie API van het Schema gebruikt, begin door een verzoek van de POST aan het `/tenant/fieldgroups` eindpunt te doen en de details van de gebiedsgroep in het verzoeklichaam te verstrekken. Voor details betreffende het werken met gebiedsgroepen die de Registratie API van het Schema gebruiken, gelieve te verwijzen naar [de eindpuntgids van de gebiedsgroepen API](../../xdm/api/field-groups.md).

**API-indeling**

```http
POST /tenant/fieldgroups
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "title":"Computed Attributes Field Group",
        "description":"Description of the field group.",
        "type":"object",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `title` | De naam van de veldgroep die u maakt. |
| `meta:intendedToExtend` | De klasse XDM waarmee de veldgroep kan worden gebruikt. |

**Antwoord**

Een succesvol verzoek retourneert HTTP Response Status 201 (Gemaakt) met een antwoordinstantie die de details bevat van de nieuwe veldgroep, inclusief `$id`, `meta:altIt` en `version`. Deze waarden zijn alleen-lezen en worden toegewezen door het schemaregister.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.fieldgroups.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "fieldgroups",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of the field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Veldgroep bijwerken met extra berekende kenmerken

Aangezien meer gegevens verwerkte attributen nodig zijn, kunt u de gegevens verwerkte groep van het attributengebied met extra attributen bijwerken door een verzoek van de PUT aan het `/tenant/fieldgroups` eindpunt te doen. Voor deze aanvraag moet u de unieke id opnemen van de veldgroep die u in het pad hebt gemaakt en alle nieuwe velden die u in de hoofdtekst wilt toevoegen.

Voor meer informatie betreffende het bijwerken van een gebiedsgroep gebruikend de Registratie API van het Schema, gelieve te verwijzen naar [de eindpuntgids van de gebiedsgroepen API](../../xdm/api/field-groups.md).

**API-indeling**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

**Verzoek**

Dit verzoek voegt nieuwe gebieden met betrekking tot `purchaseSummary` informatie toe.

>[!NOTE]
>
>Wanneer het bijwerken van een gebiedsgroep door een verzoek van de PUT, moet het lichaam alle gebieden omvatten die worden vereist wanneer het creëren van een nieuwe gebiedsgroep in een verzoek van de POST.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Field Group",
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Description of field group.",
        "definitions": {
          "computedAttributesFieldGroup": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "meta:xdmType": "object",
                "properties": {
                  "birthdayCurrentMonth": {
                    "type": "boolean",
                    "meta:xdmType": "boolean"
                  },
                  "purchaseSummary": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                      "totalSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      },
                      "countPurchases": {
                        "meta:xdmType": "int",
                        "type": "integer",
                        "minimum": -2147483648,
                        "maximum": 2147483647
                      },
                      "averageSpend": {
                        "type": "number",
                        "meta:xdmType": "number"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/computedAttributesFieldGroup"
          }
        ]
      }'
```

**Antwoord**

Met een geslaagde reactie worden de details van de bijgewerkte veldgroep geretourneerd.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:altId": "_{TENANT_ID}.fieldgroups.860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
  "meta:resourceType": "fieldgroups",
  "version": "1.0",
  "title": "Computed Attributes Field Group",
  "type": "object",
  "description": "Description of field group.",
  "definitions": {
    "computedAttributesFieldGroup": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "birthdayCurrentMonth": {
              "type": "boolean",
              "meta:xdmType": "boolean"
            },
            "purchaseSummary": {
              "type": "object",
              "meta:xdmType": "object",
              "properties": {
                "totalSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                },
                "countPurchases": {
                  "meta:xdmType": "int",
                  "type": "integer",
                  "minimum": -2147483648,
                  "maximum": 2147483647
                },
                "averageSpend": {
                  "type": "number",
                  "meta:xdmType": "number"
                }
              }
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/computedAttributesFieldGroup",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612861108205,
    "repo:lastModifiedDate": 1612861108205,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "627faa3346d3004aef2010e9bd2b7e721b19ae7857b276f3ef733e6e732d495f",
    "meta:globalLibVersion": "1.19.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een schema maken dat geschikt is voor profielen

Om een schema tot stand te brengen gebruikend de Registratie API van het Schema, begin door een verzoek van de POST aan het `/tenant/schemas` eindpunt te doen en de details van het schema in het verzoeklichaam te verstrekken. Het schema moet ook voor [!DNL Profile] worden toegelaten en als deel van het verenigingsschema voor de schemaklasse verschijnen.

Voor meer informatie over [!DNL Profile]-Toegelaten schema&#39;s en verenigingsschema&#39;s, te herzien gelieve [[!DNL Schema Registry] API gids](../../xdm/api/overview.md) en [de documentatie van de schemacompositie](../../xdm/schema/composition.md).

**API-indeling**

```http
POST /tenants/schemas
```

**Verzoek**

Het volgende verzoek leidt tot een nieuw schema dat verwijzingen `computedAttributesFieldGroup` eerder in dit document (gebruikend zijn unieke identiteitskaart) wordt gecreeerd en voor het de unieschema van het Profiel (gebruikend `meta:immutableTags` serie) wordt toegelaten. Voor gedetailleerde instructies op hoe te om een schema tot stand te brengen gebruikend de Registratie API van het Schema, gelieve te verwijzen naar [schema&#39;s API eindpuntgids](../../xdm/api/schemas.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "type": "object",
        "title": "Computed Attributes Schema",
        "meta:extensible": false,
        "meta:abstract": false,
        "meta:immutableTags": [
          "union"
        ],
        "meta:extends": [
          "https://ns.adobe.com/xdm/context/profile",
          "https://ns.adobe.com/xdm/context/identitymap",
          "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
        ],
        "description": "Description of schema.",
        "definitions": {
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
          },
          {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
          },
          {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
          }
        ],
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
      }' 
```

**Antwoord**

Een succesvolle reactie retourneert HTTP-status 201 (gemaakt) en een lading die de details bevat van het nieuwe schema, inclusief `$id`, `meta:altId` en `version`. Deze waarden zijn alleen-lezen en worden toegewezen door het schemaregister.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:altId": "_{TENANT}.schemas.699c1f16821c51086394fef8233d7fdb61e6f5b574b5a230",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Computed Attributes Schema",
  "type": "object",
  "description": "Description of schema.",
  "definitions": {},
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/identitymap",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/xdm/context/identitymap",
    "https://ns.adobe.com/{TENANT_ID}/fieldgroups/860ad1b1b35e0a88ecf6df92ebce08335c180313d5805352"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1612385766411,
    "repo:lastModifiedDate": 1612385766411,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "a9c6b5c25c109970ffa5eaeb3db2b47b59c696e1d9407fb39ccf7e48b74b558e",
    "meta:globalLibVersion": "1.18.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "{SANDBOX_ID}",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT}",
  "meta:immutableTags": [
    "union"
  ]
}
```

## Volgende stappen

Nu u een schema en gebiedsgroep hebt gecreeerd waarin uw gegevens verwerkte attributen zullen worden opgeslagen, kunt u de gegevens verwerkte attributen tot stand brengen gebruikend het `/computedattributes` API eindpunt. Voor gedetailleerde stappen aan het creëren van een gegevens verwerkt attribuut in API, volg de stappen die in [gegevens verwerkte attributen API eindpuntgids](ca-api.md) worden verstrekt.
