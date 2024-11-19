---
title: Audit events export API Endpoint
description: Leer hoe u auditgebeurtenissen in Experience Platform exporteert met de API voor auditquery.
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Een lijst met auditgebeurtenissen exporteren

U kunt gebeurtenisgegevens terugwinnen door een verzoek van de GET tot het `/audit/export` eindpunt te richten, specificerend de gebeurtenissen u in de nuttige lading wenst terug te winnen.

**API formaat**

```http
GET /audit/export
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `timestamp` | Wanneer u filtert met een tijdstempel, kunt u het beste een bereik gebruiken met de operatoren > en &lt; in plaats van een exacte waarde. <br/> Voorbeeld: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | De status van de actie. Een status kan een van de volgende zijn: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/> Voorbeeld: `?property=status==Deny`. |
| `action` | Het type actie dat is opgenomen voor de gebeurtenis. Een handeling kan een van de volgende handelingen zijn: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> Voorbeeld: `?property=action==Create` . |
| `user` | De gebruiker die de gebeurtenis heeft uitgevoerd. |
| `assetType` | Het type van middel van het Platform dat de actie werd uitgevoerd. <br/> Voorbeeld: `?property=assetType==<an asset type>`. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Reactie**

De resultaten worden gegenereerd in een CSV-bestand voor export. Een geslaagde reactie retourneert HTTP 307 zonder responstekst. In de antwoordheader van `Location` wordt een koppeling naar het exportbestand weergegeven.
