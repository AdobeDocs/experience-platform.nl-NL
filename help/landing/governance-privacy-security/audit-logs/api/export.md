---
title: Audit events export API Endpoint
description: Leer hoe u auditgebeurtenissen in Experience Platform exporteert met de API voor auditquery.
role: Developer
feature: Audits, API
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: d4edaf61030b341cbef9d5ebe5502ed649dffcd6
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Een lijst met auditgebeurtenissen exporteren

U kunt gebeurtenisgegevens ophalen door een GET-aanvraag in te dienen bij het `/audit/export` -eindpunt en de gebeurtenissen op te geven die u in de payload wilt ophalen.

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
| `assetType` | Het type Experience Platform-resource waarop de handeling is uitgevoerd. <br/> Voorbeeld: `?property=assetType==<an asset type>`. |

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/export
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**Reactie**

De resultaten worden gegenereerd in een CSV-bestand voor export, waarbij elke vermelding een kerngebeurtenis of een verbeterde auditgebeurtenis vertegenwoordigt. Een geslaagde reactie retourneert HTTP 307 zonder responstekst. In de antwoordheader van `Location` wordt een koppeling naar het exportbestand weergegeven.
