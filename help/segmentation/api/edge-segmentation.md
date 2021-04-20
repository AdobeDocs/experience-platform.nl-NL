---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;randsegmentatie;Edge-segmentatie;streamingrand;
solution: Experience Platform
title: 'Edge Segmentation met de API '
topic: developer guide
description: Dit document bevat voorbeelden over het gebruik van randsegmentatie met de Adobe Experience Platform Segmentation Service API.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 36169a42c7f6a73ca9cc165cd338d6a1cf245bfc
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Randsegmentatie (bèta)

>[!NOTE]
>
>In het volgende document wordt beschreven hoe u randsegmentatie kunt uitvoeren met behulp van de API. Voor informatie die randsegmentatie gebruikend UI uitvoert, te lezen gelieve [de gids van de segmentatie van de rand UI](../ui/edge-segmentation.md). Bovendien wordt de segmentatie tussen randen momenteel in bèta uitgevoerd. De documentatie en de functionaliteit kunnen worden gewijzigd.

De segmentatie van de rand is de capaciteit om segmenten in Adobe Experience Platform onmiddellijk op de rand te evalueren, toelatend de zelfde pagina en volgende het verpersoonlijkingsgebruiksgevallen van de paginagrootte.

## Aan de slag

Deze ontwikkelaarsgids vereist een werkend inzicht in de diverse [!DNL Adobe Experience Platform] diensten betrokken bij randsegmentatie. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd consumentenprofiel in real time, dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Segmentation]](../home.md): Verstrekt de capaciteit om segmenten en publiek van uw  [!DNL Real-time Customer Profile] gegevens tot stand te brengen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

Om met succes vraag aan [!DNL Data Prep] API eindpunten te maken, te lezen gelieve de gids op [Aan de slag met Platform APIs](../../landing/api-guide.md) om over vereiste kopballen en hoe te om steekproefAPI vraag te lezen.

## Type randsegmenteringsquery {#query-types}

Opdat een segment wordt geëvalueerd gebruikend randsegmentatie, moet de vraag aan de volgende richtlijnen in overeenstemming zijn:

| Type query | Details |
| ---------- | ------- |
| Binnenkomende hit | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. |
| Binnenkomende hit die verwijst naar een profiel | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, zonder tijdbeperking, en een of meer profielkenmerken. |
| Frequentiequery | Elke segmentdefinitie die verwijst naar een gebeurtenis die minstens een bepaald aantal keer plaatsvindt. |
| Frequentiequery die naar een profiel verwijst | Elke segmentdefinitie die verwijst naar een gebeurtenis die minstens een bepaald aantal keren plaatsvindt en die een of meer profielkenmerken heeft. |

{style=&quot;table-layout:auto&quot;}

De volgende vraagtypes zijn **not** momenteel gesteund door randsegmentatie:

| Type query | Details |
| ---------- | ------- |
| Het venster Relative-time | Als een vraag naar een tijdvenster verwijst, kan het niet worden geëvalueerd gebruikend randsegmentatie. |
| Negatie | Als een vraag een negatie, of een `not` gebeurtenis bevat, kan het niet worden geëvalueerd gebruikend randsegmentatie. |
| Meerdere gebeurtenissen | Als een query meer dan één gebeurtenis bevat, kan deze niet worden geëvalueerd met behulp van randsegmentatie. |

{style=&quot;table-layout:auto&quot;}

## Alle segmenten ophalen die zijn ingeschakeld voor segmentatie van randen

U kunt een lijst van alle segmenten terugwinnen die voor randsegmentatie binnen uw IMS Organisatie door een verzoek van de GET aan het `/segment/definitions` eindpunt te doen worden toegelaten.

**API-indeling**

Om segmenten terug te winnen die voor randsegmentatie worden toegelaten, moet u de vraagparameter `evaluationInfo.synchronous.enabled=true` in de verzoekweg omvatten.

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

Een succesvolle reactie keert een serie van segmenten in uw IMS Organisatie terug die voor randsegmentatie worden toegelaten. Meer gedetailleerde informatie over de gesegmenteerde teruggekeerde definitie kan in [segment worden gevonden eindpuntgids](./segment-definitions.md).

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

U kunt een segment tot stand brengen dat voor randsegmentatie door een verzoek van de POST aan het `/segment/definitions` eindpunt wordt toegelaten te doen. Naast het aanpassen van één van de [de types van randsegmenteringsvraag hierboven](#query-types), moet u de `evaluationInfo.synchronous.enabled` vlag in de nuttige lading aan waar plaatsen.

**API-indeling**

```http
POST /segment/definitions
```

**Verzoek**

>[!NOTE]
>
>Het onderstaande voorbeeld is een standaardverzoek om een segment te maken. Lees voor meer informatie over het maken van een segmentdefinitie de zelfstudie over [het maken van een segment](../tutorials/create-a-segment.md).

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
    },
    "evaluationInfo": {
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | Het `evaluationInfo` voorwerp bepaalt het type van evaluatie de segmentdefinitie zal ondergaan. Als u randsegmentatie wilt gebruiken, stelt u `evaluationInfo.synchronous.enabled` in met een waarde `true`. |

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
```

## Volgende stappen

Nu u weet hoe te om rand-segmentatie-Toegelaten segmenten tot stand te brengen, kunt u hen gebruiken om het gebruik van de zelfde-pagina en volgende-pagina verpersoonlijking toe te laten gevallen.

Als u wilt leren hoe u vergelijkbare acties kunt uitvoeren en met segmenten kunt werken via de Adobe Experience Platform-gebruikersinterface, gaat u naar de [gebruikersgids voor segmentBuilder](../ui/segment-builder.md).
