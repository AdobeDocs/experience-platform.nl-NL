---
keywords: Experience Platform;home;populaire onderwerpen;streamingverbinding;maak streamingverbinding;api-hulplijn;zelfstudie;maak een streamingverbinding;streaming opname;opname;
solution: Experience Platform
title: Een streamingverbinding maken met de API
topic: zelfstudie
type: Zelfstudie
description: Deze zelfstudie helpt u bij het gebruik van streaming opname-API's, die onderdeel zijn van de API's van de Adobe Experience Platform Data Ingestie Service.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 1%

---


# Een streamingverbinding maken met de API

De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om door de stappen te lopen om een streamingverbinding te maken met behulp van de Flow Service API.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Het gestandaardiseerde kader voor het  [!DNL Platform] organiseren van ervaringsgegevens.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, consumentenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan het stromen ingestie APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../../../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Verbinding maken

Een verbinding geeft de bron op en bevat de informatie die nodig is om de stroom compatibel te maken met API&#39;s voor streaming invoer. Wanneer u een verbinding maakt, kunt u een niet-geverifieerde en een geverifieerde verbinding maken.

### Niet-geverifieerde verbinding

Niet-geverifieerde verbindingen zijn de standaardstreamingverbindingen die u kunt maken wanneer u gegevens wilt streamen naar het Platform.

**API-indeling**

```http
POST /flowservice/connections
```

**Verzoek**

Als u een streamingverbinding wilt maken, moet u de provider-id en de verbindingsspecificatie-id opgeven als onderdeel van het verzoek om POST. De provider-id is `521eee4d-8cbe-4906-bb48-fb6bd4450033` en de verbindingsspecificatie-id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
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
             "name": "Sample connection"
         }
     }
 }
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sourceId` | De id van de streamingverbinding die u wilt maken. |
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Deze waarde moet `xdm` zijn. |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |
| `connectionSpec.id` | De verbindingsspecificatie `id` voor het stromen verbindingen. |

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van de nieuwe verbinding. Dit wordt hierna `{CONNECTION_ID}` genoemd. |
| `etag` | Een id die is toegewezen aan de verbinding en die de revisie van de verbinding opgeeft. |

### Geverifieerde verbinding

De voor authentiek verklaarde verbindingen zouden moeten worden gebruikt wanneer u tussen verslagen moet onderscheiden die uit vertrouwde op en niet-vertrouwde op bronnen komen. Gebruikers die gegevens met PII (Personeel Identified Information) willen verzenden, moeten een geverifieerde verbinding maken bij het streamen van gegevens naar het Platform.

**API-indeling**

```http
POST /flowservice/connections
```

**Verzoek**

Als u een streamingverbinding wilt maken, moet u de provider-id en de verbindingsspecificatie-id opgeven als onderdeel van het verzoek om POST. De provider-id is `521eee4d-8cbe-4906-bb48-fb6bd4450033` en de verbindingsspecificatie-id is `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
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


| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sourceId` | De id van de streamingverbinding die u wilt maken. |
| `auth.params.dataType` | Het gegevenstype voor de streamingverbinding. Deze waarde moet `xdm` zijn. |
| `auth.params.name` | De naam van de streamingverbinding die u wilt maken. |
| `auth.params.authenticationRequired` | De parameter die opgeeft dat de gemaakte streamingverbinding |
| `connectionSpec.id` | De verbindingsspecificatie `id` voor het stromen verbindingen. |

**Antwoord**

Een succesvolle reactie keert status 201 van HTTP met details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | De `id` van de nieuwe verbinding. Dit wordt hierna `{CONNECTION_ID}` genoemd. |
| `etag` | Een id die is toegewezen aan de verbinding en die de revisie van de verbinding opgeeft. |

## URL voor streamingeindpunt ophalen

Met de gemaakte verbinding kunt u nu de URL van het streamingeindpunt ophalen.

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

Een succesvolle reactie keert status 200 van HTTP met gedetailleerde informatie over de gevraagde verbinding terug. De URL van het streamingeindpunt wordt automatisch gemaakt met de verbinding en kan worden opgehaald met de waarde `inletUrl`.

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

Door deze zelfstudie te volgen, hebt u een het stromen verbinding van HTTP gecreeerd, toelatend u om het stromen eindpunt te gebruiken om gegevens in Platform in te voeren. Lees de [zelfstudie voor het maken van een streamingverbinding](../../../ui/create/streaming/http.md) voor instructies voor het maken van een streamingverbinding in de gebruikersinterface.

Lees de zelfstudie over [streamingtijdreeksgegevens](../../../../../ingestion/tutorials/streaming-time-series-data.md) of de zelfstudie over [streamingrecordgegevens](../../../../../ingestion/tutorials/streaming-record-data.md) voor meer informatie over het streamen van gegevens naar Platform.

## Aanhangsel

Deze sectie bevat aanvullende informatie over het maken van streamingverbindingen met de API.

### Berichten verzenden naar een geverifieerde streamingverbinding

Als verificatie is ingeschakeld voor een streamingverbinding, moet de client de `Authorization`-header aan hun aanvraag toevoegen.

Als de `Authorization` kopbal niet aanwezig is, of een ongeldig/verlopen toegangstoken wordt verzonden, zal een HTTP 401 Onbevoegde reactie worden teruggekeerd, met een gelijkaardige reactie zoals hieronder:

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
