---
title: API-eindpunt voor controlegebeurtenissen
description: Leer hoe u auditgebeurtenissen in Experience Platform ophaalt met behulp van de API voor auditquery.
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Het eindpunt van gebeurtenissen controleren

De logboeken van de controle worden gebruikt om details van gebruikersactiviteit voor diverse diensten en mogelijkheden te verstrekken. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde. Met het eindpunt `/audit/events` in de [!DNL Audit Query] API kunt u gebeurtenisgegevens voor de activiteit van uw organisatie in [!DNL Experience Platform] programmatisch ophalen.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Audit Query]  API ](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Controles weergeven

U kunt gebeurtenisgegevens ophalen door een GET-aanvraag in te dienen bij het `/audit/events` -eindpunt en de gebeurtenissen op te geven die u in de payload wilt ophalen.

**API formaat**

```http
GET /audit/events
```

De API van [!DNL Audit Query] ondersteunt het gebruik van queryparameters voor pagina- en filterresultaten bij het weergeven van gebeurtenissen.

| Parameter | Beschrijving |
| --- | --- |
| `limit` | Het maximumaantal records dat in de reactie moet worden geretourneerd. De standaardwaarde `limit` is 50. |
| `start` | Een aanwijzer naar het eerste item voor de geretourneerde zoekresultaten. Om tot de volgende pagina van resultaten toegang te hebben, zou deze parameter met de zelfde hoeveelheid moeten verhogen die door grens wordt vermeld. Voorbeeld: als u toegang wilt krijgen tot de volgende pagina met resultaten voor een aanvraag met limit=50, gebruikt u de parameter start=50, vervolgens start=100 voor de pagina erna, enzovoort. |
| `queryId` | Wanneer het maken van een vraag aan het /audit/events eindpunt, omvat de reactie een vraagId koordbezit. Om de zelfde vraag in een afzonderlijke vraag te maken, kunt u de waarde van Id als één enkele vraagparameter omvatten in plaats van manueel het vormen van de onderzoeksparameters opnieuw. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Reactie**

Een succesvolle reactie keert de resulterende datapoints voor de metriek en de filters terug die in het verzoek worden gespecificeerd.

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `events` | Een array waarvan de objecten elk van de gebeurtenissen vertegenwoordigen die in de aanvraag zijn opgegeven. Elk object bevat informatie over de filterconfiguratie en retourneert gebeurtenisgegevens. |
| `userEmail` | De e-mail van de gebruiker die de gebeurtenis heeft uitgevoerd. |
| `eventType` | Het type gebeurtenis. Tot de gebeurtenistypen behoren `Core` en `Enhanced` . |
| `imsOrgId` | De id van de organisatie waarop de gebeurtenis heeft plaatsgevonden. |
| `permissionResource` | Het product of de capaciteit die de toestemming verstrekte voeren de actie uit. Een bron kan een van de volgende zijn: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Het type machtiging dat bij de handeling is betrokken. |
| `assetType` | Het type Experience Platform-resource waarop de handeling is uitgevoerd. |
| `assetId` | Een unieke id voor de Experience Platform-bron waarop de handeling is uitgevoerd. |
| `assetName` | De naam van de Experience Platform-bron waarop de handeling is uitgevoerd. |
| `action` | Het type actie dat is opgenomen voor de gebeurtenis. Een handeling kan een van de volgende handelingen zijn: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | De status van de actie. Een status kan een van de volgende zijn: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
