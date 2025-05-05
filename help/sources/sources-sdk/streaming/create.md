---
title: Een nieuwe verbindingsspecificatie maken voor Streaming SDK met de Flow Service API
description: Het volgende document verstrekt stappen op hoe te om een verbindingsspecificatie tot stand te brengen gebruikend de Dienst API van de Stroom en een nieuwe bron door Zelfbediening Bronnen te integreren.
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Een nieuwe verbindingsspecificatie maken met de API van [!DNL Flow Service]

>[!NOTE]
>
>Self-Serve Sources Streaming SDK bevindt zich in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Een verbindingsspecificatie vertegenwoordigt de structuur van een bron. Het bevat informatie over de authentificatievereisten van een bron, bepaalt hoe de brongegevens kunnen worden onderzocht en worden geïnspecteerd, en verstrekt informatie over de attributen van een bepaalde bron. Met het eindpunt `/connectionSpecs` in de [!DNL Flow Service] API kunt u de verbindingsspecificaties binnen uw organisatie programmatisch beheren.

In het volgende document worden de stappen beschreven voor het maken van een verbindingsspecificatie met de API [!DNL Flow Service] en het integreren van een nieuwe bron via Self-Serve Sources (Streaming SDK).

## Aan de slag

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Artefacten verzamelen

Als u een nieuwe streamingbron wilt maken met behulp van Self-Serve Sources, moet u eerst coördineren met de Adobe, een persoonlijke Git-opslagplaats aanvragen en op de details met betrekking tot het label, de beschrijving, de categorie en het pictogram voor de bron uitlijnen met de Adobe.

Zodra u de Git-opslagruimte hebt opgegeven, moet u deze als volgt structureren:

* Bronnen
   * {your_source}
      * Artefacten
         * {your_source}-category.txt
         * {your_source} -description.txt
         * {your_source} -icon.svg
         * {your_source} -label.txt
         * {your_source} -connectionSpec.json

| Artefacten (bestandsnamen) | Beschrijving | Voorbeeld |
| --- | --- | --- |
| {your_source} | De naam van de bron. Deze map moet alle artefacten bevatten die betrekking hebben op uw bron, in uw persoonlijke Git-opslagplaats. | `medallia` |
| {your_source}-category.txt | De categorie waartoe uw bron behoort, opgemaakt als een tekstbestand. **Nota**: Als u gelooft dat uw bron niet in om het even welke bovengenoemde categorieën past, gelieve uw vertegenwoordiger van de Adobe te contacteren om te bespreken. | `medallia-category.txt` Geef in het bestand bijvoorbeeld de categorie van de bron op. `streaming` |
| {your_source} -description.txt | Een korte beschrijving van de bron. | [!DNL Medallia] is een marketingautomatiseringsbron die u kunt gebruiken om [!DNL Medallia] -gegevens naar het Experience Platform te brengen. |
| {your_source} -icon.svg | De afbeelding die moet worden gebruikt om uw bron weer te geven in de catalogus met bronnen in het Experience Platform. Dit pictogram moet een SVG-bestand zijn. |
| {your_source} -label.txt | De naam van de bron zoals deze moet worden weergegeven in de catalogus met bronnen van het Experience Platform. | Medallia |
| {your_source} -connectionSpec.json | Een JSON-bestand dat de verbindingsspecificatie van uw bron bevat. Dit bestand is in eerste instantie niet vereist omdat u de verbindingsspecificatie invult als u deze handleiding invult. | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>Tijdens de testperiode van de verbindingsspecificatie kunt u in plaats van de sleutelwaarden `text` gebruiken in de verbindingsspecificatie.

Nadat u de benodigde bestanden hebt toegevoegd aan uw persoonlijke Git-opslagplaats, moet u een pull-aanvraag (PR) maken die door de Adobe kan worden gecontroleerd. Wanneer uw PR wordt goedgekeurd en samengevoegd, zult u van identiteitskaart worden voorzien die voor uw verbindingsspecificatie kan worden gebruikt om naar het etiket, de beschrijving, en het pictogram van uw bron te verwijzen.

Voer vervolgens de onderstaande stappen uit om uw verbindingsspecificatie te configureren. Voor extra begeleiding op de verschillende functionaliteiten die u aan uw bron, zoals geavanceerde het plannen, douaneschema, of verschillende paginatietypen kunt toevoegen, te herzien gelieve de gids op [ vormend bronspecificaties ](../config/sourcespec.md).

## Sjabloon voor verbindingsspecificatie kopiëren

Nadat u de vereiste artefacten hebt verzameld, kopieert en plakt u de onderstaande sjabloon voor de verbindingsspecificatie naar de teksteditor van uw keuze en werkt u de kenmerken tussen haakjes `{}` bij met informatie die relevant is voor uw specifieke bron.

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
    "documentationLink": "https://docs.adobe.com/content/help/nl-NL/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
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

Zodra u het malplaatje van de verbindingsspecificatie hebt verworven, kunt u beginnen een nieuwe verbindingsspecificatie te ontwerpen door de aangewezen waarden in te vullen die aan uw bron beantwoorden.

Een verbindingsspecificatie kan in twee verschillende delen worden verdeeld: de bronspecificaties en de verkennende specificaties.

Zie de volgende documenten voor meer informatie over de secties van een verbindingsspecificatie:

* [Uw bronspecificatie configureren](../config/sourcespec.md)
* [Uw verkenningsspecificatie configureren](../config/explorespec.md)

Wanneer de opgegeven gegevens zijn bijgewerkt, kunt u de nieuwe verbindingsspecificatie verzenden door een aanvraag voor een POST in te dienen bij het `/connectionSpecs` -eindpunt van de [!DNL Flow Service] API.

**API formaat**

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
          "documentationLink": "https://docs.adobe.com/content/help/nl-NL/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

**Reactie**

Een geslaagde reactie retourneert de zojuist gemaakte verbindingsspecificatie, inclusief de unieke `id` .

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
          "authRequired": false,
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
        "documentationLink": "https://docs.adobe.com/content/help/nl-NL/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

Nu u een nieuwe verbindingsspecificatie hebt gecreeerd, moet u zijn overeenkomstige identiteitskaart van de verbindingsspecificatie aan een bestaande stroomspecificatie toevoegen. Zie het leerprogramma bij [ het bijwerken stroomspecificaties ](./update-flow-specs.md) voor meer informatie.

Om wijzigingen in de verbindingsspecificatie te maken die u creeerde, zie het leerprogramma bij [ het bijwerken van verbindingsspecificaties ](./update-connection-specs.md).
