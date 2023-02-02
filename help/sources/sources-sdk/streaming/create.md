---
title: Een nieuwe verbindingsspecificatie maken voor Streaming SDK met de Flow Service API
description: Het volgende document verstrekt stappen op hoe te om een verbindingsspecificatie tot stand te brengen gebruikend de Dienst API van de Stroom en een nieuwe bron door Zelfbediening Bronnen te integreren.
hide: true
hidefromtoc: true
source-git-commit: f91ebcf8e27fd7d9019c5bb6d270b89fd08785ef
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# Een nieuwe verbindingsspecificatie maken met de opdracht [!DNL Flow Service] API

Een verbindingsspecificatie vertegenwoordigt de structuur van een bron. Het bevat informatie over de authentificatievereisten van een bron, bepaalt hoe de brongegevens kunnen worden onderzocht en worden geïnspecteerd, en verstrekt informatie over de attributen van een bepaalde bron. De `/connectionSpecs` in de [!DNL Flow Service] API staat u toe om de verbindingsspecificaties binnen uw organisatie programmatically te beheren.

In het volgende document worden de volgende stappen beschreven voor het maken van een verbindingsspecificatie met de opdracht [!DNL Flow Service] API en een nieuwe bron integreren via Self-Serve Sources (Streaming SDK).

## Aan de slag

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Artefacten verzamelen

Als u een nieuwe streamingbron wilt maken met behulp van Self-Serve Sources, moet u eerst coördineren met Adobe, een persoonlijke Git-opslagplaats aanvragen en op de details met betrekking tot het label, de beschrijving, de categorie en het pictogram voor uw bron uitlijnen met Adobe.

Zodra u de Git-opslagruimte hebt opgegeven, moet u deze als volgt structureren:

* Bronnen
   * {your_source}
      * Artefacten
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| Artefacten (bestandsnamen) | Beschrijving | Voorbeeld |
| --- | --- | --- |
| {your_source} | De naam van de bron. Deze map moet alle artefacten bevatten die betrekking hebben op uw bron, in uw persoonlijke Git-opslagplaats. | `medallia` |
| {your_source}-category.txt | De categorie waartoe uw bron behoort, opgemaakt als een tekstbestand. **Opmerking**: Neem contact op met uw Adobe als u van mening bent dat de bron niet in een van de bovenstaande categorieën past. | `medallia-category.txt` Geef in het bestand de categorie van de bron op, bijvoorbeeld: `streaming`. |
| {your_source}-description.txt | Een korte beschrijving van de bron. | [!DNL Medallia] is een marketingautomatiseringsbron die u kunt gebruiken om [!DNL Medallia] gegevens naar Experience Platform. |
| {your_source}-icon.svg | De afbeelding die moet worden gebruikt om uw bron weer te geven in de catalogus met bronnen in het Experience Platform. Dit pictogram moet een SVG-bestand zijn. |
| {your_source}-label.txt | De naam van de bron zoals deze moet worden weergegeven in de catalogus met bronnen van het Experience Platform. | Medallia |
| {your_source}-connectionSpec.json | Een JSON-bestand dat de verbindingsspecificatie van uw bron bevat. Dit bestand is in eerste instantie niet vereist omdat u de verbindingsspecificatie invult als u deze handleiding invult. | `medallia-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Tijdens de testperiode van uw verbindingsspecificatie, in plaats van zeer belangrijke waarden, kunt u gebruiken `text` in het verbindingsdossier.

Nadat u de benodigde bestanden hebt toegevoegd aan uw persoonlijke Git-opslagplaats, moet u een pull-aanvraag (PR) maken die door Adobe kan worden gecontroleerd. Wanneer uw PR wordt goedgekeurd en samengevoegd, zult u van identiteitskaart worden voorzien die voor uw verbindingsspecificatie kan worden gebruikt om naar het etiket, de beschrijving, en het pictogram van uw bron te verwijzen.

Voer vervolgens de onderstaande stappen uit om uw verbindingsspecificatie te configureren. Voor extra begeleiding op de verschillende functionaliteiten die u aan uw bron kunt toevoegen, zoals geavanceerd het plannen, douaneschema, of verschillende paginatypen, te herzien gelieve de gids op [bronspecificaties configureren](../config/sourcespec.md).

## Sjabloon voor verbindingsspecificatie kopiëren

Nadat u de vereiste artefacten hebt verzameld, kopieert en plakt u de onderstaande sjabloon voor de verbindingsspecificatie naar de teksteditor van uw keuze en werkt u de kenmerken tussen haakjes bij `{}` met informatie die relevant is voor uw specifieke bron.

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [

  ],
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "Generic-Streaming"
        },
        "description": {
          "text": "Generic Streaming Connector"
        },
        "label": {
          "text": "Generic"
        },
        "frequency": {
          "text": "streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## Een verbindingsspecificatie maken {#create}

Nadat u de sjabloon voor de verbindingsspecificatie hebt verkregen, kunt u nu een nieuwe verbindingsspecificatie ontwerpen door de juiste waarden in te vullen die overeenkomen met de bron.

Een verbindingsspecificatie kan in twee afzonderlijke delen worden verdeeld: de bronspecificaties en de verkennende specificaties.

Zie de volgende documenten voor meer informatie over de secties van een verbindingsspecificatie:

* [Uw bronspecificatie configureren](../config/sourcespec.md)
* [Uw verkenningsspecificatie configureren](../config/explorespec.md)

Als de opgegeven gegevens zijn bijgewerkt, kunt u de nieuwe verbindingsspecificatie verzenden door een verzoek van de POST in te dienen bij de `/connectionSpecs` van het [!DNL Flow Service] API.

**API-indeling**

```http
POST /connectionSpecs
```

**Verzoek**

De volgende aanvraag is een voorbeeld van een volledig geschreven verbindingsspecificatie voor een streamingbron:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbindingsspecificatie geretourneerd, inclusief de unieke `id`.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## Volgende stappen

Nu u een nieuwe verbindingsspecificatie hebt gecreeerd, moet u zijn overeenkomstige identiteitskaart van de verbindingsspecificatie aan een bestaande stroomspecificatie toevoegen. Zie de zelfstudie aan [bijwerken, stroomspecificaties](./update-flow-specs.md) voor meer informatie .

Als u wijzigingen wilt aanbrengen in de verbindingsspecificatie die u hebt gemaakt, raadpleegt u de zelfstudie over [bijwerken, verbindingsspecificaties](./update-connection-specs.md).
