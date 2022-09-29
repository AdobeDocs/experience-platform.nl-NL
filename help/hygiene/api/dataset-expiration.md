---
title: API-eindpunt gegevensset vervaldatum
description: Het /ttl eindpunt in de Hygiene API van Gegevens staat u toe om datasettermijnen in Adobe Experience Platform programmatically te plannen.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: e4cc78591d0d3b4abd660956b1263092697d63d5
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Eindpunt gegevensset

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die een Adobe Healthcare Shield of Privacy Shield hebben aangeschaft.

De `/ttl` Het eindpunt in de Hygiene API van Gegevens staat u toe om vervaldata voor datasets in Adobe Experience Platform te plannen.

Een gegevenssetvervaldatum is slechts een getimed-vertraagde schrappingsverrichting. De gegevensset is in de tussentijd niet beschermd en kan dus op een andere manier worden verwijderd voordat de gegevensset vervalt.

>[!NOTE]
>
>Hoewel de vervaldatum als een specifiek tijdstip wordt gespecificeerd, kan er tot 24 uur vertraging na het verstrijken van de vervaldatum zijn voordat de eigenlijke verwijdering wordt gestart. Zodra de schrapping in werking wordt gesteld, kan het tot zeven dagen duren alvorens alle sporen van de dataset uit de systemen van de Platform zijn verwijderd.

Op elk ogenblik alvorens dataset-schrapping eigenlijk in werking wordt gesteld, kunt u het verlopen annuleren of zijn trekkertijd wijzigen. Na het annuleren van een datasetvervaldatum, kunt u het opnieuw openen door een nieuwe vervaldatum te plaatsen.

Zodra de datasetschrapping in werking wordt gesteld, zal zijn vervalsingstaak worden gemerkt zoals `executing`en mag niet worden gewijzigd. De gegevensset zelf kan maximaal zeven dagen worden hersteld, maar alleen via een handmatig proces dat via een Adobe-serviceaanvraag wordt geïnitieerd. Aangezien het verzoek uitvoert, beginnen de gegevens meer, de Dienst van de Identiteit, en het Profiel van de Klant in real time afzonderlijke processen om de inhoud van de dataset uit hun respectieve diensten te verwijderen. Zodra de gegevens van alle drie de diensten worden geschrapt, wordt de vervaldatum duidelijk zoals `executed`.

>[!WARNING]
>
>Als een dataset wordt geplaatst om te verlopen, moet u om het even welke gegevensstromen manueel veranderen die gegevens in die dataset kunnen opnemen zodat uw stroomafwaartse werkschema&#39;s niet negatief worden beïnvloed.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Controleer voordat je doorgaat de [overzicht](./overview.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Verlopen gegevensset weergeven {#list}

U kunt van alle datasettermijnen voor uw organisatie een lijst maken door een verzoek van de GET te doen.

**API-indeling**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETERS}` | Een lijst met optionele queryparameters, met meerdere parameters gescheiden door `&` tekens. Veelvoorkomende parameters zijn `size` en `page` voor pagineringsdoeleinden. Voor een volledige lijst van gesteunde vraagparameters, verwijs naar [aanhangsel](#query-params). |

{style=&quot;table-layout:auto&quot;}

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
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `totalRecords` | De telling van gegevenssetvervaltermijnen die de parameters van de lijstvraag aanstemden. |
| `ttlDetails` | Bevat de details van de teruggekeerde datasettermijnen. Voor meer details over de eigenschappen van een datasetafloop, zie de reactiesectie voor het maken van a [opzoekvraag](#lookup). |

{style=&quot;table-layout:auto&quot;}

## Een gegevensset opzoeken die vervalt {#lookup}

U kunt een datasetvervaldatum door een verzoek van de GET opzoeken.

**API-indeling**

```http
GET /ttl/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | De id van de gegevensset waarvan u de vervaldatum wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

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
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
| `imsOrg` | De id van uw organisatie. |
| `status` | De huidige status van de gegevenssetvervaldatum. |
| `expiry` | De geplande datum en tijd waarop de dataset zal worden geschrapt. |
| `updatedAt` | Een tijdstempel van wanneer de vervaldatum voor het laatst is bijgewerkt. |
| `updatedBy` | De gebruiker die de vervaldatum voor het laatst heeft bijgewerkt. |
| `displayName` | De weergavenaam voor de vervalaanvraag. |
| `description` | Een beschrijving van de vervalaanvraag. |

{style=&quot;table-layout:auto&quot;}

### Vervaltags voor catalogi

Wanneer u de [Catalogus-API](../../catalog/api/getting-started.md) om datasetdetails op te zoeken, als de dataset een actieve afloop heeft zal het onder worden vermeld `tags.adobe/hygiene/ttl`.

De volgende JSON vertegenwoordigt een afgekapte reactie voor de details van een dataset van Catalog, die een vervalwaarde van `32503680000000`. De waarde van de tag codeert de vervaldatum als een geheel getal in milliseconden sinds het begin van het Unix-tijdperk.

```json
{
  "63212313c308d51b997858ba": {
    "name": "TTL Test Dataset",
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

## Een gegevensset maken of bijwerken {#create-or-update}

U kunt een vervaldatum voor een dataset door een verzoek van de PUT tot stand brengen of bijwerken.

**API-indeling**

```http
PUT /ttl/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | Identiteitskaart van de dataset die u een vervaldatum wilt plannen. |

**Verzoek**

Het volgende verzoek plant een dataset `5b020a27e7040801dedbf46e` om eind 2022 te worden geschrapt (Greenwich Mean Time). Als er geen bestaande vervaldatum voor de gegevensset wordt gevonden, wordt een nieuwe vervaldatum gemaakt. Als de gegevensset al een in behandeling zijnde vervaldatum heeft, wordt die vervaldatum bijgewerkt met de nieuwe `expiry` waarde.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `expiry` | Een tijdstempel van ISO 8601 voor het tijdstip waarop de gegevensset wordt verwijderd. |
| `displayName` | Een weergavenaam voor de vervalaanvraag. |
| `description` | Een optionele beschrijving voor de vervalaanvraag. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de gegevenssetvervaldatum, met HTTP status 200 (OK) als een bestaande vervaldatum is bijgewerkt, of 201 (Gemaakt) als er geen bestaande vervaldatum was.

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
| `imsOrg` | De id van uw organisatie. |
| `status` | De huidige status van de gegevenssetvervaldatum. |
| `expiry` | De geplande datum en tijd waarop de dataset zal worden geschrapt. |
| `updatedAt` | Een tijdstempel van wanneer de vervaldatum voor het laatst is bijgewerkt. |
| `updatedBy` | De gebruiker die de vervaldatum voor het laatst heeft bijgewerkt. |

{style=&quot;table-layout:auto&quot;}

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
| `{EXPIRATION_ID}` | De `workorderId` van de gegevenssetvervaldatum die u wilt annuleren. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Het volgende verzoek annuleert een gegevenssetvervaldatum met identiteitskaart `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) en de vervaldatums `status` kenmerk is ingesteld op `cancelled`.

## Haal de geschiedenis van de vervalstatus van een dataset terug

U kunt de geschiedenis van de vervalstatus van een specifieke dataset opzoeken door de vraagparameter te gebruiken `include=history` in een opzoekverzoek. Het resultaat omvat informatie over de verwezenlijking van de dataset vervaldatum, om het even welke updates die zijn toegepast, en zijn annulering of uitvoering (indien van toepassing).

**API-indeling**

```http
GET /ttl/{DATASET_ID}?include=history
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | Identiteitskaart van de dataset de waarvan vervalgeschiedenis u omhoog wilt zoeken. |

{style=&quot;table-layout:auto&quot;}

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
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
| `datasetName` | De vertoningsnaam voor de dataset is deze vervaldatum van toepassing op. |
| `sandboxName` | De naam van de sandbox waarin de doelgegevensset zich bevindt. |
| `displayName` | De weergavenaam voor de vervalaanvraag. |
| `description` | Een beschrijving van de vervalaanvraag. |
| `imsOrg` | De id van uw organisatie. |
| `history` | Hiermee wordt de geschiedenis van updates voor de vervaldatum weergegeven als een array van objecten, waarbij elk object het `status`, `expiry`, `updatedAt`, en `updatedBy` kenmerken voor de vervaldatum op het moment van de update. |

{style=&quot;table-layout:auto&quot;}

## Aanhangsel

### Geaccepteerde queryparameters {#query-params}

De volgende tabel geeft een overzicht van de beschikbare queryparameters wanneer [gegevensset met lijsten verlopen](#list):

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `size` | Een geheel getal in het bereik van 1 tot en met 100 dat het maximale aantal retourneringen aangeeft. De standaardwaarde is 25. | `size=50` |
| `page` | Een geheel getal dat aangeeft welke pagina met vervaldatums moet worden geretourneerd. | `page=3` |
| `orgId` | Komt datasets vervaldagen met de organisatie ID aan die van de parameter. Deze waarde is standaard ingesteld op `x-gw-ims-org-id` kopballen, en wordt genegeerd tenzij het verzoek een de dienstteken levert. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | Een door komma&#39;s gescheiden lijst met statussen. Wanneer inbegrepen, past de reactie datasettermijnen aan de waarvan huidige status onder die vermeld is. | `status=pending,cancelled` |
| `author` | Komt overeen met verlopen waarvan `created_by` is een overeenkomst voor de zoekreeks. Als de zoektekenreeks begint met `LIKE` of `NOT LIKE`, de rest wordt behandeld als een SQL-zoekpatroon. Anders wordt de gehele zoektekenreeks beschouwd als een letterlijke tekenreeks die exact moet overeenkomen met de volledige inhoud van een tekenreeks `created_by` veld. | `author=LIKE %john%` |
| `sandboxName` | Komt overeen met de vervaldatum van de gegevensset waarvan de naam van de sandbox precies overeenkomt met het argument. Wordt standaard ingesteld op de naam van de sandbox in de aanvraag `x-sandbox-name` header. Gebruiken `sandboxName=*` om gegevenssetvervaldatums uit alle sandboxen op te nemen. | `sandboxName=dev1` |
| `datasetId` | Komt overeen met verlopen die van toepassing zijn op specifieke dataset. | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | Komt overeen met verlopen die in het venster van 24 uur zijn gemaakt, te beginnen bij het opgegeven tijdstip.<br><br>Datums zonder tijd (zoals `2021-12-07`) staat voor de datetime aan het begin van die dag. Daarom `createdDate=2021-12-07` verwijst naar elke vervaldatum die op 7 december 2021 is gemaakt, met ingang van `00:00:00` doorheen `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Komt overeen met verlopen die op of na de aangegeven tijd zijn gemaakt. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Komt overeen met verlopen die op of voor de aangegeven tijd zijn gemaakt. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | leuk `createdDate` / `createdFromDate` / `createdToDate`, maar komt overeen met de updatetijd van een gegevensset die vervalt in plaats van de aanmaaktijd.<br><br>Een vervaldatum wordt beschouwd als bijgewerkt op elke bewerking, ook wanneer deze wordt gemaakt, geannuleerd of uitgevoerd. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Komt overeen met verlopen die op elk moment in het aangegeven interval zijn geannuleerd. Dit is zelfs van toepassing als de vervaldatum later opnieuw werd geopend (door een nieuwe vervaldatum voor de zelfde dataset te plaatsen). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Komt overeen met verlopen die tijdens het opgegeven interval zijn voltooid. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Komt overeen met vervaldata die moeten worden uitgevoerd, of reeds zijn uitgevoerd, tijdens het opgegeven interval. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
