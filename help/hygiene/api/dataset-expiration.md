---
title: API-eindpunt voor gegevenssetvervaldatums
description: Het /ttl eindpunt in de Hygiene API van Gegevens staat u toe om datasettermijnen in Adobe Experience Platform programmatically te plannen.
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 5a12c75a54f420b2ca831dbfe05105dfd856dc4d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 1%

---

# Eindpunt gegevensset

>[!IMPORTANT]
>
>De mogelijkheden voor gegevenshygiëne in Adobe Experience Platform zijn momenteel alleen beschikbaar voor organisaties die een gezondheidsschild hebben aangeschaft.

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
  https://platform.adobe.io/data/core/hygiene/ttl?page=1&size=50 \
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
      "ttlId": "SDfba908e9fb2e427ab4275d20465631d7",
      "datasetId": "62799c3e1151781b63ccaa28",
      "imsOrg": "{ORG_ID}",
      "status": "cancelled",
      "expiry": "2022-05-09T22:57:05.531024Z",
      "updatedAt": "2022-05-09T22:57:05.531025Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
      "datasetId": "62759f2ede9e601b63a2ee14",
      "imsOrg": "{ORG_ID}",
      "status": "pending",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    }
  ],
  "current_page": 1,
  "total_pages": 36,
  "total_count": 886
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `results` | Bevat de details van de teruggekeerde datasettermijnen. Voor meer details over de eigenschappen van een datasetafloop, zie de reactiesectie voor het maken van a [opzoekvraag](#lookup). |
| `current_page` | De huidige pagina met resultaten in de lijst. |
| `total_pages` | Het totale aantal pagina&#39;s in het antwoord. |
| `total_count` | Het totale aantal gegevenssetvervaldata in de reactie. |

{style=&quot;table-layout:auto&quot;}

## Een gegevensset opzoeken die vervalt {#lookup}

U kunt een datasetvervaldatum door een verzoek van de GET opzoeken.

**API-indeling**

```http
GET /ttl/{TTL_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{TTL_ID}` | Identiteitskaart van de datasetvervaldatum die u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de datasetvervaldatum terug.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
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

{style=&quot;table-layout:auto&quot;}

## Een gegevensset maken die vervalt {#create}

U kunt een vervaldatum voor een dataset door een verzoek van de POST tot stand brengen.

**API-indeling**

```http
POST /ttl
```

**Verzoek**

Het volgende verzoek plant een dataset `5b020a27e7040801dedbf46e` om eind 2022 te worden geschrapt (Greenwich Mean Time).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "5b020a27e7040801dedbf46e",
        "expiry": "2022-12-31T23:59:59Z"
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `datasetId` | De id van de dataset waarvoor u een vervaldatum wilt plannen. |
| `expiry` | Een tijdstempel van ISO 8601 voor het tijdstip waarop de gegevensset wordt verwijderd. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de gegevenssetvervaldatum, met HTTP status 200 (OK) als een bestaande vervaldatum is bijgewerkt, of 201 (Gemaakt) als er geen bestaande vervaldatum was.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}"
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

{style=&quot;table-layout:auto&quot;}

## Vervaldatum gegevensset bijwerken {#update}

U kunt een datasetvervaldatum door een verzoek van de PUT bijwerken.

**API-indeling**

```http
PUT /ttl/{TTL_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{TTL_ID}` | Identiteitskaart van de datasetvervaldatum die u wilt wijzigen. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Het volgende verzoek werkt het verstrijken voor dataset bij `5b020a27e7040801dedbf46e` en loopt dus eind 2023 af (Greenwich Mean Time).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2023-12-31T23:59:59Z"
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `expiry` | Een tijdstempel van ISO 8601 voor het tijdstip waarop de gegevensset wordt verwijderd. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert de details van de bijgewerkte vervaldatum.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}"
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

{style=&quot;table-layout:auto&quot;}

## Vervaldatum gegevensset annuleren {#delete}

U kunt een gegevenssetvervaldatum annuleren door een verzoek van de DELETE te doen.

**API-indeling**

```http
DELETE /ttl/{TTL_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{TTL_ID}` | De id van de gegevenssetvervaldatum die u wilt annuleren. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Het volgende verzoek werkt het verstrijken voor dataset bij `5b020a27e7040801dedbf46e` en loopt dus eind 2023 af (Greenwich Mean Time).

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de datasetvervaldatum, met zijn terug `status` kenmerk nu ingesteld op `cancelled`.

```json
{
    "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "cancelled",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T23:47:30.071186Z",
    "updatedBy": "{USER_ID}"
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

{style=&quot;table-layout:auto&quot;}

## De geschiedenis van een gegevensset-vervaldatum ophalen

U kunt omhoog de geschiedenis van een specifieke datasetvervalsing kijken door de vraagparameter te gebruiken `include=history` in een opzoekverzoek. Het resultaat omvat informatie over de verwezenlijking van de dataset vervaldatum, om het even welke updates die zijn toegepast, en zijn annulering of uitvoering (indien van toepassing).

**API-indeling**

```http
GET /ttl/{TTL_ID}?include=history
```

| Parameter | Beschrijving |
| --- | --- |
| `{TTL_ID}` | Identiteitskaart van de datasetvervalsing waarvan geschiedenis u omhoog wilt kijken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert de details van de datasetvervaldatum, met terug `history` array met de details `status`, `expiry`, `updatedAt`, en `updatedBy` kenmerken voor elk van de opgenomen updates.

```json
{
  "ttlId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
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
| `ttlId` | De id van de vervaldatum van de gegevensset. |
| `datasetId` | De id van de gegevensset waarop deze vervaldatum van toepassing is. |
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
| `status` | Een door komma&#39;s gescheiden lijst met statussen. Wanneer inbegrepen, past de reactie datasettermijnen aan de waarvan huidige status onder die vermeld is. | `status=pending,cancelled` |
| `author` | Komt overeen met verlopen waarvan `created_by` is een overeenkomst voor de zoekreeks. Als de zoektekenreeks begint met `LIKE` of `NOT LIKE`, de rest wordt behandeld als een SQL-zoekpatroon. Anders wordt de gehele zoektekenreeks beschouwd als een letterlijke tekenreeks die exact moet overeenkomen met de volledige inhoud van een tekenreeks `created_by` veld. | `author=LIKE %john%` |
| `createdDate` | Komt overeen met verlopen die in het venster van 24 uur zijn gemaakt, te beginnen bij het opgegeven tijdstip.<br><br>Datums zonder tijd (zoals `2021-12-07`) staat voor de datetime aan het begin van die dag. Daarom `createdDate=2021-12-07` verwijst naar elke vervaldatum die op 7 december 2021 is gemaakt, met ingang van `00:00:00` doorheen `23:59:59.999999999` (UTC). | `createdDate=2021-12-07` |
| `createdFromDate` | Komt overeen met verlopen die op of na de aangegeven tijd zijn gemaakt. | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | Komt overeen met verlopen die op of voor de aangegeven tijd zijn gemaakt. | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | leuk `createdDate` / `createdFromDate` / `createdToDate`, maar komt overeen met de updatetijd van een gegevensset die vervalt in plaats van de aanmaaktijd.<br><br>Een vervaldatum wordt beschouwd als bijgewerkt op elke bewerking, ook wanneer deze wordt gemaakt, geannuleerd of uitgevoerd. | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | Komt overeen met verlopen die op elk moment in het aangegeven interval zijn geannuleerd. Dit is zelfs van toepassing als de vervaldatum later opnieuw werd geopend (door een nieuwe vervaldatum voor de zelfde dataset te plaatsen). | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | Komt overeen met verlopen die tijdens het opgegeven interval zijn voltooid. | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | Komt overeen met vervaldata die moeten worden uitgevoerd, of reeds zijn uitgevoerd, tijdens het opgegeven interval. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
