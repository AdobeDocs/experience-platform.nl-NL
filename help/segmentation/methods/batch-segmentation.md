---
title: Handleiding voor batchsegmentatie
description: Leer over partijsegmentatie met inbegrip van wat het is, hoe te om een publiek tot stand te brengen dat gebruikend partijsegmentatie wordt geëvalueerd, en hoe te om uw publiek te bekijken dat gebruikend partijsegmentatie wordt gecreeerd.
exl-id: b6fba2fb-8eec-4429-92fd-ece5c79d379d
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Hulplijn voor batchsegmentatie

De segmentatie van de partij is een methode van de segmentatiebeoordeling die u profielgegevens allen in één keer laat bewegen om het overeenkomstige publiek tot stand te brengen.

Met partijsegmentatie, kunt u gedetailleerde en rijke soorten publiek tot stand brengen, en segmentatietaken in werking stellen om te bepalen wanneer u deze gegevens aan stroomafwaartse diensten wilt verspreiden.

## In aanmerking komende querytypen {#query-types}

Alle vragen zijn verkiesbaar voor partijsegmentatie.

## publiek maken {#create-audience}

U kunt een publiek tot stand brengen dat gebruikend partijsegmentatie gebruikend of de Dienst API van de Segmentatie of door het Portaal van de Publiek in UI wordt geëvalueerd.

>[!BEGINTABS]

>[!TAB  de Dienst API van de Segmentatie ]

**API formaat**

```http
POST /segment/definitions
```

**Verzoek**

+++ Een steekproefverzoek om een segmentdefinitie tot stand te brengen die voor partijsegmentatie wordt toegelaten

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met details van uw pas gecreëerde segmentdefinitie terug.

+++Een voorbeeldreactie bij het maken van een segmentdefinitie.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

Meer informatie over het gebruiken van dit eindpunt kan in de [&#x200B; gids van het het eindpunt van de segmentdefinitie &#x200B;](../api/segment-definitions.md) worden gevonden.

>[!TAB Audience Portal]

Selecteer **[!UICONTROL Create audience]** in Audience Portal.

![&#x200B; Create publieksknoop wordt benadrukt in het Portaal van het Publiek.](../images/methods/batch/select-create-audience.png)

Er verschijnt een pop-up. Selecteer **[!UICONTROL Build rules]** om Segment Builder in te voeren.

![&#x200B; de knoop van de Regels van de Bouwstijl wordt benadrukt in creeer publiek popover.](../images/methods/batch/select-build-rules.png)

Nadat u de segmentdefinitie hebt gemaakt, selecteert u **[!UICONTROL Batch]** als **[!UICONTROL Evaluation method]** .

![&#x200B; de segmentdefinitie wordt getoond. Het evaluatietype wordt benadrukt, die de segmentdefinitie tonen kan worden geëvalueerd gebruikend het stromen segmentatie.](../images/methods/batch/batch-evaluation-method.png)

Om meer over het creëren van segmentdefinities te leren, te lezen gelieve de [&#x200B; gids van de Bouwer van het Segment &#x200B;](../ui/segment-builder.md)

>[!ENDTABS]

## Soorten publiek ophalen {#retrieve-audiences}

U kunt alle soorten publiek terugwinnen die gebruikend partijsegmentatie gebruikend of de Dienst API van de Segmentatie of door het Portaal van het Publiek in UI worden geëvalueerd.

>[!BEGINTABS]

>[!TAB  de Dienst API van de Segmentatie ]

Haal een lijst op van alle segmentdefinities die met batchsegmentatie binnen uw organisatie worden geëvalueerd door een GET-aanvraag in te dienen bij het `/segment/definitions` -eindpunt.

**API formaat**

U moet de vraagparameter `evaluationInfo.batch.enabled=true` in de verzoekweg omvatten om segmentdefinities terug te winnen die gebruikend partijsegmentatie worden geëvalueerd.

```http
GET /segment/definitions?evaluationInfo.batch.enabled=true
```

**Verzoek**

+++ Een steekproefverzoek om van alle partij-toegelaten segmentdefinities een lijst te maken

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.batch.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een serie van segmentdefinities in uw organisatie terug die gebruikend partijsegmentatie worden geëvalueerd.

+++A steekproefreactie die een lijst van alle partij-segmentation-geëvalueerde segmentdefinities in uw organisatie bevat

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

De meer gedetailleerde informatie over de gesegmenteerde teruggekeerde definitie kan in de [&#x200B; gids van het de segmentdefinitiedetectietype &#x200B;](../api/segment-definitions.md) worden gevonden.

+++

>[!TAB Audience Portal]

U kunt al publiek terugwinnen dat voor partijsegmentatie binnen uw organisatie door filters in het Portaal van de Publiek wordt toegelaten te gebruiken. Selecteer het ![&#x200B; pictogram van de filterfilter &#x200B;](../../images/icons/filter.png) pictogram om de lijst van filters te tonen.

![&#x200B; het filterpictogram wordt benadrukt in het Portaal van het Publiek.](../images/methods/filter-audiences.png)

Ga binnen de beschikbare filters naar **[!UICONTROL Update frequency]** en selecteer &quot;[!UICONTROL Batch]&quot;. Als u dit filter gebruikt, worden alle soorten publiek in uw organisatie weergegeven die met batchsegmentatie zijn geëvalueerd.

![&#x200B; de updatefrequentie van de Partij wordt geselecteerd, tonend alle publiek in de organisatie die gebruikend partijsegmentatie worden geëvalueerd.](../images/methods/batch/filter-batch.png)

Meer over het bekijken van publiek in Experience Platform leren, gelieve de [&#x200B; gids van het Portaal van het Publiek &#x200B;](../ui/audience-portal.md) te lezen.

>[!ENDTABS]

## Volgende stappen

Deze gids verklaart hoe te om een segmentdefinitie tot stand te brengen die kan worden geëvalueerd gebruikend partijsegmentatie op Adobe Experience Platform.

Om meer over het gebruiken van het gebruikersinterface van Experience Platform te leren, te lezen gelieve de [&#x200B; gebruikersgids van de Segmentatie &#x200B;](../ui/overview.md).

Voor vaak gestelde vragen over partijsegmentatie, te lezen gelieve de [&#x200B; sectie van de partijsegmentatie van FAQ &#x200B;](../faq.md#batch-segmentation).
