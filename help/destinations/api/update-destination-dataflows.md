---
keywords: Experience Platform;huis;populaire onderwerpen;de stroomdienst;update bestemmingsdataflows
solution: Experience Platform
title: Doelgegevens bijwerken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Deze zelfstudie behandelt de stappen voor het bijwerken van een doelgegevensstroom. Leer hoe u de gegevensstroom in- of uitschakelt, de basisinformatie bijwerkt of segmenten en kenmerken toevoegt en verwijdert met behulp van de Flow Service API.
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2136'
ht-degree: 0%

---

# Doelgegevens bijwerken met de Flow Service API

Deze zelfstudie behandelt de stappen voor het bijwerken van een doelgegevensstroom. Leer hoe te om de gegevensstroom toe te laten of onbruikbaar te maken, zijn basisinformatie bij te werken of segmenten en attributen toe te voegen en te verwijderen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Voor informatie over het bewerken van doelgegevensstromen met behulp van de interface van het Experience Platform, leest u [Activeringsstromen bewerken](/help/destinations/ui/edit-activation.md).

## Aan de slag {#get-started}

Voor deze zelfstudie hebt u een geldige stroom-id nodig. Als u geen geldige stroom-id hebt, selecteert u het gewenste doel in het menu [doelcatalogus](../catalog/overview.md) en voert u de volgende stappen uit: [verbinden met de bestemming](../ui/connect-destination.md) en [gegevens activeren](../ui/activation-overview.md) voordat u deze zelfstudie probeert.

>[!NOTE]
>
> De voorwaarden *stroom* en *dataflow* worden onderling verwisselbaar gebruikt in deze zelfstudie. In de context van deze zelfstudie hebben ze dezelfde betekenis.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Doelen](../home.md): [!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.
* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om uw gegevensstroom met succes bij te werken met de [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Als u aanroepen wilt uitvoeren naar Platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle middelen in Experience Platform, met inbegrip van die welke toebehoren aan [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Als de `x-sandbox-name` header is niet opgegeven, aanvragen worden opgelost onder de `prod` sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Gegevens over gegevensstroom opzoeken {#look-up-dataflow-details}

De eerste stap in het bijwerken van uw bestemmingsgegevensstroom is dataflow details terug te winnen gebruikend uw stroom ID. U kunt de huidige details van een bestaande gegevensstroom bekijken door een verzoek van de GET aan `/flows` eindpunt.

**API-indeling**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de doelgegevensstroom die u wilt ophalen. |

**Verzoek**

Het volgende verzoek wint informatie betreffende uw stroom ID terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de huidige details van uw gegevensstroom inclusief de versie, unieke id (`id`) en andere relevante informatie.

```json
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## Naam en beschrijving van gegevensstroom bijwerken {#update-dataflow}

Als u de naam en beschrijving van uw gegevensstroom wilt bijwerken, moet u een PATCH-aanvraag uitvoeren bij de [!DNL Flow Service] API terwijl het verstrekken van uw stroom ID, versie, en de nieuwe waarden u wilt gebruiken.

>[!IMPORTANT]
>
>De `If-Match` header is required when making a PATCH request. De waarde voor deze kopbal is de unieke versie van dataflow u wilt bijwerken. De labelwaarde wordt bijgewerkt bij elke geslaagde update van een gegevensstroom.

**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

De volgende aanvraag werkt de naam en beschrijving van uw gegevensstroom bij.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Dataflow in- of uitschakelen {#enable-disable-dataflow}

Wanneer toegelaten, voert een dataflow profielen naar de bestemming uit. Gegevensstromen zijn standaard ingeschakeld, maar kunnen worden uitgeschakeld om het exporteren van het profiel te pauzeren.

U kunt een bestaande bestemmingsgegevensstroom toelaten of onbruikbaar maken door een verzoek van de POST aan [!DNL Flow Service] API en de desbetreffende status waarnaar u de flow wilt bijwerken.

**API-indeling**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**Verzoek**

Met de volgende aanvraag wordt de status van uw gegevensstroom bijgewerkt naar ingeschakeld.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Met de volgende aanvraag wordt de status van uw gegevensstroom bijgewerkt naar uitgeschakeld.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Een segment toevoegen aan een gegevensstroom {#add-segment}

Om een segment aan de bestemmingsdataflow toe te voegen, voer een verzoek van PATCH aan de [!DNL Flow Service] API terwijl het verstrekken van uw stroom ID, versie, en het segment u wilt toevoegen.

**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

Met het volgende verzoek wordt een nieuw segment toegevoegd aan een bestaande doelgegevensstroom.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "endData":"2022-03-10"
               "startTime":"16:00",
            }
         }
      }
   }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. Als u een segment wilt toevoegen aan een gegevensstroom, gebruikt u de opdracht `add` bewerking. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. Wanneer u een segment toevoegt aan een gegevensstroom, gebruikt u het pad dat in het voorbeeld is opgegeven. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |
| `id` | Geef de id op van het segment dat u toevoegt aan de doelgegevensstroom. |
| `name` | **(Optioneel)**. Geef de naam op van het segment dat u toevoegt aan de doelgegevensstroom. Merk op dat dit gebied niet verplicht is en u kunt met succes een segment aan de bestemmingsdataflow toevoegen zonder zijn naam te verstrekken. |
| `filenameTemplate` | Voor *batchbestemmingen* alleen. Dit veld is alleen vereist wanneer u een segment toevoegt aan een gegevensstroom in exportdoelen voor batchbestanden zoals Amazon S3, SFTP of Azure Blob. <br> Dit veld bepaalt de bestandsnaamindeling van de bestanden die naar uw doel worden geëxporteerd. <br> De volgende opties zijn beschikbaar: <br> <ul><li>`%DESTINATION_NAME%`: Verplicht. De geëxporteerde bestanden bevatten de doelnaam.</li><li>`%SEGMENT_ID%`: Verplicht. De geëxporteerde bestanden bevatten de id van het geëxporteerde segment.</li><li>`%SEGMENT_NAME%`: **(Optioneel)**. De geëxporteerde bestanden bevatten de naam van het geëxporteerde segment.</li><li>`DATETIME(YYYYMMdd_HHmmss)` of `%TIMESTAMP%`: **(Optioneel)**. Selecteer één van deze twee opties voor uw dossiers om de tijd te omvatten wanneer zij door Experience Platform worden geproduceerd.</li><li>`custom-text`: **(Optioneel)**. Vervang deze tijdelijke aanduiding door aangepaste tekst die u aan het einde van de bestandsnamen wilt toevoegen.</li></ul> <br> Raadpleeg voor meer informatie over het configureren van bestandsnamen de [bestandsnamen configureren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) in de activeringszelfstudie voor batchbestemmingen. |
| `exportMode` | Voor *batchbestemmingen* alleen. Dit veld is alleen vereist wanneer u een segment toevoegt aan een gegevensstroom in exportdoelen voor batchbestanden zoals Amazon S3, SFTP of Azure Blob. <br> Verplicht. Selecteren `"DAILY_FULL_EXPORT"` of `"FIRST_FULL_THEN_INCREMENTAL"`. Voor meer informatie over de twee opties raadpleegt u [volledige bestanden exporteren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) en [incrementele bestanden exporteren](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) in de activeringszelfstudie voor batchbestemmingen. |
| `startDate` | Selecteer de datum waarop het segment moet beginnen met het exporteren van profielen naar uw bestemming. |
| `frequency` | Voor *batchbestemmingen* alleen. Dit veld is alleen vereist wanneer u een segment toevoegt aan een gegevensstroom in exportdoelen voor batchbestanden zoals Amazon S3, SFTP of Azure Blob. <br> Verplicht. <br> <ul><li>Voor de `"DAILY_FULL_EXPORT"` u kunt de exportmodus `ONCE` of `DAILY`.</li><li>Voor de `"FIRST_FULL_THEN_INCREMENTAL"` u kunt de exportmodus `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `endDate` | Voor *batchbestemmingen* alleen. Dit veld is alleen vereist wanneer u een segment toevoegt aan een gegevensstroom in exportdoelen voor batchbestanden zoals Amazon S3, SFTP of Azure Blob. <br> Niet van toepassing bij selectie `"exportMode":"DAILY_FULL_EXPORT"` en `"frequency":"ONCE"`. <br> Hiermee stelt u de datum in waarop segmentleden stoppen met exporteren naar de bestemming. |
| `startTime` | Voor *batchbestemmingen* alleen. Dit veld is alleen vereist wanneer u een segment toevoegt aan een gegevensstroom in exportdoelen voor batchbestanden zoals Amazon S3, SFTP of Azure Blob. <br> Verplicht. Selecteer het tijdstip waarop bestanden met leden van het segment moeten worden gegenereerd en naar uw bestemming moeten worden geëxporteerd. |

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Een segment verwijderen uit een gegevensstroom {#remove-segment}

Om een segment uit een bestaande bestemmingsdataflow te verwijderen, voer een verzoek van PATCH aan [!DNL Flow Service] API terwijl het verstrekken van uw stroom ID, versie, en de indexselecteur van het segment u wilt verwijderen. Indexering begint bij `0`. Bijvoorbeeld, verwijdert het steekproefverzoek verder hieronder de eerste en tweede segmenten uit dataflow.

**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

Het volgende verzoek verwijdert twee segmenten uit een bestaande bestemmingsdataflow.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. Als u een segment uit een gegevensstroom wilt verwijderen, gebruikt u de opdracht `remove` bewerking. |
| `path` | Geeft aan welk bestaand segment moet worden verwijderd uit de doelgegevensstroom op basis van de index van de segmentkiezer. Om de orde van segmenten in een dataflow terug te winnen, voer een vraag van de GET aan `/flows` en inspecteer de `transformations.segmentSelectors` eigenschap. Om het eerste segment in dataflow te schrappen, gebruik `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## De componenten van een segment van de update in een dataflow {#update-segment}

U kunt componenten van een segment in een bestaande bestemmingsgegevensstroom bijwerken. U kunt bijvoorbeeld de exportfrequentie wijzigen of de sjabloon voor de bestandsnaam bewerken. Om dit te doen, doe een verzoek van de PATCH aan [!DNL Flow Service] API terwijl het verstrekken van uw stroom ID, versie, en de indexselecteur van het segment u wilt bijwerken. Indexering begint bij `0`. Bijvoorbeeld, werkt het verzoek hieronder het negende segment in een dataflow bij.

**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

Wanneer het bijwerken van een segment in een bestaande bestemmingsdataflow, zou u eerst een GET verrichting moeten uitvoeren om de details van het segment terug te winnen u wilt bijwerken. Geef vervolgens alle segmentgegevens op in de payload, niet alleen de velden die u wilt bijwerken. In het onderstaande voorbeeld wordt aangepaste tekst toegevoegd aan het einde van de bestandsnaamsjabloon en wordt de frequentie van het exportschema bijgewerkt van 6 uur tot 12 uur.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

Raadpleeg de sectie voor beschrijvingen van de eigenschappen in de payload [Een segment toevoegen aan een gegevensstroom](#add-segment).


**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Een profielkenmerk toevoegen aan een gegevensstroom {#add-profile-attribute}

Als u een profielkenmerk aan de doelgegevensstroom wilt toevoegen, voert u een PATCH-verzoek uit aan de [!DNL Flow Service] API terwijl het verstrekken van uw stroom ID, versie, en het profielattribuut u wilt toevoegen.

**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

Met de volgende aanvraag wordt een nieuw profielkenmerk toegevoegd aan een bestaande doelgegevensstroom.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. Als u een profielkenmerk aan een gegevensstroom wilt toevoegen, gebruikt u de opdracht `add` bewerking. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. Wanneer u een profielkenmerk aan een gegevensstroom toevoegt, gebruikt u het pad dat in het voorbeeld is opgegeven. |
| `value.path` | De waarde van het profielkenmerk dat u toevoegt aan de gegevensstroom. |

**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Een profielkenmerk verwijderen uit een gegevensstroom {#remove-profile-attribute}

Als u een profielkenmerk wilt verwijderen uit een bestaande doelgegevensstroom, voert u een PATCH-verzoek uit naar de [!DNL Flow Service] API terwijl het verstrekken van uw stroom ID, versie, en de indexselecteur van het profielattribuut u wilt verwijderen. Indexering begint bij `0`. Met de voorbeeldaanvraag hieronder verwijdert u bijvoorbeeld het vijfde profielkenmerk van de gegevensstroom.


**API-indeling**

```http
PATCH /flows/{FLOW_ID}
```

**Verzoek**

Met de volgende aanvraag wordt een profielkenmerk verwijderd uit een bestaande doelgegevensstroom.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. Als u een segment uit een gegevensstroom wilt verwijderen, gebruikt u de opdracht `remove` bewerking. |
| `path` | Geeft aan welk bestaand profielkenmerk uit de doelgegevensstroom moet worden verwijderd, op basis van de index van de segmentkiezer. Om de orde van profielattributen in een dataflow terug te winnen, voer een vraag van de GET aan `/flows` en inspecteer de `transformations.profileSelectors` eigenschap. Om het eerste segment in dataflow te schrappen, gebruik `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**Antwoord**

Een geslaagde reactie retourneert uw flow-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl u uw stroom-id opgeeft.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het API-foutbericht voor Experience Platforms. Zie [API-statuscodes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) en [aanvragen, koptekstfouten](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Door deze zelfstudie te volgen hebt u geleerd hoe u verschillende componenten van een doelgegevensstroom kunt bijwerken, zoals het toevoegen of verwijderen van segmenten of profielkenmerken met gebruik van [!DNL Flow Service] API. Voor meer informatie over bestemmingen, zie [Overzicht van doelen](../home.md).
