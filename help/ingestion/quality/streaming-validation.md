---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Validatie van gestreamde invoer
topic: overview
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Validatie van gestreamde invoer

Met streaming opname kunt u uw gegevens uploaden naar het Adobe Experience Platform met streaming eindpunten in real-time. API&#39;s voor streaming opname ondersteunen twee validatiemodi: synchroon en asynchroon.

## Aan de slag

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [XDM-systeem](../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
- [Streaming inname](../streaming-ingestion/overview.md): Een van de methoden waarmee gegevens naar het Experience Platform kunnen worden verzonden.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief die welke tot het schemaregister behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: `application/json`

### Validatiedekking

De streamingservice voor validatie omvat validatie op de volgende gebieden:
- Bereik
- Aanwezigheid
- Enum
- Patroon
- Type
- Indeling

## Synchrone validatie

Synchrone validatie is een validatiemethode die directe feedback geeft over de oorzaak van een mislukte opname. Nochtans, op mislukking, worden de verslagen die bevestiging ontbreken gelaten vallen en verhinderd om stroomafwaarts worden verzonden. Dit betekent dat synchrone validatie alleen tijdens het ontwikkelingsproces moet worden gebruikt. Wanneer het doen van synchrone bevestiging, worden de bezoekers geïnformeerd over zowel het resultaat van de bevestiging XDM, als, als het ontbrak, de reden voor mislukking.

Synchrone validatie is standaard niet ingeschakeld. Om het toe te laten, moet u in de facultatieve vraagparameter overgaan `synchronousValidation=true` wanneer het maken van API vraag. Bovendien is de synchrone bevestiging momenteel slechts beschikbaar als uw stroomeindpunt op het VA7 gegevenscentrum is.

Als een bericht tijdens synchrone bevestiging ontbreekt, zal het bericht niet aan de outputrij worden geschreven, die directe terugkoppelt voor gebruikers verstrekt.

**API-indeling**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` waarde van de eerder gemaakte streamingverbinding. |

**Verzoek**

Verzend de volgende aanvraag voor het invoeren van gegevens naar de gegevensinlaat met synchrone validatie:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | De JSON-tekst van gegevens die u wilt innemen. |

**Antwoord**

Als synchrone validatie is ingeschakeld, bevat een geslaagde reactie eventuele validatiefouten in de payload:

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

De bovenstaande reactie geeft aan hoeveel schemaovertredingen zijn gevonden en wat de overtredingen zijn. In deze reactie staat bijvoorbeeld dat de toetsen `workEmail` en `person` niet in het schema zijn gedefinieerd en daarom niet zijn toegestaan. De waarde voor wordt ook gemarkeerd als `_id` onjuist, omdat het schema een `string`verwacht, maar in plaats daarvan `long` is een ingevoegd. Wanneer vijf fouten zijn aangetroffen, wordt de verwerking van dat bericht door de validatieservice **gestopt** . Andere berichten blijven echter geparseerd.

## Asynchrone validatie

Asynchrone validatie is een validatiemethode die geen directe feedback biedt. In plaats daarvan, worden de gegevens verzonden naar een ontbroken partij in het meer van Gegevens om gegevensverlies te verhinderen. Deze mislukte gegevens kunnen later worden opgehaald voor verdere analyse en replay. Deze methode moet bij de productie worden gebruikt. Tenzij anders gevraagd, werkt streaming opname in asynchrone validatiemodus.

**API-indeling**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De `id` waarde van de eerder gemaakte streamingverbinding. |

**Verzoek**

Verzend de volgende aanvraag voor het invoeren van gegevens naar de gegevensinlaat met asynchrone validatie:

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | De JSON-tekst van gegevens die u wilt innemen. |

>[!NOTE] Er is geen extra queryparameter vereist, omdat asynchrone validatie standaard is ingeschakeld.

**Antwoord**

Als asynchrone validatie is ingeschakeld, retourneert een geslaagde reactie het volgende:

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

Let op: in het antwoord staat dat synchrone validatie is overgeslagen, omdat dit niet expliciet is gevraagd.

## Aanhangsel

Deze sectie bevat informatie over wat de verschillende statuscodes voor reacties voor het opnemen van gegevens betekenen.

### Statuscodes

| Statuscode | Wat het betekent |
| ----------- | ------------- |
| 200 | Geslaagd. Voor synchrone validatie betekent dit dat de validatiecontroles zijn geslaagd. Voor asynchrone validatie betekent dit dat alleen het bericht is ontvangen. De gebruikers kunnen de uiteindelijke berichtstatus door de dataset te observeren te weten komen. |
| 400 | Fout. Er is iets mis met uw verzoek. Er wordt een foutbericht met meer informatie ontvangen van de Streaming Validation Services. |
| 401 | Fout. Uw verzoek is niet geautoriseerd. U moet een aanvraag indienen met een token voor toonder. Voor meer informatie over het aanvragen van toegang raadpleegt u deze [zelfstudie](../../tutorials/authentication.md) of dit [blogbericht](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Fout. Er is een interne systeemfout opgetreden. |
| 501 | Fout. Dit betekent dat synchrone validatie **niet** wordt ondersteund voor deze locatie. |
| 503 | Fout. De service is momenteel niet beschikbaar. Clients moeten ten minste drie keer een exponentiële back-offstrategie gebruiken. |