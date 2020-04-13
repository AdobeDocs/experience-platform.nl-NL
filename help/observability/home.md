---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Observability Insights
topic: overview
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c

---


# Overzicht van observatiegegevens van Adobe Experience Platform

Observability Insights is een RESTful API waarmee u belangrijke waarneembaarheidsmetriek in het Platform van de Ervaring van Adobe kunt blootstellen. Deze metriek verstrekt inzicht in het gebruiksstatistieken van het Platform, gezondheid-controles voor de diensten van het Platform, historische tendensen, en prestatiesindicatoren voor diverse functies van het Platform.

In dit document wordt een voorbeeld gegeven van een aanroep van de API Observability Insights. Voor een volledige lijst van de eindpunten van de Waarnemelijkheid, gelieve te verwijzen naar de [Bron](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)van de Inzichten van de Observability API.

## Aan de slag

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt. Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../sandboxes/home.md).

* x-sandbox-name: `{SANDBOX_NAME}`

## Metrische waarden voor waarneembaarheid ophalen

U kunt waarnemingsbaarheidsmetriek terugwinnen door een GET verzoek aan het `/metrics` eindpunt in de Inzichten API van de Waarneming te doen.

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
| `{ID}` | De id voor een bepaald middel van het Platform waarvan metriek u wilt blootstellen. Deze id kan optioneel, vereist of niet van toepassing zijn, afhankelijk van de gebruikte maatstaven. Raadpleeg het referentiedocument over [beschikbare metriek](metrics.md)voor een lijst met beschikbare metriek en ondersteunde id&#39;s (zowel vereist als optioneel) voor elke meting. |
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

Een geslaagde reactie retourneert een lijst met objecten die elk een tijdstempel bevatten binnen de opgegeven waarden `dateRange` en de bijbehorende waarden voor de metriek die in het aanvraagpad zijn opgegeven. Als de bron `id` van een platform is opgenomen in het aanvraagpad, zijn de resultaten alleen van toepassing op die specifieke bron. Als het `id` wordt weggelaten, zullen de resultaten op alle toepasselijke middelen binnen uw IMS Organisatie van toepassing zijn.

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