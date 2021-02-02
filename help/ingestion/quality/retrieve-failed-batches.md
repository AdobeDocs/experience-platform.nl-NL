---
keywords: Experience Platform;home;populaire onderwerpen;ophalen mislukte batches;mislukte batches;batch-opname;Batch-opname;Mislukte batches;Get failed batches;get failed batches;Download failed batches;download mislukte batches; download mislukte batches;
solution: Experience Platform
title: Ontbroken batches ophalen
topic: tutorial
type: Tutorial
description: Deze zelfstudie behandelt stappen voor het ophalen van informatie over een mislukte batch met gebruik van API's voor gegevensinname.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---


# Mislukte batches ophalen met de API

Adobe Experience Platform biedt twee methoden voor het uploaden en opnemen van gegevens. U kunt batch-opname gebruiken, waarmee u de gegevens kunt invoegen met verschillende bestandstypen (zoals CSV&#39;s) of streaming opname, waardoor u de gegevens in [!DNL Platform] kunt invoegen met streaming eindpunten in real-time.

Deze zelfstudie behandelt stappen voor het ophalen van informatie over een mislukte batch met behulp van [!DNL Data Ingestion] API&#39;s.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
- [[!DNL Data Ingestion]](../home.md): De methoden waarmee gegevens kunnen worden verzonden naar  [!DNL Experience Platform].

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Schema Registry] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: `application/json`

### Sample failed batch

Deze zelfstudie gebruikt voorbeeldgegevens met een verkeerd opgemaakte tijdstempel waarmee de waarde van de maand wordt ingesteld op **00**, zoals hieronder wordt weergegeven:

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
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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

Met het bovenstaande antwoord kunt u zien welke delen van de batch zijn uitgevoerd en mislukt. In dit antwoord ziet u dat het bestand `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` de mislukte batch bevat.

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

Met de volgende aanvraag kunt u het bestand downloaden dat innamefouten had.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Na het lezen van deze zelfstudie hebt u geleerd hoe u fouten kunt ophalen uit mislukte batches. Lees voor meer informatie over het in batch opnemen de [batch ingestion developer guide](../batch-ingestion/overview.md). Lees voor meer informatie over streamingopname de zelfstudie [voor het maken van een streamingverbinding](../tutorials/create-streaming-connection.md).

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
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Ontbrekend XDM-schema

Deze fout wordt getoond als `schemaRef` voor `xdmMeta` mist.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Ontbrekende bronnaam

Deze fout wordt getoond als `source` in de kopbal zijn `name` mist.

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

Deze fout wordt getoond als er geen `xdmEntity` aanwezig is.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
