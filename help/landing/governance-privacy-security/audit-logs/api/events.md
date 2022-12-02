---
title: API-eindpunt voor controlegebeurtenissen
description: Leer hoe te om controlegebeurtenissen in Experience Platform terug te winnen gebruikend de Vraag van de Controle API.
source-git-commit: 2abd3ea6f1affa7d83a3ae6ee368fa4b5b890d94
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Het eindpunt van gebeurtenissen controleren

De logboeken van de controle worden gebruikt om details van gebruikersactiviteit voor diverse diensten en mogelijkheden te verstrekken. Elke actie die in een logboek wordt geregistreerd bevat meta-gegevens die op het actietype, datum en tijd, e-mailidentiteitskaart van de gebruiker die de actie, en extra attributen relevant voor het actietype uitvoerde. De `/audit/events` in de [!DNL Audit Query] API staat u toe om gebeurtenisgegevens voor de activiteit van uw organisatie programmatically terug te winnen in [!DNL Platform].

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

## Controles weergeven

U kunt gebeurtenisgegevens ophalen door een GET-aanvraag in te dienen bij de `/audit/events` eindpunt, die de gebeurtenissen specificeren u in de nuttige lading wenst terug te winnen.

**API-indeling**

```http
GET /audit/events
```

De [!DNL Audit Query] API ondersteunt het gebruik van queryparameters voor pagina- en filterresultaten bij het weergeven van gebeurtenissen.

| Parameter | Beschrijving |
| --- | --- |
| `limit` | Het maximumaantal records dat in de reactie moet worden geretourneerd. De standaardwaarde `limit` is 50. |
| `start` | Een aanwijzer naar het eerste item voor de geretourneerde zoekresultaten. Om tot de volgende pagina van resultaten toegang te hebben, zou deze parameter met de zelfde hoeveelheid moeten verhogen die door grens wordt vermeld. Voorbeeld: Als u toegang wilt krijgen tot de volgende pagina met resultaten voor een aanvraag met limit=50, gebruikt u de parameter start=50, vervolgens start=100 voor de pagina daarna, enzovoort. |
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

**Antwoord**

Een succesvolle reactie keert de resulterende datapoints voor de metriek en de filters terug die in het verzoek worden gespecificeerd.

```json
{
   "_embedded": {
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform-int.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `customerAuditLogList` | Een array waarvan de objecten elk van de gebeurtenissen vertegenwoordigen die in de aanvraag zijn opgegeven. Elk object bevat informatie over de filterconfiguratie en retourneert gebeurtenisgegevens. |
| `userEmail` | De e-mail van de gebruiker die de gebeurtenis heeft uitgevoerd. |
| `eventType` | Het type gebeurtenis. Tot de typen gebeurtenissen behoren: `Core` en `Enhanced`. |
| `imsOrgId` | De id van de organisatie waarop de gebeurtenis heeft plaatsgevonden. |
| `permissionResource` | Het product of de capaciteit die de toestemming verstrekte voeren de actie uit. Een bron kan een van de volgende zijn: <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | Het type machtiging dat bij de handeling is betrokken. |
| `assetType` | Het type van middel van het Platform dat de actie werd uitgevoerd. |
| `assetId` | Een unieke id voor de bron van het Platform waarop de handeling is uitgevoerd. |
| `assetName` | De naam van de bron van het Platform waarop de actie werd uitgevoerd. |
| `action` | Het type actie dat is opgenomen voor de gebeurtenis. Een handeling kan een van de volgende handelingen zijn: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | De status van de actie. Een status kan een van de volgende zijn: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style=&quot;table-layout:auto&quot;}
