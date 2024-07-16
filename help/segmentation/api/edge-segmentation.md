---
solution: Experience Platform
title: Edge Segmentation using the API
description: Dit document bevat voorbeelden over het gebruik van randsegmentatie met de Adobe Experience Platform Segmentation Service API.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Edge-segmentatie

>[!NOTE]
>
>In het volgende document wordt beschreven hoe u randsegmentatie kunt uitvoeren met behulp van de API. Voor informatie die randsegmentatie gebruikend UI uitvoert, te lezen gelieve de [ gids van de randsegmentatie UI ](../ui/edge-segmentation.md).
>
>Edge-segmentatie is nu algemeen beschikbaar voor alle platformgebruikers. Als u de definities van het randsegment tijdens bèta creeerde, zullen deze segmentdefinities operationeel blijven.

Edge-segmentatie is de mogelijkheid om segmentdefinities direct aan de rand van Adobe Experience Platform te evalueren, zodat dezelfde pagina en de volgende pagina kunnen worden gebruikt.

>[!IMPORTANT]
>
> De Edge-gegevens worden opgeslagen op een locatie op de Edge-server die het dichtst bij de locatie ligt waar ze zijn verzameld en kunnen worden opgeslagen op een andere locatie dan die welke is aangewezen als het Adobe Experience Platform-datacenter in de hub (of principal).
>
> Bovendien, zal de motor van de randsegmentatie slechts verzoeken op de rand waar er **één** primaire duidelijke identiteit is, die met niet op rand-gebaseerde primaire identiteiten verenigbaar is.

## Aan de slag

Deze ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] -services die te maken hebben met segmentatie van randen. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform consumentenprofiel in realtime, gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): hiermee kunt u soorten publiek maken op basis van [!DNL Real-Time Customer Profile] -gegevens.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Platform] gegevens voor de klantervaring indeelt.

Om vraag aan om het even welk Experience Platform API eindpunten met succes te maken, te lezen gelieve de gids op [ begonnen wordt met Platform APIs ](../../landing/api-guide.md) om over vereiste kopballen te leren en hoe te om steekproefAPI vraag te lezen.

## Type Edge-segmentquery {#query-types}

Opdat een segment wordt geëvalueerd gebruikend randsegmentatie, moet de vraag aan de volgende richtlijnen in overeenstemming zijn:

| Type query | Details | Voorbeeld | PQL-voorbeeld |
| ---------- | ------- | ------- | ----------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die een artikel aan hun winkelwagentje hebben toegevoegd. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Eén profiel | Alle segmentdefinities die verwijzen naar één kenmerk met alleen profiel | Mensen die in de VS wonen. | `homeAddress.countryCode = "US"` |
| Eén gebeurtenis die naar een profiel verwijst | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die in de VS wonen en die de homepage hebben bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Een enkele gebeurtenis met een profielkenmerk negeren | Elke segmentdefinitie die verwijst naar een negatiefunctie van één binnenkomende gebeurtenis en een of meer profielkenmerken | De mensen die in de V.S. wonen en **niet** hebben de homepage bezocht. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Eén gebeurtenis binnen een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een ingestelde periode. | Mensen die de laatste 24 uur de homepage hebben bezocht. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | Mensen die in de VS wonen en de laatste 24 uur de homepage hebben bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis die binnen een tijdvenster is genegeerd met een profielkenmerk | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde enkele binnenkomende gebeurtenis binnen een tijdsperiode. | De mensen die in de V.S. wonen en **** hebben niet de homepage in de laatste 24 uren bezocht. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)]))` |
| Frequentiegebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een gebeurtenis die een bepaald aantal keren binnen een tijdvenster van 24 uur plaatsvindt. | De mensen die de homepage **minstens** vijf keer in de laatste 24 uren bezochten. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Frequentiegebeurtenis met een profielkenmerk binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | De mensen van de V.S. die de homepage **minstens** vijf keer in de laatste 24 uren bezochten. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Gebeurtenis met een negatieve frequentie binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | De mensen die niet de homepage **meer** meer dan vijf keer in de laatste 24 uren hebben bezocht. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Meerdere inkomende treffers binnen een tijdprofiel van 24 uur | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | De mensen die de homepage **of** bezochten de controlepagina binnen de laatste 24 uren. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Meerdere gebeurtenissen met een profiel binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | De mensen van de V.S. die de homepage **bezochten en** bezochten de controlepagina binnen de laatste 24 uren. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. | Mensen die in de VS wonen en in het segment &quot;bestaand&quot; zitten. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Query die verwijst naar een kaart | Elke segmentdefinitie die verwijst naar een kaart met eigenschappen. | Personen die aan hun winkelwagentje hebben toegevoegd op basis van externe segmentgegevens. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Bovendien, moet het segment **** aan een fusiebeleid worden gebonden dat op rand actief is. Voor meer informatie over samenvoegingsbeleid, te lezen gelieve de [ gids van het samenvoegingsbeleid ](../../profile/api/merge-policies.md).

Een segmentdefinitie zal **** niet voor randsegmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie bevat een combinatie van één gebeurtenis en een `inSegment` -gebeurtenis.
   - Nochtans, als het segment in de `inSegment` gebeurtenis profiel slechts is, zal de segmentdefinitie **** voor randsegmentatie worden toegelaten.
- In de segmentdefinitie wordt &quot;Jaar negeren&quot; gebruikt als onderdeel van de tijdbeperkingen.

## Alle segmenten ophalen die zijn ingeschakeld voor segmentatie van randen

U kunt een lijst van alle segmenten terugwinnen die voor randsegmentatie binnen uw organisatie door een verzoek van de GET aan het `/segment/definitions` eindpunt te doen worden toegelaten.

**API formaat**

Als u segmenten wilt ophalen die zijn ingeschakeld voor randsegmentatie, moet u de queryparameter `evaluationInfo.synchronous.enabled=true` opnemen in het aanvraagpad.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een serie van segmenten in uw organisatie terug die voor randsegmentatie worden toegelaten. De meer gedetailleerde informatie over de gesegmenteerde teruggekeerde definitie kan in de [ gids van het de segmentdefinitiedetectietype ](./segment-definitions.md) worden gevonden.

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

## Een segment maken dat is ingeschakeld voor randsegmentatie

U kunt een segment tot stand brengen dat voor randsegmentatie door een verzoek van de POST aan het `/segment/definitions` eindpunt wordt toegelaten dat één van de [ hierboven vermelde de vraagtypes van de randsegmentatie ](#query-types) aanpast.

**API formaat**

```http
POST /segment/definitions
```

**Verzoek**

>[!NOTE]
>
>Het onderstaande voorbeeld is een standaardverzoek om een segment te maken. Voor meer informatie over het creëren van een segmentdefinitie, te lezen gelieve het leerprogramma bij [ het creëren van een segment ](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
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
    }
}'
```

**Reactie**

Een succesvolle reactie keert de details van de pas gecreëerde segmentdefinitie terug die voor randsegmentatie wordt toegelaten.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
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
```

## Volgende stappen

Nu u weet hoe te om rand-segmentatie-Toegelaten segmenten tot stand te brengen, kunt u hen gebruiken om het gebruik van de zelfde-pagina en volgende-pagina verpersoonlijking toe te laten gevallen.

Leren hoe te om gelijkaardige acties uit te voeren en met segmenten te werken gebruikend het gebruikersinterface van Adobe Experience Platform, gelieve de [ gebruikersgids van de Bouwer van het Segment ](../ui/segment-builder.md) te bezoeken.

## Bijlage

In de volgende sectie worden veelgestelde vragen over de segmentatie van randen weergegeven:

### Hoe lang duurt het voordat een segment beschikbaar is op de Edge Network?

Het duurt tot één uur voor een segment beschikbaar is op de Edge Network.