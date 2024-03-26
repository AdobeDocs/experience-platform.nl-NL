---
title: API-eindpunt gegevensset vervaldatum
description: Het /ttl eindpunt in de Hygiene API van Gegevens staat u toe om datasettermijnen in Adobe Experience Platform programmatically te plannen.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 04d49282d60b2e886a6d2dae281b98b60e6ce9b3
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 0%

---

# Eindpunt gegevensset

De `/ttl` Het eindpunt in de Hygiene API van Gegevens staat u toe om vervaldata voor datasets in Adobe Experience Platform te plannen.

Een gegevenssetvervaldatum is slechts een getimed-vertraagde schrappingsverrichting. De gegevensset is in de tussentijd niet beschermd en kan dus op een andere manier worden verwijderd voordat de gegevensset vervalt.

>[!NOTE]
>
>Hoewel de vervaldatum als een specifiek tijdstip wordt gespecificeerd, kan er tot 24 uur vertraging na het verstrijken van de vervaldatum zijn voordat de eigenlijke verwijdering wordt gestart. Zodra schrapping in werking wordt gesteld, kan het tot zeven dagen duren alvorens alle sporen van de dataset uit de systemen van het Platform zijn verwijderd.

Op elk ogenblik alvorens dataset-schrapping eigenlijk in werking wordt gesteld, kunt u het verlopen annuleren of zijn trekkertijd wijzigen. Na het annuleren van een datasetvervaldatum, kunt u het opnieuw openen door een nieuwe vervaldatum te plaatsen.

Zodra de datasetschrapping in werking wordt gesteld, zal zijn vervalsingstaak worden gemerkt zoals `executing`en mag niet verder worden gewijzigd. De gegevensset zelf kan maximaal zeven dagen worden hersteld, maar alleen via een handmatig proces dat via een Adobe-serviceaanvraag wordt geïnitieerd. Aangezien het verzoek uitvoert, beginnen de gegevens meer, de Dienst van de Identiteit, en het Profiel van de Klant in real time afzonderlijke processen om de inhoud van de dataset uit hun respectieve diensten te verwijderen. Zodra de gegevens van alle drie de diensten worden geschrapt, wordt de vervaldatum duidelijk zoals `executed`.

>[!WARNING]
>
>Als een dataset wordt geplaatst om te verlopen, moet u om het even welke gegevensstromen manueel veranderen die gegevens in die dataset kunnen opnemen zodat uw stroomafwaartse werkschema&#39;s niet negatief worden beïnvloed.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Controleer voordat je doorgaat de [API-handleiding](./overview.md) voor informatie over vereiste kopballen voor verrichtingen CRUD, foutenmeldingen, de inzamelingen van Postman, en hoe te om steekproefAPI vraag te lezen.

>[!IMPORTANT]
>
>Wanneer het maken van vraag aan de gegevens Hygiene API, moet u - H gebruiken `x-sandbox-name: {SANDBOX_NAME}` header.

## Verlopen gegevensset weergeven {#list}

U kunt van alle datasettermijnen voor uw organisatie een lijst maken door een verzoek van de GET te doen. De parameters van de vraag kunnen worden gebruikt om de reactie voor aangewezen resultaten te filtreren.

**API-indeling**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETERS}` | Een lijst met optionele queryparameters, met meerdere parameters gescheiden door `&` tekens. Algemene parameters zijn `limit` en `page` voor pagineringsdoeleinden. Raadpleeg voor een volledige lijst met ondersteunde queryparameters de [aanhangsel](#query-params). |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie maakt een lijst van de resulterende datasetvervaldata. Het volgende voorbeeld is afgekapt voor ruimte.

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `totalRecords` | De telling van gegevenssetvervaltermijnen die de parameters van de lijstvraag aanstemden. |
| `ttlDetails` | Bevat de details van de teruggekeerde datasettermijnen. Voor meer details over de eigenschappen van een datasetafloop, zie de reactiesectie voor het maken van a [opzoekvraag](#lookup). |

{style="table-layout:auto"}

## Een gegevensset opzoeken die vervalt {#lookup}

Als u een gegevenssetvervaldatum wilt opzoeken, vraagt u een GET met een van de `datasetId` of de `ttlId`.

**API-indeling**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De id van de gegevensset waarvan u de vervaldatum wilt opzoeken. |
| `{TTL_ID}` | De id van de vervaldatum van de gegevensset. |

{style="table-layout:auto"}

**Verzoek**

Het volgende verzoek kijkt omhoog de vervaldetails voor dataset `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de datasetvervaldatum terug.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `ttlId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
| `datasetName` | De vertoningsnaam voor de dataset is deze vervaldatum van toepassing op. |
| `sandboxName` | De naam van de sandbox waarin de doelgegevensset zich bevindt. |
| `imsOrg` | De id van uw organisatie. |
| `status` | De huidige status van de gegevenssetvervaldatum. |
| `expiry` | De geplande datum en tijd waarop de dataset zal worden geschrapt. |
| `updatedAt` | Een tijdstempel van wanneer de vervaldatum voor het laatst is bijgewerkt. |
| `updatedBy` | De gebruiker die de vervaldatum voor het laatst heeft bijgewerkt. |
| `displayName` | De weergavenaam voor de vervalaanvraag. |
| `description` | Een beschrijving van de vervalaanvraag. |

{style="table-layout:auto"}

### Vervaltags voor catalogi

Wanneer u de opdracht [Catalogus-API](../../catalog/api/getting-started.md) om datasetdetails op te zoeken, als de dataset een actieve afloop heeft zal het onder worden vermeld `tags.adobe/hygiene/ttl`.

De volgende JSON vertegenwoordigt een afgekapte reactie voor de details van een dataset van Catalog, die een vervalwaarde van `32503680000000`. De waarde van de tag codeert de vervaldatum als een geheel getal in milliseconden sinds het begin van het Unix-tijdperk.

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## Een gegevensset maken die vervalt {#create}

Om ervoor te zorgen dat gegevens na een bepaalde periode uit het systeem worden verwijderd, plant u een vervaldatum voor een specifieke dataset door de gegevensset-id en de vervaldatum en -tijd op te geven in ISO 8601-indeling.

Om een datasetvervaldatum tot stand te brengen, voer een verzoek van de POST uit zoals hieronder getoond en verstrek de hieronder vermelde waarden binnen de nuttige lading.

**API-indeling**

```http
POST /ttl
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| Eigenschap | Beschrijving |
| --- | --- |
| `datasetId` | **Vereist** Identiteitskaart van de doeldataset die u een vervaldatum wilt plannen. |
| `expiry` | **Vereist** Een datum en tijd in ISO 8601-indeling. Als de tekenreeks geen expliciete tijdzoneverschuiving heeft, wordt aangenomen dat de tijdzone UTC is. De levensduur van de gegevens binnen het systeem wordt ingesteld op basis van de opgegeven vervalwaarde.<br>Opmerking:<ul><li>Het verzoek zal ontbreken als een datasetvervaldatum reeds voor de dataset bestaat.</li><li>Deze datum en tijd moeten ten minste **24 uur in de toekomst**.</li></ul> |
| `displayName` | Een facultatieve vertoningsnaam voor het verzoek van de datasetvervaldatum. |
| `description` | Een optionele beschrijving voor de vervalaanvraag. |

**Antwoord**

Een succesvolle reactie keert een (Gecreeerde) status van HTTP 201 en de nieuwe staat van de datasetvervaldatum terug, als er geen reeds bestaande datasetvervaldatum was.

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `ttlId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
| `datasetName` | De vertoningsnaam voor de dataset is deze vervaldatum van toepassing op. |
| `sandboxName` | De naam van de sandbox waarin de doelgegevensset zich bevindt. |
| `imsOrg` | De id van uw organisatie. |
| `status` | De huidige status van de gegevenssetvervaldatum. |
| `expiry` | De geplande datum en tijd waarop de dataset zal worden geschrapt. |
| `updatedAt` | Een tijdstempel van wanneer de vervaldatum voor het laatst is bijgewerkt. |
| `updatedBy` | De gebruiker die de vervaldatum voor het laatst heeft bijgewerkt. |
| `displayName` | Een weergavenaam voor de vervalaanvraag. |
| `description` | Een beschrijving voor de vervalaanvraag. |

De HTTP-status 400 (Onjuist verzoek) treedt op als er al een gegevenssetvervaldatum bestaat voor de gegevensset. Een mislukte reactie keert een 404 (niet Gevonden) status van HTTP terug als geen dergelijke datasetvervaldatum bestaat (of u hebt geen toegang tot het).

## Vervaldatum gegevensset bijwerken {#update}

Om een vervaldatum voor een dataset bij te werken, gebruik een verzoek van de PUT en `ttlId`. U kunt de `displayName`, `description`, en/of `expiry` informatie.

>[!NOTE]
>
>Als u de vervaldatum en -tijd wijzigt, moet deze in de toekomst minstens 24 uur duren. Deze gedwongen vertraging biedt u de mogelijkheid om de vervaldatum te annuleren of opnieuw te plannen en elk onbedoeld verlies van gegevens te voorkomen.

**API-indeling**

```http
PUT /ttl/{TTL_ID}
```

<!-- We should be avoiding usage of TTL, Can I change that to {EXPIRY_ID} or {EXPIRATION_ID} instead? -->

| Parameter | Beschrijving |
| --- | --- |
| `{TTL_ID}` | Identiteitskaart van de datasetvervaldatum die u wilt veranderen. |

**Verzoek**

Het volgende verzoek herplannt een datasetvervaldatum `SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` eind 2024 (Greenwich Mean Time). Als de bestaande gegevenssetvervaldatum wordt gevonden, wordt die vervaldatum bijgewerkt met nieuwe `expiry` waarde.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `expiry` | **Vereist** Een datum en tijd in ISO 8601-indeling. Als de tekenreeks geen expliciete tijdzoneverschuiving heeft, wordt aangenomen dat de tijdzone UTC is. De levensduur van de gegevens binnen het systeem wordt ingesteld op basis van de opgegeven vervalwaarde. Om het even welke vorige verlooptimestamp voor de zelfde dataset wordt vervangen door de nieuwe vervalwaarde u hebt verstrekt. Deze datum en tijd moeten ten minste **24 uur in de toekomst**. |
| `displayName` | Een weergavenaam voor de vervalaanvraag. |
| `description` | Een optionele beschrijving voor de vervalaanvraag. |

{style="table-layout:auto"}

**Antwoord**

Een succesvolle reactie keert de nieuwe staat van de datasetvervalsing en een status 200 van HTTP terug (O.K.) als een reeds bestaande vervaldatum werd bijgewerkt.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `ttlId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
| `imsOrg` | De id van uw organisatie. |
| `status` | De huidige status van de gegevenssetvervaldatum. |
| `expiry` | De geplande datum en tijd waarop de dataset zal worden geschrapt. |
| `updatedAt` | Een tijdstempel van wanneer de vervaldatum voor het laatst is bijgewerkt. |
| `updatedBy` | De gebruiker die de vervaldatum voor het laatst heeft bijgewerkt. |

{style="table-layout:auto"}

Een mislukte reactie retourneert een HTTP-status van 404 (Niet gevonden) als een dergelijke vervaldatum van de gegevensset niet bestaat.

## Vervaldatum gegevensset annuleren {#delete}

U kunt een gegevenssetvervaldatum annuleren door een verzoek van de DELETE te doen.

>[!NOTE]
>
>Alleen gegevenssetvervaldatums met de status `pending` kan worden geannuleerd. Wanneer wordt geprobeerd een vervaldatum te annuleren die is uitgevoerd of al is geannuleerd, wordt een HTTP 404-fout geretourneerd.

**API-indeling**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{EXPIRATION_ID}` | De `ttlId` van de gegevenssetvervaldatum die u wilt annuleren. |

{style="table-layout:auto"}

**Verzoek**

Het volgende verzoek annuleert een gegevenssetvervaldatum met identiteitskaart `SD-b16c8b48-a15a-45c8-9215-587ea89369bf`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en de vervaldatums `status` kenmerk is ingesteld op `cancelled`.

## Haal de geschiedenis van de vervalstatus van een dataset terug {#retrieve-expiration-history}

U kunt de geschiedenis van de vervalstatus van een specifieke dataset opzoeken door de vraagparameter te gebruiken `include=history` in een opzoekverzoek. Het resultaat omvat informatie over de verwezenlijking van de dataset vervaldatum, om het even welke updates die zijn toegepast, en zijn annulering of uitvoering (indien van toepassing). U kunt ook de opdracht `ttlId` van het verstrijken van de gegevensset.

**API-indeling**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{TTL_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | Identiteitskaart van de dataset de waarvan vervalgeschiedenis u omhoog wilt zoeken. |
| `{TTL_ID}` | De id van de vervaldatum van de gegevensset. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de datasetvervaldatum, met terug `history` array met de details `status`, `expiry`, `updatedAt`, en `updatedBy` kenmerken voor elk van de opgenomen updates.

```json
{
  "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `ttlId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
| `datasetName` | De vertoningsnaam voor de dataset is deze vervaldatum van toepassing op. |
| `sandboxName` | De naam van de sandbox waarin de doelgegevensset zich bevindt. |
| `displayName` | De weergavenaam voor de vervalaanvraag. |
| `description` | Een beschrijving van de vervalaanvraag. |
| `imsOrg` | De id van uw organisatie. |
| `history` | Hiermee wordt de geschiedenis van updates voor de vervaldatum weergegeven als een array van objecten, waarbij elk object het `status`, `expiry`, `updatedAt`, en `updatedBy` kenmerken voor de vervaldatum op het moment van de update. |

{style="table-layout:auto"}

## Bijlage

### Geaccepteerde queryparameters {#query-params}

De volgende tabel geeft een overzicht van de beschikbare queryparameters wanneer [gegevensset met gegevenslijsten verlopen](#list):

>[!NOTE]
>
>De `description`, `displayName`, en `datasetName` parameters bevatten allemaal de mogelijkheid om te zoeken op basis van LIKE-waarden. Dit betekent dat u geplande gegevenssetvervaldatums genoemd kunt vinden: &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; door naar het koord &quot;Name1&quot;te zoeken.

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `author` | Komt overeen met verlopen waarvan `created_by` is een overeenkomst voor de zoekreeks. Als de zoektekenreeks begint met `LIKE` of `NOT LIKE`, de rest wordt behandeld als een SQL-zoekpatroon. Anders wordt de gehele zoektekenreeks beschouwd als een letterlijke tekenreeks die exact moet overeenkomen met de volledige inhoud van een tekenreeks `created_by` veld. | `author=LIKE %john%`, `author=John Q. Public` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Komt overeen met verlopen die op elk moment in het aangegeven interval zijn geannuleerd. Dit geldt ook als de vervaldatum later opnieuw is geopend (door een nieuwe vervaldatum in te stellen voor dezelfde gegevensset). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Komt overeen met verlopen die tijdens het opgegeven interval zijn voltooid. | `completedToDate=2021-11-11-06:00` |
| `createdDate` | Komt overeen met verlopen die in het venster van 24 uur zijn gemaakt, te beginnen bij het opgegeven tijdstip.<br><br>Datums zonder tijd (zoals `2021-12-07`) staat voor de datetime aan het begin van die dag. Daarom `createdDate=2021-12-07` verwijst naar elke vervaldatum die op 7 december 2021 is gemaakt, vanaf `00:00:00` doorheen `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Komt overeen met verlopen die op of na de aangegeven tijd zijn gemaakt. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Komt overeen met verlopen die op of voor de aangegeven tijd zijn gemaakt. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `datasetId` | Komt overeen met verlopen die van toepassing zijn op specifieke dataset. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Komt overeen met verlopen waarvan de naam van de gegevensset de opgegeven zoekreeks bevat. De overeenkomst is niet hoofdlettergevoelig. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Komt overeen met verlopen waarvan de weergavenaam de opgegeven zoekreeks bevat. De overeenkomst is niet hoofdlettergevoelig. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Hiermee filtert u de resultaten op basis van een exacte uitvoeringsdatum, een einddatum voor de uitvoering of een begindatum voor de uitvoering. Zij worden gebruikt om gegevens of verslagen terug te winnen verbonden aan de uitvoering van een verrichting op een specifieke datum, vóór een bepaalde datum, of na een bepaalde datum. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Komt overeen met vervaldata die moeten worden uitgevoerd, of reeds zijn uitgevoerd, tijdens het opgegeven interval. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Een geheel getal in het bereik van 1 tot en met 100 dat het maximale aantal retourneringen aangeeft. De standaardwaarde is 25. | `limit=50` |
| `orderBy` | De `orderBy` queryparameter geeft de sorteervolgorde aan van de resultaten die door de API worden geretourneerd. Gebruik dit schema om de gegevens te rangschikken op basis van een of meer velden, in oplopende (ASC) of aflopende (DESC) volgorde. Gebruik + of - prefix om ASC, DESC respectievelijk te betekenen. De volgende waarden worden geaccepteerd: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status`. | `-datasetName` |
| `orgId` | Komt datasets vervaldagen met de organisatie ID aan die van de parameter. Deze waarde is standaard ingesteld op de waarde van `x-gw-ims-org-id` kopballen, en wordt genegeerd tenzij het verzoek een de dienstteken levert. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Een geheel getal dat aangeeft welke pagina met verlopen moet worden geretourneerd. | `page=3` |
| `sandboxName` | Komt overeen met de vervaldatum van de gegevensset waarvan de naam van de sandbox precies overeenkomt met het argument. Wordt standaard ingesteld op de naam van de sandbox in de aanvraag `x-sandbox-name` header. Gebruiken `sandboxName=*` om gegevenssetvervaldatums uit alle sandboxen op te nemen. | `sandboxName=dev1` |
| `search` | Komt overeen met verlopen waarbij de opgegeven tekenreeks exact overeenkomt met de vervaldatum-id of **bevatten** op een van deze gebieden:<br><ul><li>auteur</li><li>weergavenaam</li><li>beschrijving</li><li>weergavenaam</li><li>naam gegevensset</li></ul> | `search=TESTING` |
| `status` | Een door komma&#39;s gescheiden lijst met statussen. Wanneer inbegrepen, past de reactie datasettermijnen aan de waarvan huidige status onder die vermeld is. | `status=pending,cancelled` |
| `ttlId` | Komt overeen met het vervalverzoek met de opgegeven id. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | leuk `createdDate` / `createdFromDate` / `createdToDate`, maar komt overeen met de updatetijd van een gegevensset die vervalt in plaats van de aanmaaktijd.<br><br>Een vervaldatum wordt beschouwd als bijgewerkt op elke bewerking, ook wanneer deze wordt gemaakt, geannuleerd of uitgevoerd. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

