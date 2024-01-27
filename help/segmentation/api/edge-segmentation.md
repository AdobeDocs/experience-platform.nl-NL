---
solution: Experience Platform
title: Edge Segmentation met de API
description: Dit document bevat voorbeelden over het gebruik van randsegmentatie met de Adobe Experience Platform Segmentation Service API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: d3c0e5ed596661f11191bbcd8d51c888bbd4c1d2
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 0%

---

# Randsegmentatie

>[!NOTE]
>
>In het volgende document wordt beschreven hoe u randsegmentatie kunt uitvoeren met behulp van de API. Voor informatie die randsegmentatie uitvoert die UI gebruikt, gelieve te lezen [gebruikersgids voor randsegmentatie](../ui/edge-segmentation.md).
>
>De segmentatie van de rand is nu over het algemeen beschikbaar aan alle gebruikers van het Platform. Als u de definities van het randsegment tijdens bèta creeerde, zullen deze segmentdefinities operationeel blijven.

De segmentatie van de rand is de capaciteit om segmentdefinities in Adobe Experience Platform onmiddellijk op de rand te evalueren, toelatend de zelfde pagina en volgende het verpersoonlijkingsgebruiksgevallen van de paginagrootte.

>[!IMPORTANT]
>
> De Edge-gegevens worden opgeslagen op een locatie op de Edge-server die het dichtst bij de locatie ligt waar ze zijn verzameld en kunnen worden opgeslagen op een andere locatie dan die welke is aangewezen als het Adobe Experience Platform-datacenter in de hub (of principal).
>
> Bovendien zal de engine voor randsegmentatie alleen aanvragen aan de rand uitvoeren waar deze zich bevindt **één** primaire gemarkeerde identiteit, die consistent is met niet-Edge-primaire identiteiten.

## Aan de slag

Deze ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] diensten in verband met randsegmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Hiermee kunt u een publiek opbouwen op [!DNL Real-Time Customer Profile] gegevens.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring.

Als u aanroepen naar de eindpunten van de Experience Platform-API wilt uitvoeren, leest u de handleiding op [aan de slag met platform-API&#39;s](../../landing/api-guide.md) om over vereiste kopballen en te leren hoe te om steekproefAPI vraag te lezen.

## Type Edge-segmenteringsquery {#query-types}

Opdat een segment wordt geëvalueerd gebruikend randsegmentatie, moet de vraag aan de volgende richtlijnen in overeenstemming zijn:

| Type query | Details | Voorbeeld | PQL-voorbeeld |
| ---------- | ------- | ------- | ----------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die een artikel aan hun winkelwagentje hebben toegevoegd. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Eén profiel | Alle segmentdefinities die verwijzen naar één kenmerk met alleen profiel | Mensen die in de VS wonen. | `homeAddress.countryCode = "US"` |
| Eén gebeurtenis die naar een profiel verwijst | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die in de VS wonen en die de homepage hebben bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Een enkele gebeurtenis met een profielkenmerk negeren | Elke segmentdefinitie die verwijst naar een negatiefunctie van één binnenkomende gebeurtenis en een of meer profielkenmerken | Mensen die in de VS wonen en **niet** heeft de homepage bezocht. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Eén gebeurtenis binnen een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een ingestelde periode. | Mensen die de laatste 24 uur de homepage hebben bezocht. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | Mensen die in de VS wonen en de laatste 24 uur de homepage hebben bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis die binnen een tijdvenster is genegeerd met een profielkenmerk | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde enkele binnenkomende gebeurtenis binnen een tijdsperiode. | Mensen die in de VS wonen en **niet** heeft de laatste 24 uur de homepage bezocht. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)]))` |
| Frequentiegebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een gebeurtenis die een bepaald aantal keren binnen een tijdvenster van 24 uur plaatsvindt. | Personen die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Frequentiegebeurtenis met een profielkenmerk binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen uit de VS die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Gebeurtenis met een negatieve frequentie binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen die de homepage niet hebben bezocht **meer** meer dan vijf keer in de laatste 24 uur. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Meerdere inkomende treffers binnen een tijdprofiel van 24 uur | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen die de homepage hebben bezocht **of** heeft de laatste 24 uur de afhandelingspagina bezocht. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Meerdere gebeurtenissen met een profiel binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen uit de VS die de homepage hebben bezocht **en** heeft de laatste 24 uur de afhandelingspagina bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. | Mensen die in de VS wonen en in het segment &quot;bestaand&quot; zitten. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Query die verwijst naar een kaart | Elke segmentdefinitie die verwijst naar een kaart met eigenschappen. | Personen die aan hun winkelwagentje hebben toegevoegd op basis van externe segmentgegevens. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Daarnaast wordt het segment **moet** gebonden zijn aan een samenvoegbeleid dat op rand actief is. Lees voor meer informatie over samenvoegingsbeleid de [handleiding voor samenvoegbeleid](../../profile/api/merge-policies.md).

Een segmentdefinitie zal **niet** voor randsegmentatie in de volgende scenario&#39;s worden toegelaten:

- De segmentdefinitie omvat een combinatie van één gebeurtenis en een `inSegment` gebeurtenis.
   - Als het segment echter in de `inSegment` gebeurtenis is alleen profiel, de segmentdefinitie **zal** worden ingeschakeld voor randsegmentatie.

## Alle segmenten ophalen die zijn ingeschakeld voor segmentatie van randen

U kunt een lijst van alle segmenten terugwinnen die voor randsegmentatie binnen uw organisatie door een verzoek van de GET aan te dienen worden toegelaten `/segment/definitions` eindpunt.

**API-indeling**

Als u segmenten wilt ophalen die zijn ingeschakeld voor randsegmentatie, moet u de queryparameter opnemen `evaluationInfo.synchronous.enabled=true` in het aanvraagpad.

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

**Antwoord**

Een succesvolle reactie keert een serie van segmenten in uw organisatie terug die voor randsegmentatie worden toegelaten. Meer gedetailleerde informatie over de teruggekeerde segmentdefinitie kan in worden gevonden [segmentdefinities, eindhulplijn](./segment-definitions.md).

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

U kunt een segment tot stand brengen dat voor randsegmentatie door een verzoek van de POST aan wordt toegelaten `/segment/definitions` eindpunt dat één van [hierboven vermelde typen query voor randsegmentatie](#query-types).

**API-indeling**

```http
POST /segment/definitions
```

**Verzoek**

>[!NOTE]
>
>Het onderstaande voorbeeld is een standaardverzoek om een segment te maken. Lees de zelfstudie voor meer informatie over het maken van een segmentdefinitie [een segment maken](../tutorials/create-a-segment.md).

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

**Antwoord**

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

Ga voor meer informatie over het uitvoeren van vergelijkbare acties en het werken met segmenten via de Adobe Experience Platform-gebruikersinterface naar de [Gebruikershandleiding voor Segment Builder](../ui/segment-builder.md).

## Bijlage

In de volgende sectie worden veelgestelde vragen over de segmentatie van randen weergegeven:

### Hoe lang duurt het voor een segment beschikbaar is op het Edge-netwerk?

Het duurt tot één uur voor een segment beschikbaar is in het Edge-netwerk.