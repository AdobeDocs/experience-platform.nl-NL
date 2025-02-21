---
solution: Experience Platform
title: Handleiding voor streaming segmentatie
description: Leer over het stromen segmentatie met inbegrip van wat het is, hoe te om een publiek tot stand te brengen dat gebruikend het stromen segmentatie wordt geëvalueerd, en hoe te om uw publiek te bekijken die gebruikend het stromen segmentatie wordt gecreeerd.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 3f0cfd6c36344f481751bf05236df4fb288eab60
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Hulplijn voor stroomsegmentatie

Streaming segmentering is de mogelijkheid om het publiek in Adobe Experience Platform in bijna realtime te evalueren en tegelijk de nadruk te leggen op gegevensrijkdom.

Met het stromen segmentatie, gebeurt de publiekskwalificatie nu aangezien het stromen gegevens in Platform landen, die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen. Hierdoor kunt u gegevens evalueren terwijl deze worden doorgegeven aan Platform, zodat het lidmaatschap van het publiek automatisch wordt bijgewerkt.

## In aanmerking komende querytypen {#query-types}

Een query komt in aanmerking voor streamingsegmentatie als deze voldoet aan een van de criteria die in de volgende tabel worden beschreven.

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor details bij het toelaten van geplande segmentatie, gelieve te verwijzen naar [ het Poortoverzicht van het Poort van het Publiek ](../ui/audience-portal.md#scheduled-segmentation).

| Type query | Details | Query | Voorbeeld |
| ---------- | ------- | ----- | ------- |
| Eén gebeurtenis binnen een tijdsvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een tijdvenster van minder dan 24 uur. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![ een voorbeeld van één enkele gebeurtenis binnen een relatief tijdvenster wordt getoond.](../images/methods/streaming/single-event.png) |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. | `homeAddress.country.equals("US", false)` | ![ een voorbeeld van een getoonde profielattributen.](../images/methods/streaming/profile-attribute.png) |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![ een voorbeeld van één enkele gebeurtenis met een profielattribuut binnen een relatief tijdvenster wordt getoond.](../images/methods/streaming/single-event-with-profile-attribute.png) |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. **Nota:** als een segment van segmenten wordt gebruikt, zal de profielontzetting **elke 24 uren** gebeuren. | `inSegment("a730ed3f-119c-415b-a4ac-27c396ae2dff") and inSegment("8fbbe169-2da6-4c9d-a332-b6a6ecf559b9")` | ![ een voorbeeld van een segment van segmenten wordt getoond.](../images/methods/streaming/segment-of-segments.png) |
| Meerdere gebeurtenissen met een profielkenmerk | Om het even welke segmentdefinitie die naar veelvoudige gebeurtenissen **binnen de laatste 24 uren** verwijst en (naar keuze) heeft één of meerdere profielattributen. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("directMarketing.emailClicked", false)) WHEN(today), C1: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![ een voorbeeld van veelvoudige gebeurtenissen met een profielattribuut wordt getoond.](../images/methods/streaming/multiple-events-with-profile-attribute.png) |

Een segmentdefinitie zal **niet** voor het stromen segmentatie in de volgende scenario&#39;s in aanmerking komen:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).
- De segmentdefinitie bevat een combinatie van één gebeurtenis en een `inSegment` -gebeurtenis.
   - Nochtans, als de segmentdefinitie in de `inSegment` gebeurtenis profiel slechts is, zal de segmentdefinitie **** voor het stromen segmentatie worden toegelaten.
- In de segmentdefinitie wordt &quot;Jaar negeren&quot; gebruikt als onderdeel van de tijdbeperkingen.

Houd rekening met de volgende richtlijnen die van toepassing zijn op streamingsegmenteringsvragen:

| Type query | Richtsnoer |
| ---------- | -------- |
| Single-event-query | Er gelden geen limieten voor het terugzoekvenster. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het raadplegingsvenster is beperkt tot **één dag**.</li><li>Een strikte tijd-opdracht gevend voorwaarde **moet** tussen de gebeurtenissen bestaan.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. Nochtans, kan de volledige gebeurtenis **niet** een negatie zijn.</li></ul> |

Als een segmentdefinitie wordt gewijzigd zodat deze niet meer voldoet aan de criteria voor het streamen van segmentatie, schakelt de segmentdefinitie automatisch over van &quot;Streaming&quot; naar &quot;Batch&quot;.

Bovendien, segmentonkwalificatie, zo gelijkaardig aan segmentkwalificatie, gebeurt in real time. Als een publiek niet langer in aanmerking komt voor een segment, is het dus onmiddellijk niet gekwalificeerd. Bijvoorbeeld, als de segmentdefinitie &quot;Alle gebruikers vraagt die rode schoenen in de laatste drie uren&quot;kochten, na drie uren, zullen alle profielen die aanvankelijk voor de segmentdefinitie kwalificeerden ongekwalificeerd zijn.

## publiek maken {#create-audience}

U kunt een publiek tot stand brengen dat gebruikend het stromen segmentatie gebruikend of de Dienst API van de Segmentatie of door het Portaal van de Publiek in UI wordt geëvalueerd.

Een segmentdefinitie kan stromen-toegelaten zijn als het één van de [ in aanmerking komende vraagtypes ](#eligible-query-types) aanpast.

>[!BEGINTABS]

>[!TAB  de Dienst API van de Segmentatie ]

**API formaat**

```http
POST /segment/definitions
```

**Verzoek**

+++ Een voorbeeldverzoek om een segmentdefinitie te maken die is ingeschakeld voor het streamen van segmentatie

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
                "enabled": true
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
            "enabled": false
        },
        "continuous": {
            "enabled": true
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

Meer informatie over het gebruiken van dit eindpunt kan in de [ gids van het het eindpunt van de segmentdefinitie ](../api/segment-definitions.md) worden gevonden.

>[!TAB Audience Portal]

Selecteer **[!UICONTROL Create audience]** in Audience Portal.

![ Create publieksknoop wordt benadrukt in het Portaal van het Publiek.](../images/methods/streaming/select-create-audience.png)

Er verschijnt een pop-up. Selecteer **[!UICONTROL Build rules]** om Segment Builder in te voeren.

![ de knoop van de Regels van de Bouwstijl wordt benadrukt in creeer publiek popover.](../images/methods/streaming/select-build-rules.png)

Binnen de Bouwer van het Segment, creeer een segmentdefinitie die één van de [ in aanmerking komende vraagtypes ](#eligible-query-types) aanpast. Als de segmentdefinitie voor het stromen segmentatie kwalificeert, zult u **[!UICONTROL Streaming]** als **[!UICONTROL Evaluation method]** kunnen selecteren.

![ de segmentdefinitie wordt getoond. Het evaluatietype wordt benadrukt, die de segmentdefinitie tonen kan worden geëvalueerd gebruikend het stromen segmentatie.](../images/methods/streaming/streaming-evaluation-method.png)

Om meer over het creëren van segmentdefinities te leren, te lezen gelieve de [ gids van de Bouwer van het Segment ](../ui/segment-builder.md)

>[!ENDTABS]

## Soorten publiek ophalen {#retrieve-audiences}

U kunt al publiek terugwinnen dat gebruikend het stromen segmentatie gebruikend of de Dienst API van de Segmentatie of door het Portaal van het Publiek in UI wordt geëvalueerd.

>[!BEGINTABS]

>[!TAB  de Dienst API van de Segmentatie ]

Haal een lijst op van alle segmentdefinities die worden geëvalueerd met behulp van streamingsegmentatie binnen uw organisatie door een GET-aanvraag in te dienen bij het `/segment/definitions` -eindpunt.

**API formaat**

U moet de vraagparameter `evaluationInfo.synchronous.enabled=true` in de verzoekweg omvatten om segmentdefinities terug te winnen die gebruikend het stromen segmentatie worden geëvalueerd.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Verzoek**

+++ Een voorbeeldverzoek om alle streaming-toegelaten segmentdefinities op te nemen

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Reactie**

Een succesvolle reactie keert status 200 van HTTP met een serie van segmentdefinities in uw organisatie terug die voor het stromen segmentatie worden toegelaten.

+++A steekproefreactie die een lijst van alle het stromen-segmenteren-Toegelaten segmentdefinities in uw organisatie bevat

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
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
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

De meer gedetailleerde informatie over de gesegmenteerde teruggekeerde definitie kan in de [ gids van het de segmentdefinitiedetectietype ](../api/segment-definitions.md) worden gevonden.

+++

>[!TAB Audience Portal]

U kunt al publiek terugwinnen dat voor het stromen segmentatie binnen uw organisatie door filters in het Portaal van de Publiek wordt toegelaten te gebruiken. Selecteer het ![ pictogram van de filterfilter ](../../images/icons/filter.png) pictogram om de lijst van filters te tonen.

![ het filterpictogram wordt benadrukt in het Portaal van het Publiek.](../images/methods/filter-audiences.png)

Ga binnen de beschikbare filters naar **[!UICONTROL Update frequency]** en selecteer &quot;[!UICONTROL Streaming]&quot;. Met dit filter geeft u alle soorten publiek in uw organisatie weer die zijn geëvalueerd met behulp van streaming segmentatie.

![ de het stromen updatefrequentie wordt geselecteerd, tonend alle publiek in de organisatie die gebruikend het stromen segmentatie worden geëvalueerd.](../images/methods/streaming/filter-streaming.png)

Meer over het bekijken van publiek in Platform leren, gelieve de [ gids van het Portaal van het Publiek ](../ui/audience-portal.md) te lezen.

>[!ENDTABS]

## Details publiek {#audience-details}

U kunt details van een specifiek publiek bekijken die gebruikend het stromen segmentatie door het binnen de Portaal van het Publiek te selecteren wordt geëvalueerd.

Na het selecteren van een publiek op de Portaal van de Publiek, verschijnt de pagina van publieksdetails. Dit toont informatie over het publiek, met inbegrip van een samenvatting van de publieksdetails, de hoeveelheid gekwalificeerde profielen in tijd, evenals de bestemmingen het publiek aan geactiveerd is.

![ de pagina van publieksdetails wordt getoond voor een publiek dat gebruikend het stromen segmentatie wordt geëvalueerd.](../images/methods/streaming/audience-details.png)

Voor streaming-toegelaten publiek, wordt de **[!UICONTROL Profiles over time]** kaart getoond, die het totaal kwalificeerde en nieuwe publiek bijgewerkte metriek toont.

**[!UICONTROL Total qualified]** metrisch vertegenwoordigt het totale aantal gekwalificeerde publiek, dat op partij en het stromen evaluaties voor dit publiek wordt gebaseerd.

**[!UICONTROL New audience updated]** metrisch wordt vertegenwoordigd door een lijngrafiek die de verandering in publieksgrootte door het stromen segmentatie toont. U kunt het vervolgkeuzemenu aanpassen en de laatste 24 uur, vorige week of 30 dagen weergeven.

![ De Profielen over tijdkaart wordt benadrukt.](../images/methods/streaming/profiles-over-time.png)

Voor meer details op publieksdetails, te lezen gelieve het [ Poortoverzicht van het Poort van het Publiek ](../ui/audience-portal.md#audience-details).

## Volgende stappen

Deze gids verklaart hoe het stromen-toegelaten segmentdefinities op Adobe Experience Platform werken en hoe te om het stromen-toegelaten segmentdefinities te controleren.

Om meer over het gebruiken van het gebruikersinterface van Adobe Experience Platform te leren, te lezen gelieve de [ gebruikersgids van de Segmentatie ](./overview.md).

Voor vaak gestelde vragen over het stromen segmentatie, te lezen gelieve de [ het stromen segmenteringssectie van FAQ ](../faq.md#streaming-segmentation).
