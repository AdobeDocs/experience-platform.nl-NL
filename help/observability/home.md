---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Observability Insights
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---


# Overzicht van Adobe Experience Platform Observability Insights

Observability Insights is een RESTful API die u toestaat om zeer belangrijke waarneembaarheidsmetriek in Adobe Experience Platform bloot te stellen. Deze metriek verstrekt inzicht in [!DNL Platform] gebruiksstatistieken, gezondheid-controles voor de [!DNL Platform] diensten, historische tendensen, en prestatiesindicatoren voor diverse [!DNL Platform] functionaliteit.

In dit document wordt een voorbeeld gegeven van een aanroep van de API Observability Insights. Voor een volledige lijst van de eindpunten van de Waarnemelijkheid, gelieve te verwijzen naar de [Bron](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)van de Inzichten van de Observability API.

## Aan de slag

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Voor alle aanvragen voor [!DNL Platform] API&#39;s is een header nodig die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../sandboxes/home.md)sandbox.

* x-sandbox-name: `{SANDBOX_NAME}`

## Metrische waarden voor waarneembaarheid ophalen

U kunt de metriek van de waarneembaarheid terugwinnen door een verzoek van de GET aan het `/metrics` eindpunt in de Inzichten API van de Waarnembaarheid te richten.

**API-indeling**

Wanneer het gebruiken van het `/metrics` eindpunt, moet minstens één metrische verzoekparameter worden verstrekt. Andere vraagparameters zijn facultatief voor het filtreren resultaten.

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| Parameter | Beschrijving |
| --- | --- |
| `{METRIC}` | De metrisch u wilt blootstellen. Wanneer het combineren van veelvoudige metriek in één enkele vraag, moet u ampersand (`&`) gebruiken om individuele metriek te scheiden. Bijvoorbeeld, `metric={METRIC_1}&metric={METRIC_2}`. |
| `{ID}` | De id voor een bepaalde [!DNL Platform] bron waarvan u de meetgegevens wilt weergeven. Deze id kan optioneel, vereist of niet van toepassing zijn, afhankelijk van de gebruikte maatstaven. Raadpleeg het referentiedocument over [beschikbare metriek](metrics.md)voor een lijst met beschikbare metriek en ondersteunde id&#39;s (zowel vereist als optioneel) voor elke meting. |
| `{DATE_RANGE}` | Het datumbereik voor de metriek die u wilt weergeven, in de ISO 8601-indeling (bijvoorbeeld `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`). |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met objecten die elk een tijdstempel bevatten binnen de opgegeven waarden `dateRange` en de bijbehorende waarden voor de metriek die in het aanvraagpad zijn opgegeven. Als het `id` van een [!DNL Platform] bron is opgenomen in het aanvraagpad, zijn de resultaten alleen van toepassing op die bron. Als het `id` wordt weggelaten, zullen de resultaten op alle toepasselijke middelen binnen uw IMS Organisatie van toepassing zijn.

```json
{
    "id": "5cf8ab4ec48aba145214abeb",
    "imsOrgId": "{IMS_ORG}",
    "timeseries": {
        "granularity": "MONTH",
        "items": [
            {
                "timestamp": "2019-06-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1125,
                    "timeseries.ingestion.dataset.size": 32320
                }
            },
            {
                "timestamp": "2019-05-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 1003,
                    "timeseries.ingestion.dataset.size": 31409
                }
            },
            {
                "timestamp": "2019-04-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-03-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 740,
                    "timeseries.ingestion.dataset.size": 25809
                }
            },
            {
                "timestamp": "2019-02-01T00:00:00Z",
                "metrics": {
                    "timeseries.ingestion.dataset.recordsuccess.count": 390,
                    "timeseries.ingestion.dataset.size": 16801
                }
            }
        ],
        "_page": null,
        "_links": null
    },
    "stats": {}
}
```

## Volgende stappen

In dit document wordt een overzicht gegeven van de API voor observatiegegevens. Zie het document over [beschikbare metriek](metrics.md) voor een volledige lijst van metriek die in API kan worden gebruikt.