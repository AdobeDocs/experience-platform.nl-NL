---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Meerdere berichten streamen in één HTTP-aanvraag
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Meerdere berichten verzenden in één HTTP-aanvraag

Bij het streamen van gegevens naar het Adobe Experience Platform kan het maken van veel HTTP-oproepen duur zijn. Bijvoorbeeld, in plaats van het creëren van 200 HTTP- verzoeken met 1KB nuttige lading, is het veel efficiënter om 1 HTTP- verzoek met 200 berichten van 1KB elk, met één enkele lading van 200KB tot stand te brengen. Wanneer correct gebruikt, is het groeperen van veelvoudige berichten binnen één enkel verzoek een uitstekende manier om gegevens te optimaliseren die naar het Platform van de Ervaring worden verzonden.

Dit document biedt een zelfstudie voor het verzenden van meerdere berichten naar Experience Platform binnen één HTTP-aanvraag via streaming opname.

## Aan de slag

Voor deze zelfstudie is een goed begrip van de gegevensinscriptie van het Adobe Experience Platform vereist. Lees de volgende documentatie voordat u met deze zelfstudie begint:

- [Overzicht](../home.md)van gegevensinname: Omvat de kernconcepten de Ingestie van de Gegevens van het Platform van de Ervaring, met inbegrip van innamemethodes en gegevensschakelaars.
- [Overzicht](../streaming-ingestion/overview.md)van streaming opname: De workflow en bouwstenen voor het streamen van opname, zoals streamingverbindingen, datasets, XDM Individual Profile en XDM ExperienceEvent.

Deze zelfstudie vereist ook dat u de zelfstudie [Verificatie van het Adobe Experience Platform](../../tutorials/authentication.md) hebt voltooid om oproepen naar platform-API&#39;s te kunnen uitvoeren. Voltooiing van de authentificatiezelfstudie verstrekt de waarde voor de kopbal van de Vergunning die door alle API vraag in dit leerprogramma wordt vereist. De kopbal wordt getoond in steekproefvraag als volgt:

- Autorisatie: Drager `{ACCESS_TOKEN}`

Voor alle POST-aanvragen is een extra header nodig:

- Inhoudstype: application/json

## Een streamingverbinding maken

U moet eerst een streamingverbinding maken voordat u gegevens kunt streamen naar Experience Platform. Lees de handleiding voor het [maken van een streamingverbinding](./create-streaming-connection.md) voor meer informatie over het maken van een streamingverbinding.

Na het registreren van een het stromen verbinding, zult u, als gegevensproducent, een unieke URL hebben die kan worden gebruikt om gegevens aan Platform te stromen.

## Streamen naar een gegevensset

Het volgende voorbeeld toont hoe te om veelvoudige berichten naar een specifieke dataset binnen één enkel HTTP- verzoek te verzenden. Neem identiteitskaart van de dataset in de berichtkopbal op om dat bericht direct in het te hebben worden opgenomen.

U kunt de id voor een bestaande gegevensset ophalen met behulp van de interface van het platform of met behulp van een lijstbewerking in de API. De dataset ID kan op het Platform [van de](https://platform.adobe.com) Ervaring worden gevonden door naar het lusje van **Datasets** te gaan, op de dataset te klikken u identiteitskaart voor, en het kopiëren van het koord van het gebied van identiteitskaart **van de** Dataset op het **Info** lusje wilt. Zie het overzicht [van de Dienst van de](../../catalog/home.md) Catalogus voor informatie over hoe te om datasets terug te winnen gebruikend API.

In plaats van een bestaande dataset te gebruiken, kunt u een nieuwe dataset tot stand brengen. Lees gelieve te [creëren een dataset gebruikend APIs](../../catalog/api/create-dataset.md) zelfstudie voor meer informatie over het creëren van een dataset gebruikend APIs.

**API-indeling**

```http
POST /collection/{CONNECTION_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de gemaakte streamingverbinding. |

**Verzoek**

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Antwoord**

Een geslaagde reactie retourneert de HTTP-status 207 (Multi-status). Als u de responsstructuur controleert, krijgt u meer informatie over het al dan niet slagen van elke methode die in de aanvraag wordt uitgevoerd. Er wordt een reactie geretourneerd voor elk element van de array met aanvraagberichten. Hieronder ziet u een voorbeeld van een geslaagde reactie zonder berichtfouten:

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

Zie de tabel met [responscodes](#response-codes) in het aanhangsel van deze zelfstudie voor meer informatie over statuscodes.

## Ontbroken berichten identificeren

Vergeleken met het verzenden van een verzoek met één enkel bericht, wanneer het verzenden van een HTTP- verzoek met veelvoudige berichten, zijn er extra te overwegen factoren, zoals: hoe te om te identificeren wanneer het gegeven heeft verzuimd om te verzenden, welke specifieke berichten niet konden verzenden en hoe zij kunnen worden teruggewonnen, en wat aan gegevens gebeurt die slagen wanneer andere berichten in het zelfde verzoek ontbreken.

Voordat u verdergaat met deze zelfstudie, is het raadzaam eerst de handleiding voor het [ophalen van mislukte batches](../quality/retrieve-failed-batches.md) te raadplegen.

### Aanvraaglading verzenden met geldige en ongeldige berichten

In het volgende voorbeeld wordt getoond wat er gebeurt wanneer de batch geldige en ongeldige berichten bevat.

De request-payload is een array van JSON-objecten die de gebeurtenis in het XDM-schema vertegenwoordigen. Voor een geslaagde validatie van het bericht moet aan de volgende voorwaarden worden voldaan:
- Het `imsOrgId` veld in de berichtkop moet overeenkomen met de inlaatdefinitie. Als de verzoeklading geen `imsOrgId` gebied omvat, zal de Dienst van de Kern van de Inzameling van Gegevens (DCCS) automatisch het gebied toevoegen.
- De kopbal van het bericht zou een bestaand schema moeten van XDM van verwijzingen voorzien dat in Platform UI wordt gecreeerd.
- Het `datasetId` gebied moet een bestaande dataset in Platform van verwijzingen voorzien, en zijn schema moet het schema aanpassen dat in het `header` voorwerp binnen elk bericht wordt verstrekt inbegrepen in het verzoeklichaam.

**API-indeling**

```http
POST /collection/{CONNECTION_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de gemaakte gegevensinlaat. |

**Verzoek**

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Antwoord**

De antwoordlading omvat een status voor elk bericht samen met een GUID in `xactionId` die voor het vinden kan worden gebruikt.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

In het bovenstaande voorbeeldantwoord worden foutberichten voor de vorige aanvraag weergegeven. Door dit antwoord op de vorige geldige reactie te vergelijken, kunt u opmerken dat het verzoek in een gedeeltelijk succes resulteerde, met één bericht dat met succes wordt opgenomen en drie berichten die in mislukking resulteerden. Beide reacties retourneren een statuscode &#39;207&#39;. Zie de tabel met [responscodes](#response-codes) in het aanhangsel van deze zelfstudie voor meer informatie over statuscodes.

Het eerste bericht is naar Platform verzonden en wordt niet beïnvloed door de resultaten van de andere berichten. Als u de mislukte berichten opnieuw wilt verzenden, hoeft u dit bericht dus niet opnieuw op te nemen.

Het tweede bericht is mislukt omdat het geen berichttekst bevatte. Het inzamelingsverzoek verwacht berichtelementen om geldige kopbal en lichaamssecties te hebben. Als u de volgende code na de koptekst in het tweede bericht toevoegt, wordt de aanvraag gecorrigeerd en kan het tweede bericht de validatie doorgeven:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Het derde bericht is mislukt omdat een ongeldige IMS-organisatie-id in de koptekst wordt gebruikt. De IMS-organisatie moet overeenkomen met de {CONNECTION_ID} die u wilt posten. Als u wilt bepalen welke IMS-organisatie-id overeenkomt met de streamingverbinding die u gebruikt, kunt u een `GET inlet` aanvraag uitvoeren met de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)gegevensverwerking. Zie [het ophalen van een streamingverbinding](./create-streaming-connection.md#get-data-collection-url) voor een voorbeeld van hoe eerder gemaakte streamingverbindingen kunnen worden opgehaald.

Het vierde bericht is mislukt omdat het niet het verwachte XDM-schema heeft gevolgd. De `xdmSchema` include-bestanden in de kop- en hoofdtekst van de aanvraag komen niet overeen met het XDM-schema van de aanvraag `{DATASET_ID}`. Het verbeteren van het schema in de berichtkopbal en het lichaam staat het toe om bevestiging DCCS over te gaan en met succes naar Platform worden verzonden. De berichttekst moet ook worden bijgewerkt zodat deze overeenkomt met het XDM-schema van het formulier, zodat de streamingvalidatie op Platform wordt doorgegeven. `{DATASET_ID}` Voor meer informatie over wat aan berichten gebeurt die met succes aan Platform stromen, zie de [bevestig berichten die sectie van dit leerprogramma worden opgenomen](#confirm-messages-ingested) .

### Ontbroken berichten van Platform ophalen

Mislukte berichten worden geïdentificeerd door een code van de foutenstatus in de reactiesserie.
De ongeldige berichten worden verzameld en opgeslagen in een &quot;fout&quot;partij binnen de dataset die door wordt gespecificeerd `{DATASET_ID}`.

Lees de handleiding [Ophalen mislukte batches](../quality/retrieve-failed-batches.md) voor meer informatie over het herstellen van mislukte batchberichten.

## Ontvangen berichten bevestigen

Berichten die DCCS bevestiging overgaan worden gestroomd aan Platform. Op Platform, worden de partijberichten getest door bevestiging te stromen alvorens in het gegevensmeer wordt opgenomen. De status van batches, of deze nu succesvol zijn of niet, wordt weergegeven in de gegevensset die is opgegeven door `{DATASET_ID}`.

U kunt het statuut van partijberichten bekijken die met succes aan Platform gebruikend het Platform van de [Ervaring UI](https://platform.adobe.com) door naar het lusje van **Datasets** te gaan stromen, op de dataset te klikken u aan stroomt, en het lusje van de Activiteit **van de** Dataset te controleren.

De berichten van de partij die het stromen bevestiging op Platform overgaan worden opgenomen in het gegevensmeer. De berichten zijn dan beschikbaar voor analyse of uitvoer.

## Volgende stappen

Nu u weet hoe te om veelvoudige berichten in één enkel verzoek te verzenden en te verifiëren wanneer de berichten met succes in de doeldataset worden opgenomen, kunt u beginnen het stromen van uw eigen gegevens aan Platform. Voor een overzicht van hoe te om ingebedde gegevens van Platform te vragen en terug te winnen, zie de gids van de Toegang van [Gegevens](../../data-access/tutorials/dataset-data.md) .

## Aanhangsel

Deze sectie bevat aanvullende informatie voor de zelfstudie.

### Antwoordcodes

In de volgende tabel worden statuscodes weergegeven die zijn geretourneerd door geslaagde en mislukte responsberichten.

| Statuscode | Beschrijving |
| :---: | --- |
| 207 | Hoewel &#39;207&#39; wordt gebruikt als de algemene antwoordstatuscode, moet de ontvanger de inhoud van het multistatus responsorgaan raadplegen voor meer informatie over het al dan niet slagen van de methodeuitvoering. De antwoordcode wordt gebruikt in succes, gedeeltelijk succes, en ook in mislukkingssituaties. |
| 400 | Er is een probleem met het verzoek. Zie de antwoordtekst voor een specifieker foutbericht (Bericht dat vereiste velden voor de payload ontbreken of Bericht dat de indeling xdm onbekend is). |
| 401 | Niet bevoegd: verzoek bevat geen geldige machtigingheader. Dit is slechts teruggekeerd voor inlaten die toegelaten authentificatie hebben. |
| 403 | Niet bevoegd:  Opgegeven machtigingstoken is ongeldig of verlopen. Dit is slechts teruggekeerd voor inlaten die toegelaten authentificatie hebben. |
| 413 | De lading te groot - geworpen wanneer het totale ladingsverzoek groter is dan 1MB. |
| 429 | Te veel aanvragen binnen de opgegeven tijdsduur. |
| 500 | Fout in verwerking van lading. Zie de antwoordtekst voor een specifieker foutbericht (Bericht payload schema niet opgegeven of komt niet overeen met de XDM-definitie in Platform). |
| 503 | De service is momenteel niet beschikbaar. Clients dienen ten minste drie keer een exponentiële back-offstrategie te gebruiken. |