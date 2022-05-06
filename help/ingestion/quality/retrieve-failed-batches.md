---
keywords: Experience Platform;home;populaire onderwerpen;ophalen mislukte batches;mislukte batches;batch-opname;Batch-opname;Mislukte batches;Get failed batches;get failed batches;Download failed batches;download mislukte batches; download mislukte batches;
solution: Experience Platform
title: Mislukte batches ophalen met de API voor gegevenstoegang
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie behandelt stappen voor het ophalen van informatie over een mislukte batch met gebruik van API's voor gegevensinname.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Mislukte batches ophalen met de API voor gegevenstoegang

Adobe Experience Platform biedt twee methoden voor het uploaden en opnemen van gegevens. U kunt batch-opname gebruiken, waardoor u de gegevens kunt invoegen met verschillende bestandstypen (zoals CSV&#39;s), of streaming opname, waardoor u de gegevens kunt invoegen op [!DNL Platform] het gebruiken van het stromen eindpunten in echt - tijd.

Deze zelfstudie behandelt stappen voor het ophalen van informatie over een mislukte batch met behulp van [!DNL Data Ingestion] API&#39;s.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
- [[!DNL Data Ingestion]](../home.md): De methoden waarmee gegevens kunnen worden verzonden naar [!DNL Experience Platform].

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke tot de [!DNL Schema Registry], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- `Content-Type: application/json`

### Sample failed batch

In deze zelfstudie worden voorbeeldgegevens gebruikt met een verkeerd opgemaakte tijdstempel die instelt dat de waarde van de maand moet worden ingesteld **00**, zoals hieronder weergegeven:

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

De bovenstaande payload wordt niet correct gevalideerd op basis van het XDM-schema vanwege de onjuiste tijdstempel.

## De mislukte batch ophalen

**API-indeling**

```http
GET /batches/{BATCH_ID}/failed
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch die je opzoekt. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

Met het bovenstaande antwoord kunt u zien welke delen van de batch zijn uitgevoerd en mislukt. In dit antwoord ziet u dat het bestand `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` bevat de mislukte batch.

## De mislukte batch downloaden

Als u weet welk bestand in de batch is mislukt, kunt u het mislukte bestand downloaden en zien wat de foutmelding is.

**API-indeling**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{BATCH_ID}` | De id van de batch die het mislukte bestand bevat. |
| `{FAILED_FILE}` | De naam van het bestand waarvoor de opmaak is mislukt. |

**Verzoek**

Met de volgende aanvraag kunt u het bestand downloaden met innamefouten.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Aangezien de vorige opgenomen batch een ongeldige datum-tijd had, wordt de volgende validatiefout weergegeven.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## Volgende stappen

Na het lezen van deze zelfstudie hebt u geleerd hoe u fouten kunt ophalen uit mislukte batches. Lees voor meer informatie over het gebruik van batch [handleiding voor het ontwikkelen van batch-inhoud](../batch-ingestion/overview.md). Lees voor meer informatie over streaming opname de [een zelfstudie over streamingverbindingen maken](../tutorials/create-streaming-connection.md).

## Aanhangsel

Deze sectie bevat informatie over andere typen innamefouten die kunnen optreden.

### Onjuist opgemaakte XDM

Net als de tijdstempelfout in de vorige voorbeeldstroom zijn deze fouten het gevolg van onjuist opgemaakte XDM. Deze foutberichten variëren, afhankelijk van de aard van het probleem. Er kan dan ook geen specifiek foutvoorbeeld worden weergegeven.

### Ontbrekende of ongeldige IMS-organisatie-id

Deze fout wordt weergegeven als de IMS-organisatie-id ontbreekt in de payload.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Ontbrekend XDM-schema

Deze fout wordt weergegeven als de `schemaRef` voor de `xdmMeta` ontbreekt.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Ontbrekende bronnaam

Deze fout wordt weergegeven als de `source` in de koptekst ontbreekt het `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### Ontbrekende XDM-entiteit

Deze fout wordt weergegeven als er geen `xdmEntity` aanwezig.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
