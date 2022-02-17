---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;randsegmentatie;Edge-segmentatie;streamingrand;
solution: Experience Platform
title: 'Edge Segmentation met de API '
topic-legacy: developer guide
description: Dit document bevat voorbeelden over het gebruik van randsegmentatie met de Adobe Experience Platform Segmentation Service API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 0173fbd36791f837e0d0336f9fa7bcc84e64909f
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Randsegmentatie

>[!NOTE]
>
>In het volgende document wordt beschreven hoe u randsegmentatie kunt uitvoeren met behulp van de API. Voor informatie die randsegmentatie uitvoert die UI gebruikt, gelieve te lezen [UI-hulplijn voor randsegmentatie](../ui/edge-segmentation.md).
>
>De segmentatie van de rand is nu over het algemeen beschikbaar aan alle gebruikers van het Platform. Als u Edge-segmenten hebt gemaakt tijdens de bètaversie, blijven deze segmenten operationeel.

De segmentatie van de rand is de capaciteit om segmenten in Adobe Experience Platform onmiddellijk op de rand te evalueren, toelatend de zelfde pagina en volgende het verpersoonlijkingsgebruiksgevallen van de paginagrootte.

>[!IMPORTANT]
>
> De Edge-gegevens worden opgeslagen op een locatie op de Edge-server die het dichtst bij de locatie ligt waar ze zijn verzameld en kunnen worden opgeslagen op een andere locatie dan die welke is aangewezen als het Adobe Experience Platform-datacenter in de hub (of principal).
>
> Bovendien zal de engine voor randsegmentatie alleen aanvragen aan de rand uitvoeren waar deze zich bevindt **één** primaire gemarkeerde identiteit, die consistent is met primaire identiteiten die niet op randen zijn gebaseerd.

## Aan de slag

Deze ontwikkelaarshandleiding vereist een goed begrip van de verschillende [!DNL Adobe Experience Platform] diensten in verband met randsegmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Segmentation]](../home.md): Biedt de mogelijkheid om segmenten en publiek te maken van uw [!DNL Real-time Customer Profile] gegevens.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.

Als u aanroepen naar de eindpunten van de Experience Platform-API wilt uitvoeren, leest u de handleiding op [aan de slag met Platform-API&#39;s](../../landing/api-guide.md) om over vereiste kopballen en te leren hoe te om steekproefAPI vraag te lezen.

## Type Edge-segmenteringsquery {#query-types}

Opdat een segment wordt geëvalueerd gebruikend randsegmentatie, moet de vraag aan de volgende richtlijnen in overeenstemming zijn:

| Type query | Details | Voorbeeld |
| ---------- | ------- | ------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die een artikel aan hun winkelwagentje hebben toegevoegd. |
| Eén gebeurtenis die naar een profiel verwijst | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die in de VS wonen en die de homepage hebben bezocht. |
| Een enkele gebeurtenis met een profielkenmerk negeren | Elke segmentdefinitie die verwijst naar een negatiefunctie van één binnenkomende gebeurtenis en een of meer profielkenmerken | Mensen die in de VS wonen en **niet** heeft de homepage bezocht. |
| Eén gebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen 24 uur. | Mensen die de laatste 24 uur de homepage hebben bezocht. |
| Eén gebeurtenis met een profielkenmerk binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en één binnenkomende gebeurtenis binnen 24 uur. | Mensen die in de VS wonen en de laatste 24 uur de homepage hebben bezocht. |
| Eén gebeurtenis die binnen een tijdvenster van 24 uur is genegeerd met een profielkenmerk | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde enkele binnenkomende gebeurtenis binnen 24 uur. | Mensen die in de VS wonen en **niet** heeft de laatste 24 uur de homepage bezocht. |
| Frequentiegebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een gebeurtenis die een bepaald aantal keren binnen een tijdvenster van 24 uur plaatsvindt. | Personen die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. |
| Frequentiegebeurtenis met een profielkenmerk binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen uit de VS die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. |
| Gebeurtenis met een negatieve frequentie binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen die de homepage niet hebben bezocht **meer** meer dan vijf keer in de laatste 24 uur. |
| Meerdere inkomende treffers binnen een tijdprofiel van 24 uur | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen die de homepage hebben bezocht **of** heeft de laatste 24 uur de afhandelingspagina bezocht. |
| Meerdere gebeurtenissen met een profiel binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen uit de VS die de homepage hebben bezocht **en** heeft de laatste 24 uur de afhandelingspagina bezocht. |

Daarnaast wordt het segment **moet** gebonden zijn aan een samenvoegbeleid dat op rand actief is. Lees voor meer informatie over samenvoegingsbeleid de [handleiding voor samenvoegbeleid](../../profile/api/merge-policies.md).

## Alle segmenten ophalen die zijn ingeschakeld voor segmentatie van randen

U kunt een lijst van alle segmenten terugwinnen die voor randsegmentatie binnen uw IMS Organisatie door een verzoek van de GET aan te dienen worden toegelaten `/segment/definitions` eindpunt.

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
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een serie van segmenten in uw IMS Organisatie terug die voor randsegmentatie worden toegelaten. Meer gedetailleerde informatie over de teruggekeerde segmentdefinitie kan in worden gevonden [segmentdefinities, eindhulplijn](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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
            "imsOrgId": "{IMS_ORG_ID}",
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrgId": "{IMS_ORG}",
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
