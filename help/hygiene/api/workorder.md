---
title: Werkorders verwijderen opnemen
description: Leer hoe te om het /workorder eindpunt in de Hygiene API van Gegevens te gebruiken om het werkorden van het verslag te beheren schrapt in Adobe Experience Platform. Deze handleiding heeft betrekking op quota, verwerkingstijdlijnen en API-gebruik.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 1d923e6c4a344959176abb30a8757095c711a601
workflow-type: tm+mt
source-wordcount: '2541'
ht-degree: 0%

---

# Werkorders opnemen om gegevens te verwijderen {#work-order-endpoint}

Gebruik het `/workorder` eindpunt in de API voor gegevenshygiëne om werkorders voor het verwijderen van records in Adobe Experience Platform te maken, weer te geven en te beheren. Met werkorders kunt u gegevensverwijdering in verschillende gegevenssets beheren, controleren en volgen, zodat u de gegevenskwaliteit kunt behouden en de standaarden voor gegevensbeheer van uw organisatie kunt ondersteunen.

>[!IMPORTANT]
>
>De opdracht Werkorders voor het verwijderen van records is bedoeld voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. **gebruik geen het werkorden van het verslag schrappingswerk voor de verzoeken van de gegevenssubject rechten onder privacyverordeningen zoals GDPR.** voor de gevallen van het nalevingsgebruik, gebruik [&#x200B; Adobe Experience Platform Privacy Service &#x200B;](../../privacy-service/home.md).

## Aan de slag

Alvorens u begint, zie het [&#x200B; overzicht &#x200B;](./overview.md) om over vereiste kopballen te leren, hoe te steekproefAPI vraag lezen, en waar te om verwante documentatie te vinden.

## Quoten en verwerkingstijdlijnen {#quotas}

Voor het opnemen van verwijderwerkorders gelden dagelijkse en maandelijkse indieningslimieten voor id&#39;s, die worden bepaald door de licentierechten van uw organisatie. Deze limieten gelden voor aanvragen voor het verwijderen van records via de gebruikersinterface en API.

>[!NOTE]
>
>U kunt tot **1.000.000 herkenningstekens per dag** voorleggen, maar slechts als uw resterende maandquotum het toestaat. Als uw maandelijks maximum minder dan 1 miljoen bedraagt, kan uw dagelijkse inzending die limiet niet overschrijden.

### Maandelijkse indieningstoeslagrechten per product {#quota-limits}

In de volgende tabel staan de indieningslimieten voor id&#39;s per product en machtigingsniveau. Voor elk product is de maandelijkse limiet de laagste van twee waarden: een vast identificatieplafond of een op percentage gebaseerde drempel die is gekoppeld aan uw gelicentieerde gegevensvolume.

| Product | Beschrijving van rechten | Maandelijkse limiet (Welke lager is) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP of Adobe Journey Optimizer | Zonder &#39;Privacy and Security Shield&#39; of &#39;Healthcare Shield Add-on&#39; | 2.000.000 ID&#39;s of 5% van het adresseerbare publiek |
| Real-Time CDP of Adobe Journey Optimizer | Met privacy- en beveiligingsschild of de invoegtoepassing Gezondheidsschild | 15.000.000 id&#39;s of 10% van het adresseerbare publiek |
| Customer Journey Analytics | Zonder &#39;Privacy and Security Shield&#39; of &#39;Healthcare Shield Add-on&#39; | 2.000.000 ID&#39;s of 100 ID&#39;s per miljoen CJA rijen met rechten |
| Customer Journey Analytics | Met privacy- en beveiligingsschild of de invoegtoepassing Gezondheidsschild | 15.000.000 ID&#39;s of 200 ID&#39;s per miljoen CJA rijen met rechten |

>[!NOTE]
>
>De meeste organisaties zullen lagere maandelijkse grenzen hebben die op hun werkelijk adresseerbare publiek of de rijaanspraken van CJA worden gebaseerd.

>[!NOTE]
>
>De quota zijn opnieuw ingesteld op de eerste dag van elke kalendermaand. Ongebruikte quota **niet** draagt over.

>[!NOTE]
>
>Het gebruik van de quota is gebaseerd op de vergunning gegeven maandelijkse bevoegdheid van uw organisatie voor **voorgelegde herkenningstekens**. De quota&#39;s worden niet door systeemgaranties afgedwongen, maar kunnen worden gecontroleerd en herzien.\
>Het verslag schrapt de capaciteit van de het werkorde is a **gedeelde dienst**. Uw maandelijkse limiet weerspiegelt de hoogste rechten voor Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics en alle toepasselijke add-ons voor schild.

### Tijdlijnen verwerken voor id-verzending {#sla-processing-timelines}

Na verzending worden werkorders voor het verwijderen van records in een wachtrij geplaatst en verwerkt op basis van uw machtigingsniveau.

| Beschrijving van product en rechten | Duur wachtrij | Maximale verwerkingstijd (SLA) |
|------------------------------------|---------------------|-------------------------------|
| Zonder &#39;Privacy and Security Shield&#39; of &#39;Healthcare Shield Add-on&#39; | Tot 15 dagen | 30 dagen |
| Met privacy- en beveiligingsschild of de invoegtoepassing Gezondheidsschild | Doorgaans 24 uur | 15 dagen |

Als uw organisatie hogere limieten nodig heeft, neemt u contact op met uw Adobe-vertegenwoordiger voor een beoordeling van uw rechten.

>[!TIP]
>
>Om uw huidige quotagebruik of machtigingsrij te controleren, zie de [&#x200B; gids van de de verwijzingsverwijzing van de Quota &#x200B;](../api/quota.md).

## Werkorders voor het verwijderen van records weergeven {#list}

Haal een gepagineerde lijst op van werkorders voor het verwijderen van records voor bewerkingen voor gegevenshygiëne in uw organisatie. De resultaten van de filter gebruikend vraagparameters. Elk werkorderrecord bevat het actietype (zoals `identity-delete` ), de status, de gerelateerde gegevensset en gebruikersgegevens en metagegevens van de audit.

**API formaat**

```http
GET /workorder
```

In de volgende tabel worden de queryparameters beschreven die beschikbaar zijn voor het opnemen van recordverwijderwerkorders.

| Query-parameter | Beschrijving |
| --------------- | ------------|
| `search` | Niet-hoofdlettergevoelige gedeeltelijke overeenkomst (vervangingsonderzoek) over gebieden: auteur, displayName, description, of datasetName. Komt ook exact overeen met de vervaldatum-id. |
| `type` | Filterresultaten op basis van het type werkorder (bijvoorbeeld `identity-delete`). |
| `status` | Lijst met door komma&#39;s gescheiden statussen van werkorders. Statuswaarden zijn hoofdlettergevoelig.<br> Enum: `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | Zoek de persoon die de werkorder (of de oorspronkelijke maker) het laatst heeft bijgewerkt. Accepteert letterlijke tekens of SQL-patronen. |
| `displayName` | Niet-hoofdlettergevoelige overeenkomst voor de weergavenaam van de werkorder. |
| `description` | Niet-hoofdlettergevoelige overeenkomst voor een beschrijving van de werkorder. |
| `workorderId` | Exacte overeenkomst voor werkorder-id. |
| `sandboxName` | Exacte overeenkomst voor naam van sandbox die in de aanvraag wordt gebruikt, of gebruik `*` om alle sandboxen op te nemen. |
| `fromDate` | Filteren op werkorders die op of na deze datum zijn gemaakt. `toDate` moet worden ingesteld. |
| `toDate` | Filteren op werkorders die vóór of op deze datum zijn gemaakt. `fromDate` moet worden ingesteld. |
| `filterDate` | Retourneert alleen werkorders die op deze datum zijn gemaakt, bijgewerkt of gewijzigd. |
| `page` | Pagina-index die moet worden geretourneerd (begint bij 0). |
| `limit` | Maximale resultaten per pagina (1-100, standaard: 25). |
| `orderBy` | Sorteervolgorde voor resultaten. Gebruik het voorvoegsel `+` of `-` voor oplopend/aflopend. Voorbeeld: `orderBy=-datasetName` . |
| `properties` | Door komma&#39;s gescheiden lijst met extra velden die per resultaat moeten worden opgenomen. Optioneel. |


**Verzoek**

Met de volgende aanvraag worden alle voltooide werkorders voor het verwijderen van records opgehaald, met een maximum van twee per pagina:

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een gepagineerde lijst van verslag terug schrapt werkorden.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

In de volgende tabel worden de eigenschappen in het antwoord beschreven.

| Eigenschap | Beschrijving |
| --- | --- |
| `results` | Array met recordverwijderwerkorderobjecten. Elk object bevat de onderstaande velden. |
| `workorderId` | De unieke id voor de werkvolgorde voor het verwijderen van records. |
| `orgId` | Uw unieke organisatie-id. |
| `bundleId` | De unieke id van de bundel die deze record bevat, verwijdert de werkvolgorde. Bundling staat veelvoudige schrappingsorden toe om samen door stroomafwaartse diensten worden gegroepeerd en worden verwerkt. |
| `action` | Het handelingstype dat is aangevraagd in de werkorder. |
| `createdAt` | De tijdstempel op het moment dat de werkorder werd gemaakt. |
| `updatedAt` | De tijdstempel op het moment dat de werkorder voor het laatst is bijgewerkt. |
| `operationCount` | Het aantal bewerkingen dat is opgenomen in de werkorder. |
| `targetServices` | Lijst met doelservices voor de werkorder. |
| `status` | Huidige status van de werkorder. Mogelijke waarden zijn: `received`, `validated`, `submitted`, `ingested`, `completed` en `failed` . |
| `createdBy` | De e-mail en id van de gebruiker die de werkorder heeft gemaakt. |
| `datasetId` | De unieke identificatie voor de dataset verbonden aan de het werkorde. Als het verzoek op alle datasets van toepassing is, zal dit gebied aan ALLE worden geplaatst. |
| `datasetName` | De naam van de dataset verbonden aan de het werkorde. |
| `displayName` | Een door de mens leesbaar label voor de werkorder. |
| `description` | Een beschrijving van het doel van de werkorder. |
| `total` | Het totale aantal werkorders voor het verwijderen van records dat overeenkomt met de query. |
| `count` | Aantal werkorders voor het verwijderen van records op de huidige pagina. |
| `_links` | Paginering- en navigatiekoppelingen |
| `next` | Object met `href` (tekenreeks) en `templated` (Boolean) voor de volgende pagina. |
| `page` | Object met `href` (tekenreeks) en `templated` (Boolean) voor paginanavigatie. |

{style="table-layout:auto"}

## Een werkorder voor het verwijderen van records maken {#create}

Om verslagen te schrappen verbonden aan één of meerdere identiteiten van één enkele dataset of alle datasets, doe een POST- verzoek aan het `/workorder` eindpunt.

Werkorders worden asynchroon verwerkt en verschijnen na verzending in de lijst met werkorders.

>[!TIP]
>
>Elk verslag schrapt werkorde die door API wordt voorgelegd kan tot **100.000 identiteiten** omvatten. U kunt zo veel mogelijk identiteiten per aanvraag indienen om de efficiëntie te maximaliseren. Vermijd inzendingen met een laag volume, zoals werkorders met één id.

**API formaat**

```http
POST /workorder
```

>[!NOTE]
>
>U kunt verslagen van datasets slechts schrappen de waarvan bijbehorend schema XDM een primaire identiteit of identiteitskaart bepaalt.

>[!IMPORTANT]
>
>Het verslag schrapt werkorden handelt exclusief op het **primaire identiteitsgebied**. De volgende beperkingen zijn van toepassing:
>
>- **secundaire identiteiten worden niet gescand.** Als een dataset veelvoudige identiteitsgebieden bevat, slechts wordt de primaire identiteit gebruikt voor aanpassing. Records kunnen niet worden aangeroepen of verwijderd op basis van niet-primaire identiteiten.
>- **Verslagen zonder een bevolkte primaire identiteit worden overgeslagen.** Als een record geen metagegevens van de primaire identiteit heeft ingevuld, kan het niet worden verwijderd.
>- **Gegevens die vóór identiteitsconfiguratie worden opgenomen zijn niet verkiesbaar.** Als het primaire identiteitsveld na gegevensinvoer aan een schema is toegevoegd, kunnen eerder opgenomen records niet worden verwijderd via werkorders voor het verwijderen van records.

>[!NOTE]
>
>Als u probeert om een verslag tot stand te brengen schrap het werkorde voor een dataset die reeds een actieve afloop heeft, keert het verzoek HTTP 400 (Onjuist Verzoek) terug.Een actieve vervaldatum is om het even welke geplande schrapping die nog niet heeft voltooid.

**Verzoek**

Het volgende verzoek schrapt alle verslagen verbonden aan gespecificeerde e-mailadressen van een bepaalde dataset.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

In de volgende tabel worden de eigenschappen beschreven voor het maken van een werkvolgorde voor het verwijderen van records.

| Eigenschap | Beschrijving |
| --- | --- |
| `displayName` | Een leesbaar label voor deze record waarmee de werkvolgorde wordt verwijderd. |
| `description` | Een beschrijving van de werkvolgorde voor het verwijderen van records. |
| `action` | De gevraagde actie voor het verslag schrapt werkorde. Gebruik `delete_identity` om records te verwijderen die aan een bepaalde identiteit zijn gekoppeld. |
| `datasetId` | De unieke id voor de gegevensset. Gebruik dataset ID voor een specifieke dataset, of `ALL` om alle datasets te richten. Datasets moeten een primaire identiteit of een identiteitskaart hebben. Als er een identiteitskaart bestaat, is deze aanwezig als een veld op hoofdniveau met de naam `identityMap` .<br> Merk op dat een datasetrij vele identiteiten in zijn identiteitskaart kan hebben, maar slechts één kan als primair worden gemerkt. `"primary": true` moet worden opgenomen om ervoor te zorgen dat de `id` overeenkomt met een primaire identiteit. |
| `namespacesIdentities` | Een serie van voorwerpen, elk die:<br> bevatten<ul><li> `namespace`: Een object met een eigenschap `code` die de naamruimte voor identiteit opgeeft (bijvoorbeeld &quot;email&quot;).</li><li> `IDs`: een array met identiteitswaarden die voor deze naamruimte moeten worden verwijderd.</li></ul>Naamruimten bieden context voor identiteitsgegevens. U kunt de standaardnaamruimten van Experience Platform gebruiken of zelf naamruimten maken. Meer leren, zie de [&#x200B; documentatie van identiteitsnamespace &#x200B;](../../identity-service/features/namespaces.md) en de [&#x200B; Dienst API specificatie van de Identiteit &#x200B;](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

**Reactie**

Een succesvolle reactie keert de details van het nieuwe verslag terug schrapt werkorde.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

In de volgende tabel worden de eigenschappen in het antwoord beschreven.

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De unieke id voor de werkvolgorde voor het verwijderen van records. Gebruik deze waarde om de status of details van de verwijdering op te zoeken. |
| `orgId` | Uw unieke organisatie-id. |
| `bundleId` | De unieke id van de bundel die deze record bevat, verwijdert de werkvolgorde. Bundling staat veelvoudige schrappingsorden toe om samen door stroomafwaartse diensten worden gegroepeerd en worden verwerkt. |
| `action` | Het handelingstype verzocht in het verslag schrapt werkorde. |
| `createdAt` | De tijdstempel op het moment dat de werkorder werd gemaakt. |
| `updatedAt` | De tijdstempel op het moment dat de werkorder voor het laatst is bijgewerkt. |
| `operationCount` | Het aantal bewerkingen dat is opgenomen in de werkorder. |
| `targetServices` | Een lijst met doelservices voor het verwijderen van records. |
| `status` | Huidige status van de record: werkorder verwijderen. |
| `createdBy` | De e-mail en id van de gebruiker die de recordwerkorder heeft gemaakt, worden verwijderd. |
| `datasetId` | De unieke id voor de gegevensset. Als het verzoek voor alle datasets is, zal de waarde aan `ALL` worden geplaatst. |
| `datasetName` | De naam van de dataset voor dit verslag schrapt werkorde. |
| `displayName` | Een door mensen leesbaar label voor de werkvolgorde voor het verwijderen van records. |
| `description` | Een beschrijving van de werkvolgorde voor het verwijderen van records. |

{style="table-layout:auto"}

>[!NOTE]
>
>De handelingseigenschap voor recordverwijderwerkorders is momenteel `identity-delete` in API-reacties. Als de API verandert om een andere waarde te gebruiken (zoals `delete_identity`), wordt deze documentatie dienovereenkomstig bijgewerkt.

## ID-lijsten converteren naar JSON voor aanvragen voor het verwijderen van records

Als u een werkvolgorde voor het verwijderen van records wilt maken vanuit CSV-, TSV- of TXT-bestanden met id&#39;s, kunt u conversiescripts gebruiken om de vereiste JSON-nuttige ladingen voor het `/workorder` -eindpunt te maken. Deze aanpak is vooral handig wanneer u met bestaande gegevensbestanden werkt. Voor gebruiksklare manuscripten en uitvoerige instructies, bezoek de [&#x200B; csv-aan-gegeven-hygiëne bewaarplaats GitHub &#x200B;](https://github.com/perlmonger42/csv-to-data-hygiene).

### JSON-payloads genereren

De volgende voorbeelden van basscript tonen hoe u de conversiescripts in Python of Ruby kunt uitvoeren:

>[!BEGINTABS]

>[!TAB  Voorbeeld om manuscript Python in werking te stellen ]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.py sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!TAB Voorbeeld om Ruby manuscript  in werking te stellen]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.rb sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!ENDTABS]

In de onderstaande tabel worden de parameters in de basscripts beschreven.

| Parameter | Beschrijving |
| ---           | ---     |
| `verbose` | Brede uitvoer inschakelen. |
| `column` | De index (op 1 gebaseerd) of koptekstnaam van de kolom die de identiteitswaarden bevat die moeten worden verwijderd. Wordt standaard ingesteld op de eerste kolom als deze niet is opgegeven. |
| `namespace` | Een object met een eigenschap `code` die de naamruimte van de identiteit opgeeft (bijvoorbeeld &#39;email&#39;). |
| `dataset-id` | De unieke identificatie voor de dataset verbonden aan de het werkorde. Als het verzoek op alle datasets van toepassing is, zal dit gebied aan `ALL` worden geplaatst. |
| `description` | Een beschrijving van de werkvolgorde voor het verwijderen van records. |
| `output-dir` | De map voor het schrijven van de JSON-uitvoerlading. |

{style="table-layout:auto"}

In het onderstaande voorbeeld ziet u een JSON-laadbewerking die is omgezet vanuit een CSV-, TSV- of TXT-bestand. Deze bevat records die zijn gekoppeld aan de opgegeven naamruimte en wordt gebruikt om records te verwijderen die worden geïdentificeerd door e-mailadressen.

```json
{
  "action": "delete_identity",
  "datasetId": "66f4161cc19b0f2aef3edf10",
  "displayName": "output/sample-big-001.json",
  "description": "a simple sample",
  "identities": [
    {
      "namespace": {
        "code": "email"
      },
      "id": "1"
    },
    {
      "namespace": {
        "code": "email"
      },
      "id": "2"
    }
  ]
}
```

In de volgende tabel worden de eigenschappen in de JSON-payload beschreven.

| Eigenschap | Beschrijving |
| ---          | ---     |
| `action` | De gevraagde actie voor het verslag schrapt werkorde. Automatisch ingesteld op `delete_identity` door het conversiescript. |
| `datasetId` | De unieke id voor de gegevensset. |
| `displayName` | Een leesbaar label voor deze record waarmee de werkvolgorde wordt verwijderd. |
| `description` | Een beschrijving van de werkvolgorde voor het verwijderen van records. |
| `identities` | Een serie van voorwerpen, elk die:<br> bevatten<ul><li> `namespace`: Een object met een eigenschap `code` die de naamruimte voor identiteit opgeeft (bijvoorbeeld &#39;email&#39;).</li><li> `id`: De identiteitswaarde die voor deze naamruimte moet worden verwijderd.</li></ul> |

{style="table-layout:auto"}

### Verzend de gegenereerde JSON-gegevens naar het eindpunt van `/workorder`

Om een verzoek voor te leggen, volg de instructies in [&#x200B; creeer een verslag schrapt werkorde &#x200B;](#create) sectie. Zorg ervoor dat u de omgezette JSON-payload als de aanvraaginstantie (`-d`) gebruikt wanneer u uw `curl` POST-aanvraag naar het API-eindpunt `/workorder` verzendt.

## Gegevens ophalen voor een specifieke werkorder voor het verwijderen van records {#lookup}

U kunt informatie voor een specifieke werkorder voor het verwijderen van records ophalen door een GET-aanvraag in te dienen bij `/workorder/{WORKORDER_ID}` . De reactie omvat actietype, status, bijbehorende dataset en gebruikersinformatie, en controlemetagegevens.

**API formaat**

```http
GET /workorder/{WORKORDER_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{WORK_ORDER_ID}` | De unieke id voor de werkvolgorde voor het verwijderen van records die u opzoekt. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert de details van de opgegeven werkvolgorde voor het verwijderen van records.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

In de volgende tabel worden de eigenschappen in het antwoord beschreven.

| Eigenschap | Beschrijving |
| --- | --- |
| `workorderId` | De unieke id voor de werkvolgorde voor het verwijderen van records. |
| `orgId` | De unieke id van uw organisatie. |
| `bundleId` | De unieke id van de bundel die deze record bevat, verwijdert de werkvolgorde. Bundling staat veelvoudige schrappingsorden toe om samen door stroomafwaartse diensten worden gegroepeerd en worden verwerkt. |
| `action` | Het handelingstype verzocht in het verslag schrapt werkorde. |
| `createdAt` | De tijdstempel op het moment dat de werkorder werd gemaakt. |
| `updatedAt` | De tijdstempel op het moment dat de werkorder voor het laatst is bijgewerkt. |
| `operationCount` | Het aantal bewerkingen dat is opgenomen in de werkorder. |
| `targetServices` | Een lijst van doeldiensten die door dit verslag worden beïnvloed schrapt werkorde. |
| `status` | De huidige status van de record verwijdert de werkvolgorde. |
| `createdBy` | De e-mail en id van de gebruiker die de recordwerkorder heeft gemaakt, worden verwijderd. |
| `datasetId` | De unieke identificatie voor de dataset verbonden aan de het werkorde. |
| `datasetName` | De naam van de dataset verbonden aan de het werkorde. |
| `displayName` | Een door mensen leesbaar label voor de werkvolgorde voor het verwijderen van records. |
| `description` | Een beschrijving van de werkvolgorde voor het verwijderen van records. |

## De werkvolgorde voor het verwijderen van records bijwerken

Werk de `name` en `description` voor een recordverwijderwerkorder bij door een PUT-aanvraag in te dienen bij het `/workorder/{WORKORDER_ID}` -eindpunt.

**API formaat**

```http
PUT /workorder/{WORKORDER_ID}
```

In de volgende tabel wordt de parameter voor deze aanvraag beschreven.

| Parameter | Beschrijving |
| --- | --- |
| `{WORK_ORDER_ID}` | De unieke id voor de werkvolgorde voor het verwijderen van records die u wilt bijwerken. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

In de volgende tabel worden de eigenschappen beschreven die u kunt bijwerken.

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | Het bijgewerkte leesbare label voor de werkvolgorde voor het verwijderen van records. |
| `description` | De bijgewerkte beschrijving voor de werkvolgorde voor het verwijderen van records. |

{style="table-layout:auto"}

**Reactie**

Een geslaagde reactie retourneert de bijgewerkte aanvraag voor de werkorder.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
  "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | De unieke id voor de werkvolgorde voor het verwijderen van records. |
| `orgId` | De unieke id van uw organisatie. |
| `bundleId` | De unieke id van de bundel die deze record bevat, verwijdert de werkvolgorde. Bundling staat veelvoudige schrappingsorden toe om samen door stroomafwaartse diensten worden gegroepeerd en worden verwerkt. |
| `action` | Het handelingstype verzocht in het verslag schrapt werkorde. |
| `createdAt` | De tijdstempel op het moment dat de werkorder werd gemaakt. |
| `updatedAt` | De tijdstempel op het moment dat de werkorder voor het laatst is bijgewerkt. |
| `operationCount` | Het aantal bewerkingen dat is opgenomen in de werkorder. |
| `targetServices` | Een lijst van doeldiensten die door dit verslag worden beïnvloed schrapt werkorde. |
| `status` | De huidige status van de record verwijdert de werkvolgorde. Mogelijke waarden zijn: `received`, `validated`, `submitted`, `ingested`, `completed` en `failed` . |
| `createdBy` | De e-mail en id van de gebruiker die de recordwerkorder heeft gemaakt, worden verwijderd. |
| `datasetId` | De unieke id voor de gegevensset die is gekoppeld aan de werkvolgorde voor het verwijderen van records. |
| `datasetName` | De naam van de dataset verbonden aan het verslag schrapt werkorde. |
| `displayName` | Een door mensen leesbaar label voor de werkvolgorde voor het verwijderen van records. |
| `description` | Een beschrijving van de werkvolgorde voor het verwijderen van records. |
| `productStatusDetails` | Een array met de huidige status van downstreamprocessen voor de aanvraag. Elk object bevat:<ul><li>`productName`: De naam van de downstreamservice.</li><li>`productStatus`: De huidige verwerkingsstatus van de downstreamservice.</li><li>`createdAt`: De tijdstempel op het moment dat de service de meest recente status heeft gepost.</li></ul>Deze eigenschap is beschikbaar nadat de werkorder is ingediend bij downstreamservices om te beginnen met de verwerking. |

{style="table-layout:auto"}
