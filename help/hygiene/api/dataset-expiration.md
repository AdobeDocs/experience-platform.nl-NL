---
title: API-eindpunt gegevensset vervaldatum
description: Het /ttl eindpunt in de Hygiene API van Gegevens staat u toe om datasettermijnen in Adobe Experience Platform programmatically te plannen.
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 0%

---

# Eindpunt gegevensset

Gebruik het `/ttl` eindpunt in de API voor gegevenshygiëne om te plannen wanneer datasets in Adobe Experience Platform moeten worden verwijderd.

Een gegevenssetvervaldatum is een vertraagde schrappingsverrichting. De gegevensset is niet in de tussentijd beschermd en kan op een andere manier worden verwijderd vóór de geplande vervaldatum.

>[!NOTE]
>
>Hoewel de vervaldatum als een specifiek tijdstip wordt gespecificeerd, kan er tot 24 uur vertraging na het verstrijken van de vervaldatum zijn voordat de eigenlijke verwijdering wordt gestart. Wanneer de verwijdering is gestart, kan het maximaal zeven dagen duren voordat alle sporen van de gegevensset uit Experience Platform-systemen zijn verwijderd.

Voordat het verwijderen begint, kunt u de vervaldatum annuleren of de geplande tijd ervan wijzigen. Stel een nieuwe vervaldatum in om een geannuleerde vervaldatum opnieuw te openen.

Nadat het verwijderen is gestart, wordt de vervaltaak gemarkeerd als `executing` en kan deze niet meer worden gewijzigd. De gegevensset kan maximaal zeven dagen worden hersteld, maar alleen via een handmatig verzoek van de Adobe-service. Tijdens schrapping, verwijderen het gegevens meer, de Dienst van de Identiteit, en het Profiel van de Klant in real time elk de gegevenssetinhoud afzonderlijk. Wanneer het verwijderen is voltooid, wordt de vervaldatum gemarkeerd als `completed` .

>[!WARNING]
>
>Als een dataset wordt geplaatst om te verlopen, moet u om het even welke gegevensstromen manueel veranderen die gegevens in die dataset kunnen opnemen zodat uw stroomafwaartse werkschema&#39;s niet negatief worden beïnvloed.

Het geavanceerde Beheer van de Levenscyclus van Gegevens steunt datasetschrappingen door het eindpunt van de gegevenssetvervalsing en identiteitskaart schrappingen (rij-vlakke gegevens) gebruikend primaire identiteiten via het [ werkordeeindpunt ](./workorder.md). U kunt [ datasetvervalingen ](../ui/dataset-expiration.md) en [ verslagschrappingen ](../ui/record-delete.md) door Experience Platform UI ook beheren. Raadpleeg de gekoppelde documentatie voor meer informatie.

>[!NOTE]
>
>Gegevenslevenscyclus ondersteunt het verwijderen van batches niet.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de Data Hygiene API. Alvorens verder te gaan, te herzien gelieve de [ API gids ](./overview.md) voor informatie over vereiste kopballen voor verrichtingen CRUD, foutenmeldingen, de inzamelingen van Postman, en hoe te om steekproefAPI vraag te lezen.

>[!IMPORTANT]
>
>Wanneer u de gegevens Hygiene API aanroept, moet u de header -H `x-sandbox-name: {SANDBOX_NAME}` gebruiken.

## Verlopen gegevensset weergeven {#list}

U kunt van alle datasettermijnen een lijst maken die voor uw organisatie door een verzoek van GET aan het `/ttl` eindpunt worden gevormd.

De resultaten van de filter gebruikend vraagparameters om slechts de termijnen terug te keren die aan uw criteria voldoen. Elk resultaat omvat status en configuratiedetails voor elke datasetvervaldatum.

**API formaat**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMETERS}` | Een lijst met optionele queryparameters, met meerdere parameters gescheiden door `&` tekens. Algemene parameters zijn `limit` en `page` voor pagineringsdoeleinden. Voor een volledige lijst van gesteunde vraagparameters, verwijs naar de [ bijlage sectie ](#query-params) een volledige lijst van gesteunde vraagparameters. De meest gebruikte parameters zijn hieronder en in het aanhangsel opgenomen. |
| `author` | Filter op de gebruiker die de gegevenssetvervaldatum het laatst heeft bijgewerkt of gemaakt. Biedt ondersteuning voor SQL-achtige patronen (bijvoorbeeld `LIKE %john%` ). |
| `datasetId` | Filtervervaltijden met een specifieke dataset-id. |
| `datasetName` | Een hoofdlettergevoelig filter voor overeenkomende gegevenssetnamen. |
| `status` | Filter op een door komma&#39;s gescheiden lijst met statussen: `pending`, `executing`, `cancelled`, `completed`. |
| `expiryDate` | Filter voor verlopen met een specifieke vervaldatum. |
| `limit` | Het maximale aantal resultaten bepalen dat moet worden geretourneerd (1-100, standaard: 25). |
| `page` | Pagineringsresultaten met een op nul gebaseerde index (standaardpaginaformaat: 50, max: 100). |

{style="table-layout:auto"}

**Verzoek**

Het volgende verzoek wint alle datasettermijnen terug die vóór 1 Augustus, 2021 worden bijgewerkt, en laatst bijgewerkt door een gebruiker de waarvan naam &quot;Jansen&quot;aanpast.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie maakt een lijst van de resulterende datasetvervaldata. Het volgende voorbeeld is afgekapt voor ruimte.

>[!IMPORTANT]
>
>`ttlId` in de reactie wordt ook wel `{DATASET_EXPIRATION_ID}` genoemd. Zij allebei verwijzen naar het unieke herkenningsteken voor de datasetvervaldatum.

```json
{
  "results": [
    {
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `results` | Een serie van configuraties van de datasetvervaldatum. |
| `ttlId` | Het unieke herkenningsteken voor de configuratie van de gegevenssetvervaldatum. |
| `datasetId` | Het unieke herkenningsteken van de dataset verbonden aan deze configuratie. |
| `datasetName` | De naam van de gegevensset. |
| `sandboxName` | De sandbox waarin deze gegevenssetvervaldatum is geconfigureerd. |
| `displayName` | Een voor mensen leesbare naam voor de vervalconfiguratie. |
| `description` | Een beschrijving van de vervalconfiguratie. |
| `imsOrg` | Uw unieke organisatie-id. |
| `status` | De huidige status van de vervaldatum. Een van: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | De geplande vervaldatum en -tijd (ISO 8601-indeling). |
| `updatedAt` | De tijdstempel van de laatste update van deze configuratie. |
| `updatedBy` | De id en e-mail van de gebruiker of service die de configuratie voor het laatst heeft bijgewerkt. |
| `current_page` | De index van de huidige resultatenpagina (op nul gebaseerd). |
| `total_pages` | The total number of result pages available. |
| `total_count` | Het totale aantal verslagen van de gegevenssetvervalconfiguratie teruggekeerde. |

{style="table-layout:auto"}

## Een gegevensset opzoeken die vervalt {#lookup}

Haal de details voor een specifieke configuratie van de datasetvervaldatum door een verzoek van GET met of identiteitskaart van de datasetvervaldatum of datasetidentiteitskaart als wegparameter te doen.

>[!IMPORTANT]
>
>U kunt een id voor de vervaldatum van een gegevensset opgeven (bijvoorbeeld `SD-xxxxxx-xxxx` ) of een id voor een gegevensset in het pad. `ttlId` in de reactie is de unieke id voor de vervaldatum van de gegevensset.

**API formaat**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| Parameter | Beschrijving |
| --- | --- |
| `{ID}` | Het unieke herkenningsteken voor de configuratie van de gegevenssetvervaldatum. U kunt of een identiteitskaart van de gegevenssetvervaldatum of een datasetidentiteitskaart verstrekken. |
| `include` | (Optioneel) Indien ingesteld op `history` , bevat de reactie een `history` -array met wijzigingsgebeurtenissen voor de configuratie. |

{style="table-layout:auto"}

**Verzoek**

In het volgende verzoek worden de vervalgegevens voor de gegevensset `62759f2ede9e601b63a2ee14` weergegeven:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de details van de datasetvervaldatum terug.

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `ttlId` | Het unieke herkenningsteken voor de configuratie van de gegevenssetvervaldatum. |
| `datasetId` | De unieke id voor de gegevensset. |
| `datasetName` | De naam van de gegevensset. |
| `sandboxName` | De sandbox waarin de gegevenssetvervaldatum is geconfigureerd. |
| `displayName` | Een voor mensen leesbare naam voor de vervalconfiguratie van de gegevensset. |
| `description` | Een beschrijving van de configuratie van de datasetvervaldatum. |
| `imsOrg` | Uw unieke organisatie-id die aan deze configuratie is gekoppeld. |
| `status` | De huidige status van de configuratie van de datasetvervaldatum.<br> Één van: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | De geplande tijdstempel voor de vervaldatum voor de gegevensset (ISO 8601-indeling). |
| `updatedAt` | Tijdstempel voor de meest recente update. |
| `updatedBy` | De id en e-mail van de gebruiker of dienst die het laatst de gegevenssetvervaldatum bijwerkte. |

{style="table-layout:auto"}

### Vervaltags voor catalogi

Wanneer het gebruiken van de [ Catalogus API ](../../catalog/api/getting-started.md) om datasetdetails op te zoeken, als de dataset een actieve afloop heeft zal het onder `tags.adobe/hygiene/ttl` worden vermeld.

In de volgende JSON wordt een ingekorte API-reactie van de catalogus weergegeven voor een dataset met de vervalwaarde `32503680000000` . De tag codeert de vervaldatum als het aantal milliseconden dat is verstreken sinds het Unix-tijdperk.

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

Creeer een nieuwe configuratie van de datasetvervaldatum om te bepalen wanneer een dataset zal verlopen en verkiesbaar voor schrapping zijn.\
Geef de id van de gegevensset, de vervaldatum of de datum-tijd (in ISO 8601-indeling), een weergavenaam en (optioneel) een beschrijving op.

>[!NOTE]
>
>De vervalwaarde kan een datum (JJJJ-MM-DD) of een datum en een tijd (JJJJ-MM-DDTHH :MM: SSZ) zijn. Als u slechts een datum verstrekt, gebruikt het systeem middernacht UTC (00 :00: 00Z) op die dag. De vervaldatum moet in de toekomst ten minste 24 uur zijn.

Om een datasetvervaldatum tot stand te brengen, verzend een POST- verzoek zoals hieronder getoond.

>[!TIP]
>
>Als u een fout van 404 ontvangt, zorg ervoor dat het verzoek geen extra voorwaartse schuine strepen heeft. Een volgslash kan ertoe leiden dat een POST-aanvraag mislukt.

**API formaat**

```http
POST /ttl
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `datasetId` | **Vereist.** De unieke id voor de dataset om de vervaldatum toe te passen. |
| `expiry` | **Vereist.** De vervaldatum en -tijd in de ISO 8601-indeling. Dit bepaalt de levensduur van gegevens binnen het systeem. Als slechts een datum wordt verstrekt, blijft aan middernacht UTC (00 :00: 00Z) in gebreke. Het verstrijken **moet minstens 24 uren in de toekomst zijn**. <br>**NOTA**:<ul><li>Het verzoek zal ontbreken als een datasetvervaldatum reeds voor de dataset bestaat.</li></ul> |
| `displayName` | **Vereist.** Een voor mensen leesbare naam voor de vervalconfiguratie van de gegevensset. |
| `description` | Een facultatieve beschrijving voor de configuratie van de datasetvervaldatum. |

**Reactie**

Een succesvolle reactie keert een (Gecreeerde) status HTTP 201 en de nieuwe configuratie van de datasetvervaldatum terug.

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `ttlId` | De unieke herkenningsteken voor de gecreeerde configuratie van de datasetvervaldatum. |
| `datasetId` | De unieke id voor de gegevensset. |
| `datasetName` | De naam van de gegevensset. |
| `sandboxName` | De sandbox waarin deze gegevenssetvervaldatum is geconfigureerd. |
| `displayName` | De vertoningsnaam voor de configuratie van de datasetvervaldatum. |
| `description` | Een beschrijving van de configuratie van de datasetvervaldatum. |
| `imsOrg` | Uw unieke organisatie-id die aan deze configuratie is gekoppeld. |
| `status` | De huidige status van de configuratie van de datasetvervaldatum.<br> Één van: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | De geplande tijdstempel voor de vervaldatum voor de gegevensset. |
| `updatedAt` | De tijdstempel voor de meest recente update. |
| `updatedBy` | De herkenningsteken en e-mail van de gebruiker of de dienst die de configuratie van de datasetvervaldatum het laatst bijwerkte. |

De HTTP-status 400 (Onjuist verzoek) treedt op als er al een gegevenssetvervaldatum bestaat voor de gegevensset. De HTTP-status 404 (Niet gevonden) treedt op als een dergelijke gegevensset niet bestaat of als u geen toegang hebt tot de gegevensset.

## Een configuratie voor de vervaldatum van een gegevensset bijwerken {#update}

Als u een bestaande vervalconfiguratie van een gegevensset wilt bijwerken, vraagt u PUT om `/ttl/DATASET_EXPIRATION_ID` . U kunt alleen de velden `displayName` , `description` en `expiry` van de configuratie bijwerken. Updates zijn alleen toegestaan wanneer de vervalstatus `pending` is.

>[!NOTE]
>
>Het `expiry` gebied keurt een datum (JJJJ-MM-DD) of datum en tijd (JJJJ-MM-DDTHH :MM: SSZ) goed. Als slechts een datum wordt verstrekt, gebruikt het systeem middernacht UTC (00 :00: 00Z) op die dag. Het verstrijken **moet minstens 24 uren in de toekomst zijn**.

**API formaat**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | Het unieke herkenningsteken voor de configuratie van de gegevenssetvervaldatum. **NOTA**: Dit wordt bedoeld als `ttlId` in de reactie. |

**Verzoek**

De volgende aanvraag werkt de vervaldatum, weergavenaam en beschrijving voor de vervaldatum van de gegevensset bij `SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45` :

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `displayName` | (Optioneel) Een nieuwe, leesbare naam voor de vervalconfiguratie van de gegevensset. |
| `description` | (Optioneel) Een nieuwe beschrijving voor de vervalconfiguratie van de gegevensset. |
| `expiry` | (Optioneel) Een nieuwe vervaldatum of -datum en -tijd in de ISO 8601-indeling. Als alleen een datum wordt opgegeven, wordt standaard UTC om middernacht gebruikt. De vervaldatum moet **minstens 24 uren in de toekomst** zijn. |

>[!NOTE]
>
>In de aanvraag moet ten minste een van deze velden worden ingevuld.

**Reactie**

Een succesvolle reactie keert HTTP status 200 (OK) en de bijgewerkte configuratie van de datasetvervaldatum terug.

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `ttlId` | De unieke herkenningsteken voor de bijgewerkte configuratie van de datasetvervaldatum. |
| `datasetId` | De unieke id voor de gegevensset. |
| `datasetName` | De naam van de gegevensset. |
| `sandboxName` | De sandbox waarin deze gegevenssetvervaldatum is geconfigureerd. |
| `displayName` | De vertoningsnaam voor de configuratie van de datasetvervaldatum. |
| `description` | Een beschrijving van de configuratie van de datasetvervaldatum. |
| `imsOrg` | De organisatie-id die aan deze configuratie is gekoppeld. |
| `status` | De huidige status van de configuratie van de datasetvervaldatum.<br> Één van: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | De geplande tijdstempel voor de vervaldatum voor de gegevensset. |
| `updatedAt` | De tijdstempel voor de meest recente update. |
| `updatedBy` | De herkenningsteken en e-mail van de gebruiker of de dienst die de configuratie van de datasetvervaldatum het laatst bijwerkte. |

{style="table-layout:auto"}

Een mislukte reactie retourneert een HTTP-status van 404 (Niet gevonden) als een dergelijke vervaldatum van de gegevensset niet bestaat.

## Vervaldatum gegevensset annuleren {#delete}

Annuleer een in afwachting zijnde configuratie voor de vervaldatum van een dataset door een DELETE-aanvraag in te dienen bij `/ttl/{ID}`.

>[!NOTE]
>
>Alleen gegevenssetverlopen in de status `pending` kunnen worden geannuleerd. Als u probeert een vervaldatum te annuleren die al `executing` , `completed` of `cancelled` is, wordt HTTP 400 geretourneerd (Ongeldige aanvraag).

**API formaat**

```http
DELETE /ttl/{ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{ID}` | Het unieke herkenningsteken voor de configuratie van de gegevenssetvervaldatum. U kunt of een identiteitskaart van de gegevenssetvervaldatum of een datasetidentiteitskaart verstrekken. |

{style="table-layout:auto"}

**Verzoek**

Het volgende verzoek annuleert een gegevenssetvervaldatum met identiteitskaart `SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert HTTP status 200 (OK) en de geannuleerde configuratie van de datasetvervaldatum terug. Het kenmerk `status` van de vervaldatum wordt niet ingesteld op `cancelled` .

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| Eigenschap | Beschrijving |
|---|---|
| `ttlId` | De unieke herkenningsteken voor de geschrapte configuratie van de datasetvervaldatum. |
| `datasetId` | De unieke id voor de gegevensset. |
| `datasetName` | De naam van de gegevensset. |
| `sandboxName` | De sandbox waarin deze gegevenssetvervaldatum is geconfigureerd. |
| `displayName` | De vertoningsnaam voor de configuratie van de datasetvervaldatum. |
| `description` | Een beschrijving van de configuratie van de datasetvervaldatum. |
| `imsOrg` | Uw unieke organisatie-id die aan deze configuratie is gekoppeld. |
| `status` | De huidige status van de configuratie van de datasetvervaldatum.<br> Één van: `pending`, `executing`, `cancelled`, `completed`. |
| `expiry` | De geplande tijdstempel voor de vervaldatum voor de gegevensset. |
| `updatedAt` | De tijdstempel voor de meest recente update. |
| `updatedBy` | De herkenningsteken en e-mail van de gebruiker of de dienst die de configuratie van de datasetvervaldatum het laatst bijwerkte. |

**Voorbeeld 400 (Slecht Verzoek) reactie**

Er treedt een fout van 400 op wanneer u probeert een gegevensset te annuleren die de vervalconfiguratie `executing` , `completed` of `cancelled` heeft.

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>Er treedt een fout van 404 op wanneer wordt geprobeerd een gegevenssetvervaldatum te annuleren die al `completed` of `cancelled` is.

## Bijlage

### Geaccepteerde queryparameters {#query-params}

De volgende lijst schetst de beschikbare vraagparameters wanneer [ van de lijst dataset vervalst ](#list):

>[!NOTE]
>
>De parameters `description`, `displayName` en `datasetName` bevatten allemaal de mogelijkheid te zoeken op basis van LIKE-waarden. Dit betekent dat u geplande gegevenssetvervaldatums genoemd kunt vinden: &quot;Name123&quot;, &quot;Name183&quot;, &quot;DisplayName1234&quot; door naar het koord &quot;Name1&quot;te zoeken.

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `author` | Gebruik de `author` vraagparameter om de persoon te vinden die onlangs de datasetvervaldatum bijwerkte. Als er sinds het maken geen updates zijn uitgevoerd, komt deze overeen met de oorspronkelijke maker van de vervaldatum. Deze parameter komt overeen met vervaltijden waarbij het veld `created_by` overeenkomt met de zoektekenreeks.<br> als het onderzoekskoord met `LIKE` of `NOT LIKE` begint, wordt het resterende behandeld als SQL onderzoekspatroon. Anders wordt de gehele zoektekenreeks beschouwd als een letterlijke tekenreeks die exact moet overeenkomen met de volledige inhoud van een `created_by` -veld. | `author=LIKE %john%`, `author=John Q. Public` |
| `datasetId` | Komt overeen met verlopen die van toepassing zijn op specifieke dataset. | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | Komt overeen met verlopen waarvan de naam van de gegevensset de opgegeven zoekreeks bevat. De overeenkomst is niet hoofdlettergevoelig. | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | Komt overeen met verlopen waarvan de weergavenaam de opgegeven zoekreeks bevat. De overeenkomst is niet hoofdlettergevoelig. | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | Hiermee filtert u de resultaten op basis van een exacte uitvoeringsdatum, een einddatum voor de uitvoering of een begindatum voor de uitvoering. Zij worden gebruikt om gegevens of verslagen terug te winnen verbonden aan de uitvoering van een verrichting op een specifieke datum, vóór een bepaalde datum, of na een bepaalde datum. | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | Komt overeen met verlopen die in het 24-uurvenster van de gespecificeerde datum voorkwamen. | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | Komt overeen met vervaldata die moeten worden uitgevoerd, of reeds zijn uitgevoerd, tijdens het opgegeven interval. | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | Een geheel getal in het bereik van 1 tot en met 100 dat het maximale aantal retourneringen aangeeft. De standaardwaarde is 25. | `limit=50` |
| `orderBy` | De `orderBy` query parameter specificeert de sorteervolgorde van de resultaten die door API worden geretourneerd. Gebruik dit schema om de gegevens te rangschikken op basis van een of meer velden, in oplopende (ASC) of aflopende (DESC) volgorde. Gebruik + of - prefix om ASC, DESC respectievelijk te betekenen. De volgende waarden worden geaccepteerd: `displayName`, `description`, `datasetName`, `id`, `updatedBy`, `updatedAt`, `expiry`, `status` . | `-datasetName` |
| `orgId` | Komt datasets vervaldagen met de organisatie ID aan die van de parameter. Deze waarde is standaard ingesteld op de waarde van de headers van `x-gw-ims-org-id` en wordt genegeerd, tenzij de aanvraag een servicetoken levert. | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | Een geheel getal dat aangeeft welke pagina met verlopen moet worden geretourneerd. | `page=3` |
| `sandboxName` | Komt overeen met de vervaldatum van de gegevensset waarvan de naam van de sandbox precies overeenkomt met het argument. Wordt standaard ingesteld op de naam van de sandbox in de `x-sandbox-name` -header van de aanvraag. Gebruik `sandboxName=*` om gegevenssetvervaldatums van alle sandboxen op te nemen. | `sandboxName=dev1` |
| `search` | Komt verlopen overeen waar het gespecificeerde koord een nauwkeurige gelijke voor vervalidentiteitskaart is, of **bevat** op om het even welk van deze gebieden is:<br><ul><li>auteur</li><li>weergavenaam</li><li>beschrijving</li><li>weergavenaam</li><li>naam gegevensset</li></ul> | `search=TESTING` |
| `status` | Een door komma&#39;s gescheiden lijst met statussen. Wanneer inbegrepen, past de reactie datasettermijnen aan de waarvan huidige status onder die vermeld is. | `status=pending,cancelled` |
| `ttlId` | Komt overeen met het vervalverzoek met de opgegeven id. | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | Komt overeen met verlopen die in het 24-uurvenster van de gespecificeerde datum werden bijgewerkt. | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | Komt overeen met verlopen die in het 24-uursvenster werden bijgewerkt en die bij het aangegeven tijdstip begonnen.<br><br> een vervaldatum wordt beschouwd als bijgewerkt op elke geef uit, met inbegrip van wanneer het wordt gecreeerd, geannuleerd, of uitgevoerd. | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

