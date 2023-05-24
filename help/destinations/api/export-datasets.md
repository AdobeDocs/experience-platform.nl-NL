---
solution: Experience Platform
title: (Bèta) de datasets van de uitvoer door de Dienst API van de Stroom te gebruiken
description: Leer hoe te om de Dienst API van de Stroom te gebruiken om datasets naar uitgezochte bestemmingen uit te voeren.
type: Tutorial
exl-id: f23a4b22-da04-4b3c-9b0c-790890077eaa
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3333'
ht-degree: 0%

---

# (Bèta) de datasets van de uitvoer door te gebruiken [!DNL Flow Service API]

>[!IMPORTANT]
>
>* De functionaliteit om datasets uit te voeren is momenteel in Bèta en niet beschikbaar aan alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.
>* Deze bètafunctionaliteit ondersteunt de export van gegevens van de eerste generatie, zoals gedefinieerd in de Real-time Customer Data Platform [productbeschrijving](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
>* Deze functionaliteit is beschikbaar voor klanten die het Real-Time CDP Premier of Ultimate-pakket hebben aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.


In dit artikel wordt uitgelegd welke workflow is vereist voor het gebruik van de [!DNL Flow Service API] om te exporteren [gegevenssets](/help/catalog/datasets/overview.md) van Adobe Experience Platform naar uw voorkeurslocatie voor cloudopslag, zoals [!DNL Amazon S3], SFTP-locaties, of [!DNL Google Cloud Storage].

>[!TIP]
>
>U kunt het gebruikersinterface van het Experience Platform ook gebruiken om datasets uit te voeren. Lees de [UI-zelfstudie voor het exporteren van gegevenssets](/help/destinations/ui/export-datasets.md) voor meer informatie .

## Ondersteunde doelen {#supported-destinations}

Momenteel, kunt u datasets naar de bestemmingen van de wolkenopslag uitvoeren die in het schermafbeelding worden benadrukt en hieronder worden vermeld.

![Doelen die de uitvoer van gegevenssets ondersteunen](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Aan de slag {#get-started}

![Overzicht - de stappen om een bestemming tot stand te brengen en datasets uit te voeren](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md): Alle gegevens die met succes in Adobe Experience Platform zijn ingevoerd, blijven behouden in het dialoogvenster [!DNL Data Lake] als datasets. Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat. Datasets bevatten ook metagegevens die verschillende aspecten van de gegevens beschrijven die ze opslaan.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u moet weten om datasets naar de bestemmingen van de wolkenopslag in Platform uit te voeren.

### Vereiste machtigingen {#permissions}

Om datasets uit te voeren, hebt u nodig **[!UICONTROL Manage Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, en **[!UICONTROL Manage and Activate Dataset Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Om ervoor te zorgen dat u de noodzakelijke toestemmingen hebt om datasets uit te voeren en dat de bestemming het uitvoeren van datasets steunt, doorblader de bestemmingscatalogus. Als een doel een **[!UICONTROL Activate]** of **[!UICONTROL Export datasets]** controle, dan hebt u de aangewezen toestemmingen.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste en optionele koppen {#gather-values-headers}

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [Zelfstudie over verificatie van Experience Platforms](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Bronnen in [!DNL Experience Platform] kan worden geïsoleerd naar specifieke virtuele sandboxen. In verzoeken om [!DNL Platform] API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Experience Platform], zie de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

### API-naslagdocumentatie {#api-reference-documentation}

In deze zelfstudie vindt u begeleidende referentiedocumentatie voor alle API-bewerkingen. Zie de [[!DNL Flow Service] - Doelen-API-documentatie op de Adobe Developer-website](https://developer.adobe.com/experience-platform-apis/references/destinations/). We raden u aan deze zelfstudie en de API-naslagdocumentatie parallel te gebruiken.

### Woordenlijst {#glossary}

Voor beschrijvingen van de termen die u in deze API-zelfstudie zult tegenkomen, leest u de [verklarende woordenlijst](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) van de API-naslagdocumentatie.

### Verbindingsspecificaties en stroomspecificaties voor uw gewenste doel verzamelen {#gather-connection-spec-flow-spec}

Alvorens de werkschema te beginnen om een dataset uit te voeren, identificeer de verbindingsspecificatie en stroom specificiteit IDs van de bestemming waarnaar u datasets wilt uitvoeren. Gebruik de onderstaande tabel ter referentie.


| Bestemming | Verbindingsspecificatie | Stroomspecificatie |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style="table-layout:auto"}

U hebt deze id&#39;s nodig om verschillende [!DNL Flow Service] entiteiten. U moet ook naar delen van het dialoogvenster [!DNL Connection Spec] om bepaalde entiteiten in te stellen zodat u de [!DNL Connection Spec] van [!DNL Flow Service APIs]. Zie de voorbeelden hieronder van het terugwinnen van verbindingsspecificaties voor alle bestemmingen in de lijst:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

+++Ophalen [!DNL connection spec] for [!DNL Amazon S3]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwoord**

+++[!DNL Amazon S3] - Verbindingsspecificatie

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Blob Storage]

**Verzoek**

+++Ophalen [!DNL connection spec] for [!DNL Azure Blob Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwoord**

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Verzoek**

+++Ophalen [!DNL connection spec] for [!DNL Azure Data Lake Gen 2(ADLS Gen2])

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwoord**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Verzoek**

+++Ophalen [!DNL connection spec] for [!DNL Data Landing Zone(DLZ)]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwoord**

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Google Cloud Storage]

**Verzoek**

+++Ophalen [!DNL connection spec] for [!DNL Google Cloud Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwoord**

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**Verzoek**

+++Ophalen [!DNL connection spec] voor SFTP

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Antwoord**

+++SFTP - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

Voer de onderstaande stappen uit om een gegevenssetgegevensstroom in te stellen naar een opslaglocatie in de cloud. Voor sommige stappen verschillen de verzoeken en antwoorden tussen de verschillende cloudopslagbestemmingen. In die gevallen, gebruik de lusjes op de pagina om de verzoeken en de reacties terug te winnen specifiek voor de bestemming die u wilt verbinden en datasets uitvoeren naar. Zorg ervoor dat u de juiste [!DNL connection spec] en [!DNL flow spec] voor de bestemming u vormt.

## Een lijst met gegevenssets ophalen {#retrieve-list-of-available-datasets}

![Diagram dat stap 1 in het werkschema van de uitvoerdatasets toont](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

Om een lijst van datasets terug te winnen geschikt voor activering, begin door een API vraag aan het hieronder eindpunt te maken.

>[!BEGINSHADEBOX]

**Verzoek**

+++In aanmerking komende gegevenssets ophalen - Verzoek

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

Merk op dat om in aanmerking komende datasets terug te winnen, [!DNL connection spec] Id die wordt gebruikt in de aanvraag-URL, moet de specificatie-id van de gegevensmeerbronverbinding zijn. `23598e46-f560-407b-88d5-ea6207e49db0`en de twee queryparameters `outputField=datasets` en `outputType=activationDatasets` moet worden gespecificeerd. Alle andere vraagparameters zijn standaarddegenen die door [Catalogusservice-API](https://developer.adobe.com/experience-platform-apis/references/catalog/).

+++

**Antwoord**

+++Gegevenssets ophalen - Reactie

```json
{
    "items": [
        {
            "id": "5ef3e324052581191aa6a466",
            "name": "AAM Authenticated Profiles Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e3259ad2a1191ab7dd7d",
            "name": "AAM Devices Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e325582424191b1beb42",
            "name": "AAM Devices Profile Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328582424191b1beb44",
            "name": "AAM Realtime",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328fe742a191b2b3ea5",
            "name": "AAM Realtime Profile Updates",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        }
    ],
    "pageInfo": {
        "start": 0,
        "end": 4,
        "total": 149,
        "hasNext": true
    }
}
```

+++

>[!ENDSHADEBOX]

Een succesvol antwoord bevat een lijst met gegevenssets die in aanmerking komen voor activering. Deze datasets kunnen worden gebruikt wanneer het construeren van de bronverbinding in de volgende stap.

Voor informatie over de diverse reactieparameters voor elke teruggekeerde dataset, verwijs naar [Documentatie voor ontwikkelaars van de API voor gegevenssets](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets).

## Een bronverbinding maken {#create-source-connection}

![Diagram dat stap 2 in het werkschema van de uitvoerdatasets toont](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

Na het terugwinnen van de lijst van datasets die u wilt uitvoeren, kunt u een bronverbinding tot stand brengen gebruikend die dataset IDs.

>[!BEGINSHADEBOX]

**Verzoek**

+++Bronverbinding maken - Verzoek

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="12,16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
  "name": "Connecting to Data Lake",
  "description": "Data Lake source connection to export datasets",
  "connectionSpec": {
    "id": "23598e46-f560-407b-88d5-ea6207e49db0", // this connection spec ID is always the same for Source Connections
    "version": "1.0"
  },
  "params": {
    "datasets": [ // datasets to activate
      {
        "dataSetId": "5ef3e3259ad2a1191ab7dd7d",
        "name": "AAM Devices Data"
      }
    ]
  }
}'
```

+++



**Antwoord**

+++Bronverbinding maken - Reactie

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

Een geslaagde reactie retourneert de id (`id`) van de nieuwe bronverbinding en een `etag`. Noteer de bron-verbindings-id zoals u deze later nodig hebt wanneer u de gegevensstroom maakt.

Houd er rekening mee dat:

* De bronverbinding die in deze stap wordt gecreeerd moet met een dataflow voor zijn datasets worden verbonden om aan een bestemming te worden geactiveerd. Zie de [een gegevensstroom maken](#create-dataflow) voor informatie over hoe te om een bronverbinding aan een dataflow te verbinden.
* De dataset IDs van een bronverbinding kan niet na verwezenlijking worden gewijzigd. Als u datasets uit een bronverbinding moet toevoegen of verwijderen, moet u een nieuwe bronverbinding tot stand brengen en identiteitskaart van de nieuwe bronverbinding met dataflow verbinden.

## Een basisverbinding (doel) maken {#create-base-connection}

![Diagram dat stap 3 in het werkschema van de uitvoerdatasets toont](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

Een basisverbinding slaat veilig de geloofsbrieven aan uw bestemming op. Afhankelijk van het bestemmingstype, kunnen de geloofsbrieven nodig om tegen die bestemming voor authentiek te verklaren variëren. Om deze authentificatieparameters te vinden, wint eerst terug [!DNL connection spec] voor het gewenste doel zoals beschreven in de sectie [Verbindingsspecificaties en stroomspecificaties verzamelen](#gather-connection-spec-flow-spec) en bekijk dan de `authSpec` van de respons. Verwijs naar de tabbladen hieronder voor de `authSpec` eigenschappen van alle ondersteunde doelen.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] tonen [!DNL auth spec]

De gemarkeerde regel met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, dat extra informatie over verstrekt waar te om de authentificatieparameters in te vinden [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Access Key",
                    "type": "KeyBased",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines auth params required for connecting to amazon-s3",
                        "type": "object",
                        "properties": {
                            "s3AccessKey": {
                                "description": "Access key id",
                                "type": "string",
                                "pattern": "^[A-Z2-7]{20}$"
                            },
                            "s3SecretKey": {
                                "description": "Secret access key for the user account",
                                "type": "string",
                                "format": "password",
                                "pattern": "^[A-Za-z0-9\/\\+]{40}$"
                            }
                        },
                        "required": [
                            "s3SecretKey",
                            "s3AccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB Azure Blob Storage]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] tonen [!DNL auth spec]

De gemarkeerde regel met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, dat extra informatie over verstrekt waar te om de authentificatieparameters in te vinden [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] tonen [!DNL auth spec]

De gemarkeerde regel met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, dat extra informatie over verstrekt waar te om de authentificatieparameters in te vinden [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Data Landing Zone (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] tonen [!DNL auth spec]

>[!NOTE]
>
>De bestemming van de Gebied van Gegevens Landing vereist geen [!DNL auth spec].

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Google Cloud Storage]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] tonen [!DNL auth spec]

De gemarkeerde regel met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, dat extra informatie over verstrekt waar te om de authentificatieparameters in te vinden [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] tonen [!DNL auth spec]

>[!NOTE]
>
>De bestemming SFTP bevat twee afzonderlijke punten in [!DNL auth spec], omdat deze zowel wachtwoord- als SSH-sleutelverificatie ondersteunt.

De gemarkeerde regel met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, dat extra informatie over verstrekt waar te om de authentificatieparameters in te vinden [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

De eigenschappen gebruiken die in de verificatiespecificatie (d.w.z. `authSpec` vanuit de reactie) kunt u een basisverbinding maken met de vereiste referenties, specifiek voor elk doeltype, zoals in de volgende voorbeelden wordt getoond:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

+++[!DNL Amazon S3] - Aanvraag voor basisverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste authentificatiegeloofsbrieven te verkrijgen, verwijs naar [authenticeren naar doel](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) sectie van de Amazon S3 pagina van de bestemmingsdocumentatie.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwoord**

+++[!DNL Amazon S3] Reactie basisverbinding

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob Storage]

**Verzoek**

+++[!DNL Azure Blob Storage] - Aanvraag voor basisverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste authentificatiegeloofsbrieven te verkrijgen, verwijs naar [authenticeren naar doel](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) sectie van de Azure Blob Storage-doeldocumentatiepagina.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwoord**

+++[!DNL Azure Blob Storage] - Basisverbindingsreactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Verzoek**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Aanvraag voor basisverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste authentificatiegeloofsbrieven te verkrijgen, verwijs naar [authenticeren naar doel](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) sectie van de bestemmingsdocumentatiepagina van Azure Data Lake Gen 2 (ADLS Gen2).

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwoord**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Basisverbindingsreactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Verzoek**

+++[!DNL Data Landing Zone(DLZ)] - Aanvraag voor basisverbinding

>[!TIP]
>
>Er zijn geen verificatiereferenties vereist voor de bestemming Landing Zone voor gegevens. Raadpleeg voor meer informatie de [authenticeren naar doel](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) sectie van de de bestemmingsdocumentatiepagina van de Gebied van Gegevens Landing.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection"
}'
```

+++

**Antwoord**

+++[!DNL Data Landing Zone] - Basisverbindingsreactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Verzoek**

+++[!DNL Google Cloud Storage] - Aanvraag voor basisverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste authentificatiegeloofsbrieven te verkrijgen, verwijs naar [authenticeren naar doel](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) op de pagina met doeldocumentatie voor Google Cloud Storage.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwoord**

+++[!DNL Google Cloud Storage] - Basisverbindingsreactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Verzoek**

+++SFTP met wachtwoord - de Verzoek van de Verbinding van de basis

>[!TIP]
>
>Voor informatie over hoe te om de vereiste authentificatiegeloofsbrieven te verkrijgen, verwijs naar [authenticeren naar doel](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) van de pagina van de de bestemmingsdocumentatie van SFTP.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

+++SFTP met SSH-sleutel - Aanvraag voor basisverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste authentificatiegeloofsbrieven te verkrijgen, verwijs naar [authenticeren naar doel](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) van de pagina van de de bestemmingsdocumentatie van SFTP.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**Antwoord**

+++SFTP - De reactie van de basisverbinding

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Noteer de verbinding-id in het antwoord. Deze id is vereist in de volgende stap bij het maken van de doelverbinding.

## Een doelverbinding maken {#create-target-connection}

![Diagram dat stap 4 in het werkschema van uitvoerdatasets toont](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

Daarna, moet u een doelverbinding tot stand brengen die de uitvoerparameters voor uw datasets opslaat. Exportparameters zijn onder andere locatie, bestandsindeling, compressie en andere details. Zie de `targetSpec` eigenschappen verstrekt in de de verbindingsspecificatie van de bestemming om de gesteunde eigenschappen voor elk bestemmingstype te begrijpen. Verwijs naar de tabbladen hieronder voor de `targetSpec` eigenschappen van alle ondersteunde doelen.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] doelverbindingsparameters weergeven

Let op de gemarkeerde regels met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, die extra informatie verstrekken over waar te om te vinden [!DNL target spec] parameters in de verbindingsspecificatie. U kunt ook in het voorbeeld zien waaronder doelparameters *niet* van toepassing op gegevenssetuitvoerbestemmingen.

```json {line-numbers="true" start-line="1" highlight="10,41,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Azure Blob Storage]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] doelverbindingsparameters weergeven

Let op de gemarkeerde regels met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, die extra informatie verstrekken over waar te om te vinden [!DNL target spec] parameters in de verbindingsspecificatie. U kunt ook in het voorbeeld zien waaronder doelparameters *niet* van toepassing op gegevenssetuitvoerbestemmingen.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] doelverbindingsparameters weergeven

Let op de gemarkeerde regels met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, die extra informatie verstrekken over waar te om te vinden [!DNL target spec] parameters in de verbindingsspecificatie. U kunt ook in het voorbeeld zien waaronder doelparameters *niet* van toepassing op gegevenssetuitvoerbestemmingen.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions":{...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Data Landing Zone (DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] doelverbindingsparameters weergeven

Let op de gemarkeerde regels met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, die extra informatie verstrekken over waar te om te vinden [!DNL target spec] parameters in de verbindingsspecificatie. U kunt ook in het voorbeeld zien waaronder doelparameters *niet* van toepassing op gegevenssetuitvoerbestemmingen.

```json {line-numbers="true" start-line="1" highlight="9,21,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
        "targetSpec": { // describes the target connection parameters
            "name": "User based target",
            "type": "UserNamespace",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "properties": {
                    "path": {
                        "title": "Folder path",
                        "description": "Enter the path to your Azure Data Lake Storage folder",
                        "type": "string"
                    },
                    "fileType": {...}, // not applicable to dataset destinations
                    "datasetFileType": {
                        "conditional": {
                            "field": "flowSpec.attributes._workflow",
                            "operator": "CONTAINS",
                            "value": "DATASETS"
                        },
                        "title": "File Type",
                        "description": "Select file format",
                        "type": "string",
                        "enum": [
                            "JSON",
                            "PARQUET"
                        ]
                    },
                    "csvOptions": {...}, // not applicable to dataset destinations
                    "compression": {
                        "title": "Compression format",
                        "description": "Select the desired file compression format.",
                        "type": "string",
                        "enum": [
                            "NONE",
                            "GZIP"
                        ]
                    }
                },
                "required": [
                    "path",
                    "datasetFileType",
                    "compression",
                    "fileType"
                ]
            }
//...
```

+++

>[!TAB Google Cloud Storage]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] doelverbindingsparameters weergeven

Let op de gemarkeerde regels met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, die extra informatie verstrekken over waar te om te vinden [!DNL target spec] parameters in de verbindingsspecificatie. U kunt ook in het voorbeeld zien waaronder doelparameters *niet* van toepassing op gegevenssetuitvoerbestemmingen.

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] doelverbindingsparameters weergeven

Let op de gemarkeerde regels met inline opmerkingen in het dialoogvenster [!DNL connection spec] voorbeeld hieronder, die extra informatie verstrekken over waar te om te vinden [!DNL target spec] parameters in de verbindingsspecificatie. U kunt ook in het voorbeeld zien waaronder doelparameters *niet* van toepassing op gegevenssetuitvoerbestemmingen.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]


Aan de hand van de bovenstaande specificatie kunt u een aanvraag voor een doelverbinding samenstellen die specifiek is voor uw gewenste bestemming voor cloudopslag, zoals weergegeven in de onderstaande tabbladen.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

+++[!DNL Amazon S3] - Aanvraag voor doelverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste doelparameters te verkrijgen, verwijs naar [bestemmingsdetails invullen](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) van de [!DNL Amazon S3] pagina met doeldocumentatie.
>Voor andere ondersteunde waarden van `datasetFileType`Zie de API-naslagdocumentatie.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Beta Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwoord**

+++Target-verbinding - Reactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob Storage]

**Verzoek**

+++[!DNL Azure Blob Storage] - Aanvraag voor doelverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste doelparameters te verkrijgen, verwijs naar [bestemmingsdetails invullen](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) van de [!DNL Azure Blob Storage] pagina met doeldocumentatie.
>Voor andere ondersteunde waarden van `datasetFileType`Zie de API-naslagdocumentatie.


Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Beta Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwoord**

+++Target-verbinding - Reactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Verzoek**

+++[!DNL Azure Blob Storage] - Aanvraag voor doelverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste doelparameters te verkrijgen, verwijs naar [bestemmingsdetails invullen](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) sectie van de Azure [!DNL Data Lake Gen 2(ADLS Gen2)] pagina met doeldocumentatie.
>Voor andere ondersteunde waarden van `datasetFileType`Zie de API-naslagdocumentatie.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwoord**

+++Target-verbinding - Reactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Verzoek**

+++[!DNL Data Landing Zone] - Aanvraag voor doelverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste doelparameters te verkrijgen, verwijs naar [bestemmingsdetails invullen](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) van de [!DNL Data Landing Zone] pagina met doeldocumentatie.
>Voor andere ondersteunde waarden van `datasetFileType`Zie de API-naslagdocumentatie.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwoord**

+++Target-verbinding - Reactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Verzoek**

+++[!DNL Google Cloud Storage] - Aanvraag voor doelverbinding

>[!TIP]
>
>Voor informatie over hoe te om de vereiste doelparameters te verkrijgen, verwijs naar [bestemmingsdetails invullen](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) van de [!DNL Google Cloud Storage] pagina met doeldocumentatie.
>Voor andere ondersteunde waarden van `datasetFileType`Zie de API-naslagdocumentatie.


Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwoord**

+++Target-verbinding - Reactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Verzoek**

+++SFTP - verzoek van de Verbinding van het doel

>[!TIP]
>
>Voor informatie over hoe te om de vereiste doelparameters te verkrijgen, verwijs naar [bestemmingsdetails invullen](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) van de pagina van de de bestemmingsdocumentatie van SFTP.
>Voor andere ondersteunde waarden van `datasetFileType`Zie de API-naslagdocumentatie.

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

**Antwoord**

+++Verbinding van het Doel - Reactie

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Noteer de doel-verbindings-id uit het antwoord. Deze id zal in de volgende stap worden vereist wanneer het creëren van dataflow om datasets uit te voeren.

## Een gegevensstroom maken {#create-dataflow}

![Diagram dat stap 5 in het werkschema van de uitvoerdatasets toont](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

De definitieve stap in de bestemmingsconfiguratie is aan opstelling een dataflow. Een dataflow verbindt eerder gecreeerd entiteiten samen en verstrekt ook opties om het programma van de datasetuitvoer te vormen. Om de gegevensstroom tot stand te brengen, gebruik hieronder de ladingen, afhankelijk van uw gewenste bestemming van de wolkenopslag, en vervang entiteit IDs van vorige stappen.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

+++Gegevensset maken naar [!DNL Amazon S3] doel - verzoek

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "269ba276-16fc-47db-92b0-c1049a3c131f", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. Use "interval": 1 when you select "timeUnit": "day"
        "startTime": 1675901210 // UNIX timestamp start time (in seconds)
    }
}'
```

+++

**Antwoord**

+++Gegevensstroom maken - Reactie

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob Storage]

**Verzoek**

+++Gegevensset maken naar [!DNL Azure Blob Storage] doel - verzoek

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "95bd8965-fc8a-4119-b9c3-944c2c2df6d2", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwoord**

+++Gegevensstroom maken - Reactie

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2 (ADLS Gen2)]

**Verzoek**

+++Gegevensset maken naar [!DNL Azure Data Lake Gen 2(ADLS Gen2)] doel - verzoek

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwoord**

+++Gegevensstroom maken - Reactie

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Data Landing Zone (DLZ)]

**Verzoek**

+++Gegevensset maken naar [!DNL Data Landing Zone] doel - verzoek

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwoord**

+++Gegevensstroom maken - Reactie

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google Cloud Storage]

**Verzoek**

+++Gegevensset maken naar [!DNL Google Cloud Storage] doel - verzoek

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwoord**

+++Gegevensstroom maken - Reactie

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Verzoek**

+++Gegevensset maken gegevensstroom naar SFTP-bestemming - Verzoek

Maak een notitie van de gemarkeerde regels met inline opmerkingen in het aanvraagvoorbeeld, die aanvullende informatie bevatten. Verwijder de inline commentaren in het verzoek wanneer het kopiëren-kleeft van het verzoek in uw terminal van keus.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "354d6aad-4754-46e4-a576-1b384561c440", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "interval": 3, // also supports 6, 9, 12, 24 hour increments
        "timeUnit": "hour",
        "startTime": 1675901210 // UNIX timestamp start time(in seconds)
    }
}'
```

+++

**Antwoord**

+++Gegevensstroom maken - Reactie

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Noteer de Dataflow-id uit het antwoord. Deze id wordt vereist in de volgende stap bij het ophalen van de gegevensstroomuitvoering om de geslaagde export van de gegevensset te valideren.

## De gegevensstroomuitvoering ophalen {#get-dataflow-runs}

![Diagram dat stap 6 in het werkschema van de uitvoerdatasets toont](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

Om de uitvoering van een gegevensstroom te controleren, gebruik Dataflow loops API:

>[!BEGINSHADEBOX]

**Verzoek**

+++Dataflow-uitvoering ophalen - Verzoek

In het verzoek om dataflow looppas terug te winnen, voeg als vraagparameter dataflow identiteitskaart toe die u in de vorige stap verwierf, toen het creëren van dataflow.

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**Antwoord**

+++DataFlow-runtime ophalen

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

U vindt informatie over de [de diverse parameters die door de Dataflow-runtime-API worden geretourneerd](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) in de API-naslagdocumentatie.

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het API-foutbericht voor Experience Platforms. Zie [API-statuscodes](/help/landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](/help/landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van de Platform voor meer informatie over het interpreteren van foutenreacties.

## Volgende stappen {#next-steps}

Door dit leerprogramma te volgen, hebt u met succes Platform met één van uw aangewezen bestemmingen van de de opslagopslag van de partijwolk verbonden en opstelling een dataflow aan de respectieve bestemming om datasets uit te voeren. Zie de volgende pagina&#39;s voor meer informatie, zoals hoe u bestaande gegevensstromen kunt bewerken met de Flow Service API:

* [Overzicht van doelen](../home.md)
* [Overzicht van de doelcatalogus](../catalog/overview.md)
* [Doelgegevens bijwerken met de Flow Service API](../api/update-destination-dataflows.md)
