---
title: Audit events export API Endpoint
description: Leer hoe u auditgebeurtenissen in Experience Platform exporteert met de API voor auditquery.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Een lijst met auditgebeurtenissen exporteren

U kunt gebeurtenisgegevens ophalen door een GET-aanvraag in te dienen bij de `/audit/export` eindpunt, die de gebeurtenissen specificeren u in de nuttige lading wenst terug te winnen.

**API-indeling**

```http
GET /audit/export
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `timestamp` | Wanneer u filtert met een tijdstempel, kunt u het beste een bereik gebruiken met de operatoren > en &lt; in plaats van een exacte waarde. <br/>Voorbeeld: ?property=timestamp&lt;2020-02-08T02:46:48.610862Z&amp;property=timestamp>2020-01-01T02:46:48,610862Z. |
| `status` | De status van de actie. Een status kan een van de volgende zijn: </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |
| `action` | Het type actie dat is opgenomen voor de gebeurtenis. Een handeling kan een van de volgende handelingen zijn: <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `user` | De gebruiker die de gebeurtenis heeft uitgevoerd. |
| `assetType` | Het type van middel van het Platform dat de actie werd uitgevoerd. |

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

**Antwoord**

De resultaten worden gegenereerd in een CSV-bestand voor export. Een geslaagde reactie retourneert HTTP 307 zonder responstekst. Een koppeling naar het exportbestand vindt u in het dialoogvenster `Location` responsheader.
