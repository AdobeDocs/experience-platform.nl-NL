---
title: Edge Segmentation Guide
description: Leer hoe u Edge-segmentatie gebruikt om het publiek in Experience Platform direct aan de rand te evalueren, zodat dezelfde pagina en de volgende pagina voor het aanpassen van de paginascheiding kunnen worden gebruikt.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 1b69fa4ecadb1f6b8575358ca4a81549221430e1
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Edge-segmentatiegids

De segmentatie van Edge is de capaciteit om segmentdefinities in Adobe Experience Platform onmiddellijk [&#x200B; op de rand &#x200B;](../../landing/edge-and-hub-comparison.md) te evalueren, toelatend de zelfde pagina en volgende het gebruikscase van de paginaletterdheid.

>[!IMPORTANT]
>
> De Edge-gegevens worden opgeslagen op een locatie op de Edge-server die het dichtst bij de locatie ligt waar deze zijn verzameld. Deze gegevens kunnen ook worden opgeslagen op een andere locatie dan die welke is aangewezen als het Adobe Experience Platform-datacenter in de hub (of principal).
>
> Bovendien, zal de motor van de randsegmentatie slechts verzoeken op de rand waar er **één** primaire duidelijke identiteit is, die met niet op rand-gebaseerde primaire identiteiten verenigbaar is.

## Type Edge-segmentquery {#query-types}

Een vraag kan met randsegmentatie worden geëvalueerd als het aan om het even welke criteria voldoet die in de volgende lijst worden geschetst.

>[!NOTE]
>
>Als de vraag om het even welke vraagtypes in de volgende lijst aanpast, zal het automatisch worden geëvalueerd gebruikend randsegmentatie. Het systeem bepaalt deze mogelijkheid automatisch gebaseerd op de vraaguitdrukking.
>
>Bovendien, als het publiek **slechts** profielattributen bevat, zal het dagelijks worden geëvalueerd. Als u uw publiek in real time wilt worden geëvalueerd, zult u gebeurtenisgegevens aan uw publiek moeten toevoegen.

| Type query | Details | Query | Voorbeeld |
| ---------- | ------- | ----- | ------- |
| Eén gebeurtenis binnen een tijdsvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een tijdvenster van minder dan 24 uur. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![&#x200B; een voorbeeld van één enkele gebeurtenis binnen een relatief tijdvenster wordt getoond.](../images/methods/edge/single-event.png){zoomable="yes"} |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. | `homeAddress.country.equals("US", false)` | ![&#x200B; een voorbeeld van een getoonde profielattributen.](../images/methods/edge/profile-attribute.png){zoomable="yes"} |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![&#x200B; een voorbeeld van één enkele gebeurtenis met een profielattribuut binnen een relatief tijdvenster wordt getoond.](../images/methods/edge/single-event-with-profile-attribute.png){zoomable="yes"} |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of randsegmenten bevat. **Nota:** als een segment van segmenten wordt gebruikt, zal de profielontzetting **elke 24 uren** gebeuren. | `inSegment("a730ed3f-119c-415b-a4ac-27c396ae2dff") and inSegment("8fbbe169-2da6-4c9d-a332-b6a6ecf559b9")` | ![&#x200B; een voorbeeld van een segment van segmenten wordt getoond.](../images/methods/edge/segment-of-segments.png){zoomable="yes"} |

Bovendien, moet de segmentdefinitie **&#x200B;**&#x200B;aan een fusiebeleid worden gebonden dat op rand actief is. Voor meer informatie over samenvoegingsbeleid, te lezen gelieve de [&#x200B; gids van het samenvoegingsbeleid &#x200B;](../../profile/api/merge-policies.md).

Een segmentdefinitie zal **niet** voor randsegmentatie in het volgende scenario in aanmerking komen:

- De segmentdefinitie bevat een combinatie van één gebeurtenis en een `inSegment` -gebeurtenis.
   - Nochtans, als de segmentdefinitie in de `inSegment` gebeurtenis profiel slechts is, zal de segmentdefinitie **&#x200B;**&#x200B;voor randsegmentatie worden toegelaten.
- In de segmentdefinitie wordt &quot;Jaar negeren&quot; gebruikt als onderdeel van de tijdbeperkingen.

## publiek maken {#create-audience}

U kunt een publiek tot stand brengen dat gebruikend randsegmentatie gebruikend of de Dienst API van de Segmentatie of door het Portaal van het Publiek in UI wordt geëvalueerd.

Een segmentdefinitie kan rand-toegelaten zijn als het één van de [&#x200B; in aanmerking komende vraagtypes &#x200B;](#eligible-query-types) aanpast.

>[!BEGINTABS]

>[!TAB  de Dienst API van de Segmentatie ]

**API formaat**

```http
POST /segment/definitions
```

**Verzoek**

+++ Een voorbeeldverzoek om een segmentdefinitie te maken die is ingeschakeld voor randsegmentatie

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
                "enabled": false
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": true
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
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
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

![&#x200B; Create publieksknoop wordt benadrukt in het Portaal van het Publiek.](../images/methods/edge/select-create-audience.png){zoomable="yes"}

Er verschijnt een pop-up. Selecteer **[!UICONTROL Build rules]** om Segment Builder in te voeren.

![&#x200B; de knoop van de Regels van de Bouwstijl wordt benadrukt in creeer publiek popover.](../images/methods/edge/select-build-rules.png){zoomable="yes"}

Binnen de Bouwer van het Segment, creeer een segmentdefinitie die één van de [&#x200B; in aanmerking komende vraagtypes &#x200B;](#eligible-query-types) aanpast. Als de segmentdefinitie in aanmerking komt voor randsegmentatie, kunt u **[!UICONTROL Edge]** selecteren als **[!UICONTROL Evaluation method]** .

![&#x200B; de segmentdefinitie wordt getoond. Het evaluatietype wordt benadrukt, die de segmentdefinitie tonen kan worden geëvalueerd gebruikend randsegmentatie.](../images/methods/edge/edge-evaluation-method.png){zoomable="yes"}

Om meer over het creëren van segmentdefinities te leren, te lezen gelieve de [&#x200B; gids van de Bouwer van het Segment &#x200B;](../ui/segment-builder.md)

>[!ENDTABS]

## Soorten publiek ophalen dat is geëvalueerd met behulp van randsegmentatie {#retrieve-audiences}

U kunt al publiek terugwinnen dat gebruikend randsegmentatie gebruikend of de Dienst API van de Segmentatie of door het Portaal van het Publiek in UI wordt geëvalueerd.

>[!BEGINTABS]

>[!TAB  de Dienst API van de Segmentatie ]

Haal een lijst op van alle segmentdefinities die worden geëvalueerd met behulp van randsegmentatie binnen uw organisatie door een GET-aanvraag in te dienen bij het `/segment/definitions` -eindpunt.

**API formaat**

U moet de vraagparameter `evaluationInfo.synchronous.enabled=true` in de verzoekweg omvatten om segmentdefinities terug te winnen die gebruikend randsegmentatie worden geëvalueerd.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Verzoek**

+++ Een voorbeeldverzoek om van alle voor de rand ingeschakelde segmentdefinities een lijst te maken

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een serie van segmentdefinities in uw organisatie terug die voor randsegmentatie worden toegelaten.

+++ Een steekproefreactie die een lijst van alle rand-segmentation-Toegelaten segmentdefinities in uw organisatie bevat

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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

U kunt al publiek terugwinnen dat voor randsegmentatie binnen uw organisatie door filters in het Portaal van de Publiek wordt toegelaten te gebruiken. Selecteer het ![&#x200B; pictogram van de filterfilter &#x200B;](../../images/icons/filter.png) pictogram om de lijst van filters te tonen.

![&#x200B; het filterpictogram wordt benadrukt in het Portaal van het Publiek.](../images/methods/filter-audiences.png){zoomable="yes"}

Binnen de beschikbare filters, ga naar **frequentie van de Update** en selecteer &quot;Edge&quot;. Met dit filter geeft u alle soorten publiek in uw organisatie weer die zijn geëvalueerd met behulp van randsegmentatie.

![&#x200B; de updatefrequentie van Edge wordt geselecteerd, tonend alle publiek in de organisatie die gebruikend randsegmentatie worden geëvalueerd.](../images/methods/edge/filter-edge.png){zoomable="yes"}

Meer over het bekijken van publiek in Experience Platform leren, gelieve de [&#x200B; gids van het Portaal van het Publiek &#x200B;](../ui/audience-portal.md) te lezen.

>[!ENDTABS]

## Details publiek {#audience-details}

U kunt details van een specifiek publiek bekijken die gebruikend randsegmentatie door het binnen het Portaal van het Publiek te selecteren worden geëvalueerd.

Na het selecteren van een publiek op de Portaal van de Publiek, verschijnt de pagina van publieksdetails. Dit toont informatie over het publiek, met inbegrip van een samenvatting van de publieksdetails, de hoeveelheid gekwalificeerde profielen in tijd, evenals de bestemmingen het publiek aan geactiveerd is.

![&#x200B; de pagina van publieksdetails wordt getoond voor een publiek geëvalueerd gebruikend randsegmentatie.](../images/methods/edge/audience-details.png)

Voor gebruikers met randfunctionaliteit wordt de **[!UICONTROL Profiles over time]** -kaart weergegeven. In deze kaart ziet u het totaal aantal gekwalificeerde personen en de nieuwe populaties die zijn bijgewerkt.

**[!UICONTROL Total qualified]** metrisch vertegenwoordigt het totale aantal gekwalificeerde publiek, dat op randevaluaties voor dit publiek wordt gebaseerd.

**[!UICONTROL New audience updated]** metrisch wordt vertegenwoordigd door een lijngrafiek die de verandering in publieksgrootte door randsegmentatie toont. U kunt het vervolgkeuzemenu aanpassen en de laatste 24 uur, vorige week of 30 dagen weergeven.

![&#x200B; De Profielen over tijdkaart wordt benadrukt.](../images/methods/edge/profiles-over-time.png){zoomable="yes"}

Voor meer details op publieksdetails, te lezen gelieve het [&#x200B; Poortoverzicht van het Poort van het Publiek &#x200B;](../ui/audience-portal.md#audience-details).

## Volgende stappen

In deze handleiding wordt uitgelegd welke randsegmentatie wordt toegepast en hoe u een segmentdefinitie maakt die kan worden geëvalueerd met behulp van randsegmentatie op Adobe Experience Platform.

Om meer over het gebruiken van het gebruikersinterface van Experience Platform te leren, te lezen gelieve de [&#x200B; gebruikersgids van de Segmentatie &#x200B;](./overview.md).

Voor vaak gestelde vragen over randsegmentatie, te lezen gelieve de [&#x200B; sectie van de randsegmentatie van FAQ &#x200B;](../faq.md#edge-segmentation).

