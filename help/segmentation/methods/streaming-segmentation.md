---
solution: Experience Platform
title: Handleiding voor streaming segmentatie
description: Leer over het stromen segmentatie met inbegrip van wat het is, hoe te om een publiek tot stand te brengen dat gebruikend het stromen segmentatie wordt geëvalueerd, en hoe te om uw publiek te bekijken die gebruikend het stromen segmentatie wordt gecreeerd.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: cd22213be0dbc2e5a076927e560f1b23b467b306
workflow-type: tm+mt
source-wordcount: '1995'
ht-degree: 0%

---

# Hulplijn voor stroomsegmentatie

>[!BEGINSHADEBOX]

>[!NOTE]
>
>De subsidiabiliteitscriteria voor streamingsegmentatie zijn bijgewerkt op 20 mei 2025.

+++Updates voor geschiktheid

>[!IMPORTANT]
>
>Alle bestaande segmentdefinities die momenteel worden geëvalueerd met behulp van streaming of randsegmentatie, blijven werken zoals ze zijn, tenzij ze worden bewerkt of bijgewerkt.

## Regelset {#ruleset}

Om het even welke **nieuwe of uitgegeven** segmentdefinities die de volgende heersers aanpassen zullen **niet meer** worden geëvalueerd gebruikend het stromen of randsegmentatie. In plaats daarvan worden ze geëvalueerd met behulp van batchsegmentatie.

- Eén gebeurtenis met een tijdvenster van meer dan 24 uur
   - Activeer een publiek met alle profielen die een webpagina in de afgelopen 3 dagen hebben bekeken.
- Eén gebeurtenis zonder tijdvenster
   - Activeer een publiek met alle profielen die een webpagina hebben weergegeven.

## Tijdvenster {#time-window}

Om een publiek met het stromen segmentatie te evalueren, moet het **** binnen een 24 uurstijdvenster worden beperkt.

## Batchgegevens opnemen in streaming publiek {#include-batch-data}

Voorafgaand aan deze update kunt u een definitie voor streaming publiek maken die zowel batch- als streaming gegevensbronnen combineert. Met de nieuwste update wordt het maken van een publiek met zowel batch- als streaming-gegevensbronnen echter geëvalueerd aan de hand van batchsegmentatie.

Als u een segmentdefinitie moet evalueren met behulp van streaming of randsegmentatie die overeenkomt met de bijgewerkte linialen, moet u expliciet een batch- en streaming liniaal maken en deze combineren met behulp van segmentsegmenten. Deze partijheersers **moeten** op een profielschema worden gebaseerd.

Bijvoorbeeld, laten wij zeggen u twee publiek hebt, met één publiek die het schemagegevens van het profiel en de andere gegevens van het de gebeurtenisschema van de huisvestingservaring huisvesten:

| Doelgroep | Schema | Source-type | Query-definitie | Id van publiek |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Inwoners uit Californië | Profiel | Batch | Het adres van het huis is in de staat van Californië | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Recente controles | Experience Event | Streaming | Heeft in de laatste 24 uur ten minste één afhandeling | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Als u de partijcomponent in uw het stromen publiek wilt gebruiken, zult u een verwijzing naar het partijpubliek moeten maken gebruikend segment van segmenten.

Een voorbeeldregel die de twee soorten publiek samenvoegt, ziet er als volgt uit:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

Het resulterende publiek *zal* worden geëvalueerd gebruikend het stromen segmentatie, aangezien het hefboomwerkingen het lidmaatschap van het partijpubliek door naar de component van het partijpubliek te verwijzen.

Nochtans, als u twee publiek met gebeurtenisgegevens wilt combineren, kunt u **niet** enkel de twee gebeurtenissen combineren. U moet beide soorten publiek maken en vervolgens een ander publiek maken dat `inSegment` gebruikt om naar beide soorten publiek te verwijzen.

Bijvoorbeeld, laten wij zeggen u twee publiek hebt, met beide publiek woonachtig gebeurtenisschemagegevens:

| Doelgroep | Schema | Source-type | Query-definitie | Id van publiek |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Recente verlaten | Gebeurtenis Experience | Batch | Heeft ten minste één gebeurtenis voor verlaten in de afgelopen 24 uur | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Recente controles | Experience Event | Streaming | Heeft in de laatste 24 uur ten minste één afhandeling | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

In deze situatie, zou u een derde publiek als volgt moeten creëren:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Alle bestaande segmentdefinities die overeenkomen met de regels, blijven geëvalueerd met streaming of randsegmentatie totdat ze worden bewerkt.
>
>Bovendien, zullen alle bestaande segmentdefinities die momenteel aan de andere het stromen of de evaluatiecriteria van de randsegmentatie voldoen geëvalueerd met het stromen of randsegmentatie blijven.

## Samenvoegbeleid {#merge-policy}

Om het even welke **nieuwe of uitgegeven** segmentdefinities die voor het stromen of randsegmentatie **kwalificeren moeten** op &quot;Actief op Edge&quot;fusiebeleid zijn.

Als er geen actieve reeks van het fusiebeleid is, zult u uw fusiebeleid ](../../profile/merge-policies/ui-guide.md#configure) moeten vormen en het plaatsen om op rand actief te zijn.[


+++

>[!ENDSHADEBOX]

Streaming segmentering is de mogelijkheid om het publiek in Adobe Experience Platform in bijna realtime te evalueren en tegelijk de nadruk te leggen op gegevensrijkdom.

Met streamingsegmentatie gebeurt de kwalificatie van het publiek nu terwijl streaming data naar Experience Platform landt, waardoor de noodzaak om segmentatietaken te plannen en uit te voeren, wordt verminderd. Op deze manier kunt u gegevens evalueren terwijl deze worden doorgegeven aan Experience Platform, zodat het lidmaatschap van het publiek automatisch wordt bijgewerkt.

## In aanmerking komende regels {#rulesets}

>[!IMPORTANT]
>
>Om het stromen segmentatie te gebruiken, moet u **** een fusiebeleid gebruiken dat &quot;Actief op Edge&quot;is. Voor meer informatie over fusiebeleid, te lezen gelieve het [ overzicht van het samenvoegbeleid ](../../profile/merge-policies/overview.md).

Een liniaal komt in aanmerking voor streamingsegmentatie als het voldoet aan een van de criteria die in de volgende tabel worden beschreven.

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor details bij het toelaten van geplande segmentatie, gelieve te verwijzen naar [ het Poortoverzicht van het Poort van het Publiek ](../ui/audience-portal.md#scheduled-segmentation).

| Type query | Details | Query | Voorbeeld |
| ---------- | ------- | ----- | ------- |
| Eén gebeurtenis binnen een tijdsvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een tijdvenster van minder dan 24 uur. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![ een voorbeeld van één enkele gebeurtenis binnen een relatief tijdvenster wordt getoond.](../images/methods/streaming/single-event.png) |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. | `homeAddress.country.equals("US", false)` | ![ een voorbeeld van een getoonde profielattributen.](../images/methods/streaming/profile-attribute.png) |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![ een voorbeeld van één enkele gebeurtenis met een profielattribuut binnen een relatief tijdvenster wordt getoond.](../images/methods/streaming/single-event-with-profile-attribute.png) |
| Meerdere gebeurtenissen binnen een relatief tijdvenster van 24 uur | Om het even welke segmentdefinitie die naar veelvoudige gebeurtenissen **binnen de laatste 24 uren** verwijst en (naar keuze) heeft één of meerdere profielattributen. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("directMarketing.emailClicked", false)) WHEN(today), C1: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![ een voorbeeld van veelvoudige gebeurtenissen met een profielattribuut wordt getoond.](../images/methods/streaming/multiple-events-with-profile-attribute.png) |

Een segmentdefinitie zal **niet** voor het stromen segmentatie in de volgende scenario&#39;s in aanmerking komen:

- De segmentdefinitie omvat Adobe Audience Manager (AAM)-segmenten of -kenmerken.
- De segmentdefinitie omvat meerdere entiteiten (vragen van meerdere entiteiten).
- De segmentdefinitie bevat een combinatie van één gebeurtenis en een `inSegment` -gebeurtenis.
   - Bijvoorbeeld, die het volgende in één enkele heersers in een ketting leggen: `inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and  CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false))  WHEN(<= 24 hours before now)])`.
- In de segmentdefinitie wordt &quot;Jaar negeren&quot; gebruikt als onderdeel van de tijdbeperkingen.

Houd rekening met de volgende richtlijnen die van toepassing zijn op streamingsegmenteringsvragen:

| Type query | Richtsnoer |
| ---------- | -------- |
| Regels voor één gebeurtenis | Het raadplegingsvenster is beperkt tot **één dag**. |
| Query uitvoeren met gebeurtenisgeschiedenis | <ul><li>Het raadplegingsvenster is beperkt tot **één dag**.</li><li>Een strikte tijd-opdracht gevend voorwaarde **moet** tussen de gebeurtenissen bestaan.</li><li>Query&#39;s met ten minste één genegeerde gebeurtenis worden ondersteund. Nochtans, kan de volledige gebeurtenis **niet** een negatie zijn.</li></ul> |

Als een segmentdefinitie wordt gewijzigd zodat deze niet meer voldoet aan de criteria voor het streamen van segmentatie, schakelt de segmentdefinitie automatisch over van &quot;Streaming&quot; naar &quot;Batch&quot;.

Bovendien, segmentonkwalificatie, zo gelijkaardig aan segmentkwalificatie, gebeurt in real time. Als een publiek niet langer in aanmerking komt voor een segment, is het dus onmiddellijk niet gekwalificeerd. Bijvoorbeeld, als de segmentdefinitie &quot;Alle gebruikers vraagt die rode schoenen in de laatste drie uren&quot;kochten, na drie uren, zullen alle profielen die aanvankelijk voor de segmentdefinitie kwalificeerden ongekwalificeerd zijn.

### Soorten publiek combineren {#combine-audiences}

Als u gegevens van zowel batch- als streaming bronnen wilt combineren, moet u de batch- en streaming componenten scheiden in verschillende soorten publiek.

Laten we bijvoorbeeld rekening houden met de volgende twee soorten publiek:

| Doelgroep | Schema | Source-type | Query-definitie | Id van publiek |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Inwoners uit Californië | Profiel | Batch | Het adres van het huis is in de staat van Californië | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Recente controles | Experience Event | Streaming | Heeft in de laatste 24 uur ten minste één afhandeling | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Als u de partijcomponent in uw het stromen publiek wilt gebruiken, zult u een verwijzing naar het partijpubliek moeten maken gebruikend segment van segmenten.

Een voorbeeldregel die de twee soorten publiek samenvoegt, ziet er als volgt uit:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

Het resulterende publiek *zal* worden geëvalueerd gebruikend het stromen segmentatie, aangezien het hefboomwerkingen het lidmaatschap van het partijpubliek door naar de component van het partijpubliek te verwijzen.

Nochtans, als u twee publiek met gebeurtenisgegevens wilt combineren, kunt u **niet** enkel de twee gebeurtenissen combineren. U moet beide soorten publiek maken en vervolgens een ander publiek maken dat `inSegment` gebruikt om naar beide soorten publiek te verwijzen.

Bijvoorbeeld, laten wij zeggen u twee publiek hebt, met beide publiek woonachtig gebeurtenisschemagegevens:

| Doelgroep | Schema | Source-type | Query-definitie | Id van publiek |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Recente verlaten | Gebeurtenis Experience | Batch | Heeft ten minste één gebeurtenis voor verlaten in de afgelopen 24 uur | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Recente controles | Experience Event | Streaming | Heeft in de laatste 24 uur ten minste één afhandeling | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

In deze situatie, zou u een derde publiek als volgt moeten creëren:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

## publiek maken {#create-audience}

U kunt een publiek tot stand brengen dat gebruikend het stromen segmentatie gebruikend of de Dienst API van de Segmentatie of door het Portaal van de Publiek in UI wordt geëvalueerd.

Een segmentdefinitie kan stromen-toegelaten zijn als het één van de [ in aanmerking komende heersers ](#eligible-rulesets) aanpast.

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

Binnen de Bouwer van het Segment, creeer een segmentdefinitie die één van de [ in aanmerking komende heersers ](#eligible-rulesets) aanpast. Als de segmentdefinitie voor het stromen segmentatie kwalificeert, zult u **[!UICONTROL Streaming]** als **[!UICONTROL Evaluation method]** kunnen selecteren.

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

Meer over het bekijken van publiek in Experience Platform leren, gelieve de [ gids van het Portaal van het Publiek ](../ui/audience-portal.md) te lezen.

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
