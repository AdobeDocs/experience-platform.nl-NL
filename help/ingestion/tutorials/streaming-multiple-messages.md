---
keywords: Experience Platform;home;populaire onderwerpen;streaming ingestie;ingestie;streaming veelvoudige berichten;veelvoudige berichten;
solution: Experience Platform
title: Meerdere berichten verzenden in één HTTP-aanvraag
type: Tutorial
description: Dit document bevat een zelfstudie voor het verzenden van meerdere berichten naar Adobe Experience Platform binnen één HTTP-aanvraag via streaming invoer.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 31c00e69dd92f7c3232e09f02da36c60cd8cf486
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 1%

---

# Meerdere berichten verzenden in één HTTP-aanvraag

Wanneer het stromen van gegevens aan Adobe Experience Platform, kan het maken van talrijke vraag van HTTP duur zijn. Bijvoorbeeld, in plaats van het creëren van 200 HTTP- verzoeken met 1KB nuttige lading, is het veel efficiënter om 1 HTTP- verzoek met 200 berichten van 1KB elk, met één enkele lading van 200KB tot stand te brengen. Als u de gegevens correct gebruikt, is het groeperen van meerdere berichten binnen één aanvraag een uitstekende manier om gegevens die naar [!DNL Experience Platform] worden verzonden, te optimaliseren.

Dit document bevat een zelfstudie voor het verzenden van meerdere berichten naar [!DNL Experience Platform] binnen één HTTP-aanvraag via streaming opname.

## Aan de slag

Deze zelfstudie vereist een goed begrip van Adobe Experience Platform [!DNL Data Ingestion] . Lees de volgende documentatie voordat u met deze zelfstudie begint:

- [ het Overzicht van de Ingestie van Gegevens ](../home.md): Behandelt de kernconcepten [!DNL Experience Platform Data Ingestion], met inbegrip van innamemethodes en gegevensschakelaars.
- [ Streaming ingestie overzicht ](../streaming-ingestion/overview.md): Het werkschema en de bouwstenen van het stromen opname, zoals het stromen verbindingen, datasets, [!DNL XDM Individual Profile], en [!DNL XDM ExperienceEvent].

Dit leerprogramma vereist u ook om de [ Authentificatie aan Adobe Experience Platform ](https://www.adobe.com/go/platform-api-authentication-en) leerprogramma te voltooien om vraag aan [!DNL Experience Platform] APIs met succes te maken. Voltooiing van de authentificatiezelfstudie verstrekt de waarde voor de kopbal van de Vergunning die door alle API vraag in dit leerprogramma wordt vereist. De kopbal wordt getoond in steekproefvraag als volgt:

- Autorisatie: Drager `{ACCESS_TOKEN}`

Voor alle POST-aanvragen is een extra header nodig:

- Inhoudstype: application/json

## Een streamingverbinding maken

U moet eerst een streamingverbinding maken voordat u kunt beginnen met het streamen van gegevens naar [!DNL Experience Platform] . Lees [ creeer een het stromen verbinding ](./create-streaming-connection.md) gids om te leren hoe te om een het stromen verbinding tot stand te brengen.

Nadat u een streamingverbinding hebt geregistreerd, beschikt u als producent van gegevens over een unieke URL waarmee u gegevens kunt streamen naar Experience Platform.

## Streamen naar een gegevensset

Het volgende voorbeeld toont hoe te om veelvoudige berichten naar een specifieke dataset binnen één enkel HTTP- verzoek te verzenden. Neem identiteitskaart van de dataset in de berichtkopbal op om dat bericht direct in het te hebben worden opgenomen.

U kunt de id voor een bestaande gegevensset ophalen met de gebruikersinterface van [!DNL Experience Platform] of door een bewerking voor het weergeven van lijsten in de API te gebruiken. Identiteitskaart van de dataset kan op [ Experience Platform ](https://platform.adobe.com) worden gevonden door naar het **[!UICONTROL Datasets]** lusje te gaan, op de dataset te klikken u identiteitskaart voor wilt, en het kopiëren van het koord van het gebied van datasetidentiteitskaart op het **[!UICONTROL Info]** lusje. Zie het [ overzicht van de Dienst van de Catalogus ](../../catalog/home.md) voor informatie over hoe te om datasets terug te winnen gebruikend API.

In plaats van een bestaande dataset te gebruiken, kunt u een nieuwe dataset tot stand brengen. Gelieve te lezen [ creeer een dataset gebruikend APIs ](../../catalog/api/create-dataset.md) leerprogramma voor meer informatie bij het creëren van een dataset gebruikend APIs.

**API formaat**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de gemaakte streamingverbinding. |

**Verzoek**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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

**Reactie**

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

Voor meer informatie over statuscodes, gelieve te zien de [ lijst van de responscodes ](#response-codes) in het Bijlage van dit leerprogramma.

## Ontbroken berichten identificeren

Vergeleken met het verzenden van een verzoek met één enkel bericht, wanneer het verzenden van een HTTP- verzoek met veelvoudige berichten, zijn er extra factoren te overwegen, zoals: hoe te om te identificeren wanneer het gegeven heeft verzuimd te verzenden, welke specifieke berichten er niet in slaagden en hoe zij kunnen worden teruggewonnen, en wat aan gegevens gebeurt die slagen wanneer andere berichten in het zelfde verzoek ontbreken.

Alvorens met dit leerprogramma te werk te gaan, wordt het geadviseerd om [ eerst te herzien die ontbroken partijen ](../quality/retrieve-failed-batches.md) gids terugwinnen.

### Aanvraaglading verzenden met geldige en ongeldige berichten

In het volgende voorbeeld wordt getoond wat er gebeurt wanneer de batch geldige en ongeldige berichten bevat.

De request-payload is een array van JSON-objecten die de gebeurtenis in het XDM-schema vertegenwoordigen. Voor een geslaagde validatie van het bericht moet aan de volgende voorwaarden worden voldaan:
- Het veld `imsOrgId` in de berichtkop moet overeenkomen met de inlaatdefinitie. Als de payload van de aanvraag geen veld `imsOrgId` bevat, voegt het veld automatisch toe door [!DNL Data Collection Core Service] (DCCS).
- De koptekst van het bericht moet verwijzen naar een bestaand XDM-schema dat in de [!DNL Experience Platform] UI is gemaakt.
- Het veld `datasetId` moet verwijzen naar een bestaande gegevensset in [!DNL Experience Platform] en het schema ervan moet overeenkomen met het schema dat in het object `header` is opgegeven in elk bericht dat in de hoofdtekst van de aanvraag is opgenomen.

**API formaat**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{CONNECTION_ID}` | De id van de gemaakte gegevensinlaat. |

**Verzoek**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
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
        "imsOrgId": "{ORG_ID}",
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

**Reactie**

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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

In het bovenstaande voorbeeldantwoord worden foutberichten voor de vorige aanvraag weergegeven. Door dit antwoord op de vorige geldige reactie te vergelijken, kunt u opmerken dat het verzoek in een gedeeltelijk succes resulteerde, met één bericht dat met succes wordt opgenomen en drie berichten die in mislukking resulteerden. Beide reacties retourneren een statuscode &#39;207&#39;. Voor meer informatie over statuscodes, gelieve te zien de [ lijst van de responscodes ](#response-codes) in het Bijlage van dit leerprogramma.

Het eerste bericht is verzonden naar [!DNL Experience Platform] en wordt niet beïnvloed door de resultaten van de andere berichten. Als u de mislukte berichten opnieuw wilt verzenden, hoeft u dit bericht dus niet opnieuw op te nemen.

Het tweede bericht is mislukt omdat het geen berichttekst bevatte. Het inzamelingsverzoek verwacht berichtelementen om geldige kopbal en lichaamssecties te hebben. Als u de volgende code na de koptekst in het tweede bericht toevoegt, wordt de aanvraag gecorrigeerd en kan het tweede bericht de validatie doorgeven:

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Het derde bericht is mislukt als gevolg van een ongeldige organisatie-id die in de koptekst wordt gebruikt. De organisatie moet overeenkomen met de {CONNECTION_ID} die u wilt posten. Om te bepalen welke organisatie identiteitskaart de het stromen verbinding aanpast u gebruikt, kunt u een `GET inlet` verzoek uitvoeren gebruikend [[!DNL Streaming Ingestion API] ](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). Zie [ het terugwinnen van een het stromen verbinding ](./create-streaming-connection.md#get-data-collection-url) voor een voorbeeld van hoe te om eerder gecreeerde het stromen verbindingen terug te winnen.

Het vierde bericht is mislukt omdat het niet het verwachte XDM-schema heeft gevolgd. De `xdmSchema` in de header en de hoofdtekst van de aanvraag komt niet overeen met het XDM-schema van de `{DATASET_ID}` . Als u het schema in de berichtkop en de tekst corrigeert, kan de berichtkop en de hoofdtekst DCCS-validatie doorgeven en kan deze naar [!DNL Experience Platform] worden verzonden. De hoofdtekst van het bericht moet ook worden bijgewerkt zodat deze overeenkomt met het XDM-schema van de `{DATASET_ID}` , zodat de streamingvalidatie wordt doorgegeven aan [!DNL Experience Platform] . Voor meer informatie over wat aan berichten gebeurt die met succes aan Experience Platform stromen, zie [ berichten bevestigen die ](#confirm-messages-ingested) sectie van dit leerprogramma worden opgenomen.

### Ontbroken berichten ophalen van [!DNL Experience Platform]

Mislukte berichten worden geïdentificeerd door een code van de foutenstatus in de reactiesserie.
De ongeldige berichten worden verzameld en opgeslagen in een &quot;fout&quot;partij binnen de dataset die door `{DATASET_ID}` wordt gespecificeerd.

Lees [ terugwinnend ontbroken partijen ](../quality/retrieve-failed-batches.md) gids voor meer informatie bij het terugkrijgen van ontbroken partijberichten.

## Ontvangen berichten bevestigen

Berichten die DCCS-validatie doorgeven, worden gestreamd naar [!DNL Experience Platform] . Op [!DNL Experience Platform] worden de batchberichten getest door streamingvalidatie voordat ze in de [!DNL Data Lake] worden opgenomen. De status van batches, of deze nu succesvol zijn of niet, wordt weergegeven in de gegevensset die is opgegeven door `{DATASET_ID}` .

U kunt het statuut van partijberichten bekijken die met succes aan [!DNL Experience Platform] gebruikend [ Experience Platform UI ](https://platform.adobe.com) stromen door naar het **[!UICONTROL Datasets]** lusje te gaan, op de dataset te klikken u stromen aan, en het **[!UICONTROL Dataset Activity]** lusje te controleren.

Batchberichten die via streamingvalidatie worden doorgegeven aan [!DNL Experience Platform] , worden in de [!DNL Data Lake] opgenomen. De berichten zijn dan beschikbaar voor analyse of uitvoer.

## Volgende stappen

Nu u weet hoe te om veelvoudige berichten in één enkel verzoek te verzenden en te verifiëren wanneer de berichten met succes in de doeldataset worden opgenomen, kunt u beginnen uw eigen gegevens te stromen aan [!DNL Experience Platform]. Zie de handleiding van [!DNL Experience Platform] voor een overzicht van het opvragen en ophalen van gegevens uit [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) .

## Bijlage

Deze sectie bevat aanvullende informatie voor de zelfstudie.

### Antwoordcodes

In de volgende tabel worden de statuscodes weergegeven die zijn geretourneerd door geslaagde en mislukte responsberichten.

| Statuscode | Beschrijving |
| :---: | --- |
| 207 | Hoewel &#39;207&#39; wordt gebruikt als de algemene responsstatuscode, moet de ontvanger de inhoud van het multi-status responsorgaan raadplegen voor meer informatie over het al dan niet slagen van de methodeuitvoering. De antwoordcode wordt gebruikt in succes, gedeeltelijk succes, en ook in mislukkingssituaties. |
| 400 | Er is een probleem met het verzoek. Zie de antwoordtekst voor een specifieker foutbericht (Bericht dat vereiste velden voor de payload ontbreken of Bericht dat de indeling xdm onbekend is). |
| 401 | Niet bevoegd: verzoek bevat ongeldige machtigingsheader. Dit is slechts teruggekeerd voor inlaten die toegelaten authentificatie hebben. |
| 403 | Niet geautoriseerd: mits de machtigingstoken ongeldig of verlopen is. Dit is slechts teruggekeerd voor inlaten die toegelaten authentificatie hebben. |
| 413 | De lading te groot - geworpen wanneer het totale ladingsverzoek groter is dan 1MB. |
| 429 | Te veel aanvragen binnen de opgegeven tijdsduur. |
| 500 | Fout in verwerking van lading. Zie het antwoordgedeelte voor een specifieker foutbericht (Bericht payload-schema is bijvoorbeeld niet opgegeven of komt niet overeen met de XDM-definitie in [!DNL Experience Platform] ). |
| 503 | De service is momenteel niet beschikbaar. Clients dienen ten minste drie keer een exponentiële back-offstrategie te gebruiken. |
