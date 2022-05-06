---
keywords: Experience Platform;thuis;populaire onderwerpen;het stromen ingestie;ingestie;het stromen veelvoudige berichten;veelvoudige berichten;
solution: Experience Platform
title: Meerdere berichten verzenden in één HTTP-aanvraag
topic-legacy: tutorial
type: Tutorial
description: Dit document bevat een zelfstudie voor het verzenden van meerdere berichten naar Adobe Experience Platform binnen één HTTP-aanvraag via streaming invoer.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 1%

---

# Meerdere berichten verzenden in één HTTP-aanvraag

Wanneer het stromen van gegevens aan Adobe Experience Platform, kan het maken van talrijke vraag van HTTP duur zijn. Bijvoorbeeld, in plaats van het creëren van 200 HTTP- verzoeken met 1KB nuttige lading, is het veel efficiënter om 1 HTTP- verzoek met 200 berichten van 1KB elk, met één enkele lading van 200KB tot stand te brengen. Wanneer correct gebruikt, is het groeperen van veelvoudige berichten binnen één enkel verzoek een uitstekende manier om gegevens te optimaliseren die worden verzonden naar [!DNL Experience Platform].

Dit document bevat een zelfstudie voor het verzenden van meerdere berichten naar [!DNL Experience Platform] in één HTTP-aanvraag met streaming opname.

## Aan de slag

Deze zelfstudie vereist een goed begrip van Adobe Experience Platform [!DNL Data Ingestion]. Lees de volgende documentatie voordat u met deze zelfstudie begint:

- [Overzicht van gegevensinname](../home.md): Omvat de kernconcepten van [!DNL Experience Platform Data Ingestion], inclusief innamemethoden en gegevensconnectors.
- [Overzicht van het opnemen van streaming](../streaming-ingestion/overview.md): De werkstroom en bouwstenen van het stromen opname, zoals het stromen verbindingen, datasets, [!DNL XDM Individual Profile], en [!DNL XDM ExperienceEvent].

Voor deze zelfstudie hebt u ook het volgende nodig: [Verificatie naar Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) zelfstudie om oproepen succesvol te kunnen doen aan [!DNL Platform] API&#39;s. Voltooiing van de authentificatiezelfstudie verstrekt de waarde voor de kopbal van de Vergunning die door alle API vraag in dit leerprogramma wordt vereist. De kopbal wordt getoond in steekproefvraag als volgt:

- Autorisatie: Drager `{ACCESS_TOKEN}`

Voor alle aanvragen voor POSTEN is een extra header vereist:

- Inhoudstype: application/json

## Een streamingverbinding maken

U moet eerst een streamingverbinding maken voordat u kunt beginnen met het streamen van gegevens naar [!DNL Experience Platform]. Lees de [een streamingverbinding maken](./create-streaming-connection.md) voor informatie over het maken van een streamingverbinding.

Na het registreren van een het stromen verbinding, zult u, als gegevensproducent, een unieke URL hebben die kan worden gebruikt om gegevens aan Platform te stromen.

## Streamen naar een gegevensset

Het volgende voorbeeld toont hoe te om veelvoudige berichten naar een specifieke dataset binnen één enkel HTTP- verzoek te verzenden. Neem identiteitskaart van de dataset in de berichtkopbal op om dat bericht direct in het te hebben worden opgenomen.

U kunt identiteitskaart voor een bestaande dataset krijgen gebruikend [!DNL Platform] UI of het gebruiken van een lijstverrichting in API. De gegevensset-id is te vinden op [Experience Platform](https://platform.adobe.com) door naar de **[!UICONTROL Datasets]** tabblad, klikken op de gegevensset waarvoor u de id wilt en de tekenreeks kopiëren vanuit het veld voor de gegevensset-id op het tabblad **[!UICONTROL Info]** tab. Zie de [Overzicht van Catalog Service](../../catalog/home.md) voor informatie over hoe te om datasets terug te winnen gebruikend API.

In plaats van een bestaande dataset te gebruiken, kunt u een nieuwe dataset tot stand brengen. Lees de [een dataset maken met behulp van API&#39;s](../../catalog/api/create-dataset.md) zelfstudie voor meer informatie over het maken van een dataset met behulp van API&#39;s.

**API-indeling**

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
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

Voor meer informatie over statuscodes raadpleegt u de [responscodes](#response-codes) tabel in het aanhangsel van deze zelfstudie.

## Ontbroken berichten identificeren

Vergeleken met het verzenden van een verzoek met één enkel bericht, wanneer het verzenden van een HTTP- verzoek met veelvoudige berichten, zijn er extra te overwegen factoren, zoals: hoe te om te identificeren wanneer het gegeven heeft verzuimd om te verzenden, welke specifieke berichten niet konden verzenden en hoe zij kunnen worden teruggewonnen, en wat aan gegevens gebeurt die slagen wanneer andere berichten in het zelfde verzoek ontbreken.

Voordat u verdergaat met deze zelfstudie, is het raadzaam eerst de [ophalen van mislukte batches](../quality/retrieve-failed-batches.md) hulplijn.

### Aanvraaglading verzenden met geldige en ongeldige berichten

In het volgende voorbeeld wordt getoond wat er gebeurt wanneer de batch geldige en ongeldige berichten bevat.

De request-payload is een array van JSON-objecten die de gebeurtenis in het XDM-schema vertegenwoordigen. Voor een geslaagde validatie van het bericht moet aan de volgende voorwaarden worden voldaan:
- De `imsOrgId` veld in de berichtkop moet overeenkomen met de inlaatdefinitie. Als de aanvraaglading geen `imsOrgId` in het veld [!DNL Data Collection Core Service] (DCCS) voegt het veld automatisch toe.
- De koptekst van het bericht moet verwijzen naar een bestaand XDM-schema dat is gemaakt in het dialoogvenster [!DNL Platform] UI.
- De `datasetId` veld moet verwijzen naar een bestaande gegevensset in [!DNL Platform]en moet het schema ervan overeenkomen met het schema dat in het dialoogvenster `header` object binnen elk bericht dat in de aanvraaginstantie is opgenomen.

**API-indeling**

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
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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
        "imsOrgId": "{ORG_ID}",
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

**Antwoord**

De antwoordlading omvat een status voor elk bericht samen met een GUID in `xactionId` die kunnen worden gebruikt voor overtrekken.

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

In het bovenstaande voorbeeldantwoord worden foutberichten voor de vorige aanvraag weergegeven. Door dit antwoord op de vorige geldige reactie te vergelijken, kunt u opmerken dat het verzoek in een gedeeltelijk succes resulteerde, met één bericht dat met succes wordt opgenomen en drie berichten die in mislukking resulteerden. Beide reacties retourneren een statuscode &#39;207&#39;. Voor meer informatie over statuscodes raadpleegt u de [responscodes](#response-codes) tabel in het aanhangsel van deze zelfstudie.

Het eerste bericht is verzonden naar [!DNL Platform] en niet wordt beïnvloed door de resultaten van de andere berichten. Als u de mislukte berichten opnieuw wilt verzenden, hoeft u dit bericht dus niet opnieuw op te nemen.

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

Het derde bericht is mislukt omdat een ongeldige IMS-organisatie-id in de koptekst wordt gebruikt. De IMS-organisatie moet overeenkomen met de {CONNECTION_ID} die u wilt posten. Als u wilt bepalen welke IMS-organisatie-id overeenkomt met de streamingverbinding die u gebruikt, kunt u een `GET inlet` verzoek met [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). Zie [streamingverbinding ophalen](./create-streaming-connection.md#get-data-collection-url) voor een voorbeeld van hoe u eerder gemaakte streamingverbindingen kunt ophalen.

Het vierde bericht is mislukt omdat het niet het verwachte XDM-schema heeft gevolgd. De `xdmSchema` in de koptekst en hoofdtekst van het verzoek komt niet overeen met het XDM-schema van het `{DATASET_ID}`. Het verbeteren van het schema in de berichtkopbal en het lichaam staat het toe om bevestiging DCCS over te gaan en met succes verzonden naar [!DNL Platform]. Het berichtlichaam moet ook worden bijgewerkt om het XDM schema van te passen `{DATASET_ID}` voor het doorgeven van streamingvalidatie [!DNL Platform]. Voor meer informatie over wat met berichten gebeurt die met succes aan Platform stromen, zie [bevestiging van ontvangen berichten](#confirm-messages-ingested) in deze zelfstudie.

### Ontbroken berichten ophalen van [!DNL Platform]

Mislukte berichten worden geïdentificeerd door een code van de foutenstatus in de reactiesserie.
De ongeldige berichten worden verzameld en opgeslagen in een &quot;fout&quot;partij binnen de dataset die door wordt gespecificeerd `{DATASET_ID}`.

Lees de [ophalen van mislukte batches](../quality/retrieve-failed-batches.md) handleiding voor meer informatie over het herstellen van mislukte batchberichten.

## Ontvangen berichten bevestigen

Berichten die DCCS- bevestiging overgaan worden gestroomd aan [!DNL Platform]. Aan [!DNL Platform], worden de batchberichten getest door streamingvalidatie voordat ze in de batch worden opgenomen [!DNL Data Lake]. De status van batches, of deze nu succesvol zijn of niet, wordt weergegeven in de gegevensset die is opgegeven door `{DATASET_ID}`.

U kunt de status weergeven van batchberichten waarnaar succesvol wordt gestreamd [!DNL Platform] met de [UI Experience Platform](https://platform.adobe.com) door naar de **[!UICONTROL Datasets]** tabblad, klikken op de gegevensset waarnaar u streamt en controleren de **[!UICONTROL Dataset Activity]** tab.

Berichten in batch die streamingvalidatie doorgeven [!DNL Platform] worden opgenomen in de [!DNL Data Lake]. De berichten zijn dan beschikbaar voor analyse of uitvoer.

## Volgende stappen

Nu u weet hoe te om veelvoudige berichten in één enkel verzoek te verzenden en te verifiëren wanneer de berichten met succes in de doeldataset worden opgenomen, kunt u beginnen het stromen van uw eigen gegevens aan [!DNL Platform]. Voor een overzicht van hoe te om ingebedde gegevens van te vragen en terug te winnen [!DNL Platform], zie de [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) hulplijn.

## Aanhangsel

Deze sectie bevat aanvullende informatie voor de zelfstudie.

### Antwoordcodes

In de volgende tabel worden statuscodes weergegeven die zijn geretourneerd door geslaagde en mislukte responsberichten.

| Statuscode | Beschrijving |
| :---: | --- |
| 207 | Hoewel &#39;207&#39; wordt gebruikt als de algemene responsstatuscode, moet de ontvanger de inhoud van het multi-status responsorgaan raadplegen voor meer informatie over het al dan niet slagen van de methodeuitvoering. De antwoordcode wordt gebruikt in succes, gedeeltelijk succes, en ook in mislukkingssituaties. |
| 400 | Er is een probleem met het verzoek. Zie de antwoordtekst voor een specifieker foutbericht (Bericht dat vereiste velden voor de payload ontbreken of Bericht dat de indeling xdm onbekend is). |
| 401 | Niet bevoegd: verzoek bevat geen geldige machtigingheader. Dit is slechts teruggekeerd voor inlaten die toegelaten authentificatie hebben. |
| 403 | Niet bevoegd: Opgegeven machtigingstoken is ongeldig of verlopen. Dit is slechts teruggekeerd voor inlaten die toegelaten authentificatie hebben. |
| 413 | De lading te groot - geworpen wanneer het totale ladingsverzoek groter is dan 1MB. |
| 429 | Te veel aanvragen binnen de opgegeven tijdsduur. |
| 500 | Fout in verwerking van lading. Zie het antwoordlichaam voor een specifieker foutenmelding (bijvoorbeeld, specificeerde het nuttige ladingsschema van het Bericht niet of paste niet de definitie XDM in aan [!DNL Platform]). |
| 503 | De service is momenteel niet beschikbaar. Clients dienen ten minste drie keer een exponentiële back-offstrategie te gebruiken. |
