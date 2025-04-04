---
keywords: Experience Platform;home;populaire onderwerpen;ophalen mislukte batches;mislukte batches;batch-opname;Batch-opname;Mislukte batches;Get failed batches;get failed batches;Download failed batches;download mislukte batches; download mislukte batches;
solution: Experience Platform
title: Mislukte batches ophalen met de API voor gegevenstoegang
type: Tutorial
description: Deze zelfstudie behandelt stappen voor het ophalen van informatie over een mislukte batch met gebruik van API's voor gegevensinname.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# Mislukte batches ophalen met de API voor gegevenstoegang

Adobe Experience Platform biedt twee methoden voor het uploaden en opnemen van gegevens. U kunt batch-opname gebruiken, waarmee u de gegevens kunt invoegen met verschillende bestandstypen (zoals CSV&#39;s), of streaming opname, waardoor u de gegevens in [!DNL Experience Platform] kunt invoegen met streaming eindpunten in real-time.

Deze zelfstudie behandelt stappen voor het ophalen van informatie over een mislukte batch met behulp van [!DNL Data Ingestion] API&#39;s.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
- [[!DNL Data Ingestion]](../home.md): de methoden waarmee gegevens naar [!DNL Experience Platform] kunnen worden verzonden.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot de [!DNL Schema Registry] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- `Content-Type: application/json`

### Sample failed batch

Dit leerprogramma zal steekproefgegevens met verkeerd geformatteerde timestamp gebruiken die de waarde van de maand om **00** plaatst te zijn, zoals hieronder gezien:

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

**API formaat**

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

**Reactie**

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

Met het bovenstaande antwoord kunt u zien welke delen van de batch zijn uitgevoerd en mislukt. Uit dit antwoord kunt u zien dat het bestand `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` de mislukte batch bevat.

## De mislukte batch downloaden

Als u weet welk bestand in de batch is mislukt, kunt u het mislukte bestand downloaden en zien wat de foutmelding is.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

Na het lezen van deze zelfstudie hebt u geleerd hoe u fouten kunt ophalen uit mislukte batches. Voor meer informatie over partijingestie, te lezen gelieve de [ gids van de partijontwikkelaar ](../batch-ingestion/overview.md). Voor meer informatie over het stromen opname, te lezen gelieve [ creërend een het stromen verbindingsleerprogramma ](../tutorials/create-streaming-connection.md).

## Bijlage

Deze sectie bevat informatie over andere typen innamefouten die kunnen optreden.

### Onjuist opgemaakte XDM

Net als de tijdstempelfout in de vorige voorbeeldstroom zijn deze fouten het gevolg van onjuist opgemaakte XDM. Deze foutberichten variëren, afhankelijk van de aard van het probleem. Er kan dan ook geen specifiek foutvoorbeeld worden weergegeven.

### Ontbrekende of ongeldige organisatie-id

Deze fout wordt weergegeven als de organisatie-id ontbreekt in de payload.

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

Deze fout wordt weergegeven als de lus `schemaRef` for the `xdmMeta` ontbreekt.

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

Deze fout wordt weergegeven als de `source` in de koptekst zijn `name` niet bevat.

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

Deze fout wordt weergegeven als er geen `xdmEntity` aanwezig is.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
