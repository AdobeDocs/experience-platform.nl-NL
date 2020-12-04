---
keywords: Experience Platform;home;popular topics;authenticated streaming connection;streaming connection;create streaming connection;create authenticated streaming connection;streaming ingestion;ingestion;
solution: Experience Platform
title: Een geverifieerde streamingverbinding maken
topic: tutorial
type: Tutorial
description: De voor authentiek verklaarde Inzameling van Gegevens staat de diensten van Adobe Experience Platform, zoals het Profiel van de Klant In real time en Identiteit, toe om tussen verslagen te onderscheiden die uit vertrouwde op bronnen en onbetrouwbare bronnen komen.
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Een geverifieerde streamingverbinding maken

De voor authentiek verklaarde Inzameling van Gegevens staat de diensten van Adobe Experience Platform, zoals [!DNL Real-time Customer Profile] en [!DNL Identity], toe om tussen verslagen te onderscheiden die uit vertrouwde op bronnen en onbetrouwbare bronnen komen. De cliënten die Persoonlijk Identificeerbare Informatie (PII) willen verzenden kunnen dit doen door toegangstokens als deel van het verzoek van de POST te verzenden.

## Aan de slag

Registratie voor streamingverbindingen is vereist om te beginnen met het streamen van gegevens naar Adobe Experience Platform. Wanneer u een streamingverbinding registreert, moet u enkele belangrijke details opgeven, zoals de bron van streaminggegevens.

Na het registreren van een het stromen verbinding, zult u, als gegevensproducent, een unieke URL hebben die kan worden gebruikt om gegevens te stromen aan [!DNL Platform].

Deze zelfstudie vereist ook een praktische kennis van verschillende Adobe Experience Platform-services. Voordat u met deze zelfstudie begint, raadpleegt u de documentatie voor de volgende services:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader voor het [!DNL Platform] organiseren van ervaringsgegevens.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan het stromen ingestie APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie de documentatie over het [!DNL Platform]sandboxoverzicht voor meer informatie over sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Verbinding maken

Een verbinding geeft de bron op en bevat de informatie die nodig is om de stroom compatibel te maken met API&#39;s voor streaming invoer.

**API-indeling**

```http
POST /flowservice/connections
```

**Verzoek**

>[!NOTE]
>
>De waarden voor de lijst `providerId` en de lijst `connectionSpec` moeten **** worden gebruikt zoals in het voorbeeld wordt getoond, aangezien zij aan API zijn die u een het stromen verbinding voor het stromen opname creeert.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```

**Antwoord**

Een geslaagde reactie retourneert HTTP status 201 met details van de nieuwe verbinding.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van de nieuwe verbinding. Dit wordt hierna `{CONNECTION_ID}`genoemd. |
| `etag` | Een id die is toegewezen aan de verbinding en die de revisie van de verbinding opgeeft. |

## URL gegevensverzameling ophalen

Met de gemaakte verbinding kunt u nu de URL van uw gegevensverzameling ophalen.

**API-indeling**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` waarde van de verbinding u eerder creeerde. |

**Verzoek**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gevraagde verbinding terug. De URL van de gegevensverzameling wordt automatisch gemaakt met de verbinding en kan worden opgehaald met de `inletUrl` waarde.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Volgende stappen

Nu u een geverifieerde streamingverbinding hebt gemaakt, kunt u tijdreeksen of recordgegevens streamen, zodat u gegevens kunt invoeren binnen [!DNL Platform]. Als u wilt leren hoe u tijdreeksgegevens kunt streamen, gaat u naar de zelfstudie over [!DNL Platform]streaming tijdreeksgegevens [](./streaming-time-series-data.md). Als u wilt leren hoe u recordgegevens kunt streamen, gaat u naar de zelfstudie voor [!DNL Platform]streaming recordgegevens [](./streaming-record-data.md).

## Aanhangsel

Deze sectie bevat aanvullende informatie over geverifieerde streamingverbindingen.

### Berichten verzenden naar een geverifieerde streamingverbinding

Als verificatie is ingeschakeld voor een streamingverbinding, moet de client de `Authorization` header aan hun aanvraag toevoegen.

Als de `Authorization` header niet aanwezig is of als een ongeldig/verlopen toegangstoken wordt verzonden, wordt een HTTP 401 Unauthorised-reactie geretourneerd, met een vergelijkbare reactie als hieronder:

**Antwoord**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
