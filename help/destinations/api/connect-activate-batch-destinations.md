---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Verbinden met batchbestemmingen en gegevens activeren met de Flow Service API
description: Stapsgewijze instructies voor het gebruik van de Flow Service API om een batch-cloudopslag of e-mailmarketingbestemming in Experience Platform te maken en gegevens te activeren
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: 833e38559f7150c579840c69fa2658761fc9472c
workflow-type: tm+mt
source-wordcount: '3435'
ht-degree: 0%

---

# Verbind met op dossier-gebaseerde e-mailmarketing bestemmingen en activeer gegevens gebruikend de Dienst API van de Stroom

>[!IMPORTANT]
> 
>* Om met een bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig.
>
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig.
>
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}
>
>Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Dit leerprogramma toont aan hoe te om de Dienst API van de Stroom te gebruiken om een op dossier-gebaseerde [ e-mail marketing bestemming ](../catalog/email-marketing/overview.md) tot stand te brengen, een dataflow aan uw pas gecreëerde bestemming tot stand te brengen, en gegevens naar uw onlangs gecreeerde bestemming via Csv- dossiers uit te voeren.

>[!TIP]
> 
>Leren hoe te om gegevens aan de bestemmingen van de wolkenopslag te activeren gebruikend de Dienst API van de Stroom, lees het [ specifieke API leerprogramma ](/help/destinations/api/activate-segments-file-based-destinations.md).

In deze zelfstudie wordt in alle voorbeelden de bestemming [!DNL Adobe Campaign] gebruikt, maar de stappen zijn identiek voor op bestanden gebaseerde e-mailmarketingdoelen.

![ Overzicht - de stappen om een bestemming tot stand te brengen en publiek te activeren ](../assets/api/email-marketing/overview.png)

Als u verkiest om het gebruikersinterface van Experience Platform te gebruiken om met een bestemming te verbinden en gegevens te activeren, [ verbind een bestemming ](../ui/connect-destination.md) en [ activeer publieksgegevens aan de 3&rbrace; leerprogramma&#39;s van de partijprofieluitvoer.](../ui/activate-batch-profile-destinations.md)

## Aan de slag {#get-started}

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md) : [!DNL Adobe Experience Platform Segmentation Service] hiermee kunt u een publiek maken in [!DNL Adobe Experience Platform] op basis van uw [!DNL Real-Time Customer Profile] -gegevens.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Experience Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u moet weten om gegevens aan partijbestemmingen in Experience Platform te activeren.

### Vereiste referenties verzamelen {#gather-required-credentials}

Om de stappen in deze zelfstudie te voltooien, zou u de volgende geloofsbrieven klaar moeten hebben, afhankelijk van het type van bestemming dat u verbindt en publiek activeert aan.

* Voor [!DNL Amazon S3] verbindingen: `accessId`, `secretKey`
* Voor [!DNL Amazon S3] verbindingen naar [!DNL Adobe Campaign]: `accessId`, `secretKey`
* Voor SFTP-verbindingen: `domain` , `port` , `username` , `password` of `sshKey` (afhankelijk van de verbindingsmethode met de FTP-locatie)
* Voor [!DNL Azure Blob] verbindingen: `connectionString`

>[!NOTE]
>
>De referenties `accessId` , `secretKey` for [!DNL Amazon S3] -verbindingen en `accessId` , `secretKey` for [!DNL Amazon S3] -verbindingen naar [!DNL Adobe Campaign] zijn identiek.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste en optionele koppen {#gather-values-headers}

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Bronnen in [!DNL Experience Platform] kunnen worden geïsoleerd naar specifieke virtuele sandboxen. In aanvragen voor [!DNL Experience Platform] API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

### API-naslagdocumentatie {#api-reference-documentation}

In deze zelfstudie vindt u begeleidende referentiedocumentatie voor alle API-bewerkingen. Verwijs naar de [ documentatie van de Dienst API van de Stroom op Adobe I/O ](https://www.adobe.io/experience-platform-apis/references/flow-service/). We raden u aan deze zelfstudie en de API-naslagdocumentatie parallel te gebruiken.

## Krijg de lijst van beschikbare bestemmingen {#get-the-list-of-available-destinations}

![ stap overzicht van de stappen van de Bestemming 1 ](../assets/api/batch-destination/step1.png)

Als eerste stap moet u bepalen naar welk doel de gegevens moeten worden geactiveerd. Om met te beginnen, voer een vraag uit om een lijst van beschikbare bestemmingen te verzoeken die u kunt verbinden en publiek activeren aan. Voer het volgende GET verzoek aan het `connectionSpecs` eindpunt uit om een lijst van beschikbare bestemmingen terug te keren:

**API formaat**

```http
GET /connectionSpecs
```

**Verzoek**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Reactie**

Een succesvolle reactie bevat een lijst van beschikbare bestemmingen en hun unieke herkenningstekens (`id`). Sla de waarde op van het doel dat u wilt gebruiken, zoals in verdere stappen wordt vereist. Als u bijvoorbeeld een verbinding wilt maken met [!DNL Adobe Campaign] en een publiek wilt maken, zoekt u het volgende fragment in het antwoord:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

Voor uw verwijzing, bevat de lijst hieronder de verbindingsspecificaties - IDs voor algemeen gebruikte partijbestemmingen:

| Bestemming | Verbinding, specificatie-id |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |

{style="table-layout:auto"}

## Verbinding maken met uw [!DNL Experience Platform] -gegevens {#connect-to-your-experience-platform-data}

![ stap overzicht van de stappen 2 van de Bestemming ](../assets/api/batch-destination/step2.png)

Vervolgens moet u verbinding maken met uw [!DNL Experience Platform] -gegevens, zodat u profielgegevens kunt exporteren en activeren op de gewenste bestemming. Deze bestaat uit twee substappen die hieronder worden beschreven.

1. Eerst, moet u een vraag uitvoeren om toegang tot uw gegevens in [!DNL Experience Platform] toe te staan, door een basisverbinding te vestigen.
2. Dan, gebruikend identiteitskaart van de basisverbinding, voer een andere vraag uit waarin u a *bronverbinding* creeert, die de verbinding aan uw [!DNL Experience Platform] gegevens vestigt.

### Toegang tot uw gegevens toestaan in [!DNL Experience Platform]

**API formaat**

```http
POST /connections
```

**Verzoek**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `name` | Geef een naam op voor de basisverbinding met de Experience Platform [!DNL Profile store] . |
| `description` | U kunt desgewenst een beschrijving voor de basisverbinding opgeven. |
| `connectionSpec.id` | Gebruik identiteitskaart van verbindingsspecificatie voor de [ opslag van het Profiel van Experience Platform ](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie bevat het unieke herkenningsteken van de basisverbinding (`id`). Sla deze waarde op zoals vereist in de volgende stap om de bronverbinding te maken.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Verbinding maken met uw [!DNL Experience Platform] -gegevens {#connect-to-platform-data}

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile store",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `name` | Geef een naam op voor de bronverbinding met de Experience Platform [!DNL Profile store] . |
| `description` | U kunt desgewenst een beschrijving voor de bronverbinding opgeven. |
| `connectionSpec.id` | Gebruik identiteitskaart van verbindingsspecificatie voor de [ opslag van het Profiel van Experience Platform ](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |
| `baseConnectionId` | Gebruik de basisverbindings-id die u in de vorige stap hebt verkregen. |
| `data.format` | `CSV` is momenteel de enige ondersteunde indeling voor het exporteren van bestanden. |

{style="table-layout:auto"}

**Reactie**

Een succesvol antwoord retourneert de unieke id (`id`) voor de nieuwe bronverbinding met [!DNL Profile store] . Dit bevestigt dat u verbinding hebt gemaakt met uw [!DNL Experience Platform] -gegevens. Sla deze waarde op zoals deze in een latere stap wordt vereist.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## Verbinden met batchbestemming {#connect-to-batch-destination}

![ stap overzicht 3 van de stappen van de Bestemming ](../assets/api/batch-destination/step3.png)

In deze stap stelt u een verbinding in met de gewenste opslag van de batchcloud of het gewenste marketingdoel voor e-mail. Deze bestaat uit twee substappen die hieronder worden beschreven.

1. Eerst, moet u een vraag uitvoeren om toegang tot het bestemmingsplatform toe te staan, door vestiging een basisverbinding.
2. Dan, gebruikend identiteitskaart van de basisverbinding, zult u een andere vraag maken waarin u a *doelverbinding* creeert, die de plaats in uw opslagrekening specificeert waar de uitgevoerde gegevensdossiers, evenals het formaat van de gegevens zullen worden geleverd die zullen worden uitgevoerd.

### Toegang tot de batchbestemming toestaan {#authorize-access-to-batch-destination}

**API formaat**

```http
POST /connections
```

**Verzoek**

In de onderstaande aanvraag wordt een basisverbinding met [!DNL Adobe Campaign] -doelen tot stand gebracht. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren ([!DNL Amazon S3] , SFTP [!DNL Azure Blob] ), moet u de juiste `auth` -specificatie behouden en de andere verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "auth": {
        "specName": "S3",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }        
    "auth": {
        "specName": "Azure Blob",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }    
}'
```

Zie de onderstaande voorbeeldverzoeken om verbinding te maken met andere ondersteunde batch-cloudopslag- en e-mailmarketingdoelen.

+++ Voorbeeldverzoek om verbinding te maken met [!DNL Amazon S3] -doelen

In de onderstaande aanvraag wordt een basisverbinding met [!DNL Amazon S3] -doelen tot stand gebracht.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Amazon S3",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "auth": {
        "specName": "Access Key",
        "params": {
            "s3AccessKey": "{AMAZON_S3_ACCESS_KEY}",
            "s3SecretKey": "{AMAZON_S3_SECRET_KEY}"
        }
    }
}'
```

+++

+++ Voorbeeldverzoek om verbinding te maken met [!DNL Azure Blob] -doelen

In de onderstaande aanvraag wordt een basisverbinding met [!DNL Azure Blob] -doelen tot stand gebracht.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Azure Blob",
    "description": "Summer advertising campaign",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "auth": {
        "specName": "ConnectionString",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }
}'
```

+++

+++ Voorbeeldverzoek om verbinding te maken met [!DNL Oracle Eloqua] -doelen

In de onderstaande aanvraag wordt een basisverbinding met [!DNL Oracle Eloqua] -doelen tot stand gebracht. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren, moet u de juiste `auth` -specificatie behouden en de andere gegevens verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Eloqua destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Voorbeeldverzoek om verbinding te maken met [!DNL Oracle Responsys] -doelen

In de onderstaande aanvraag wordt een basisverbinding met [!DNL Oracle Responsys] -doelen tot stand gebracht. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren, moet u de juiste `auth` -specificatie behouden en de andere gegevens verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Responsys destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Voorbeeldverzoek om verbinding te maken met [!DNL Salesforce Marketing Cloud] -doelen

In de onderstaande aanvraag wordt een basisverbinding met [!DNL Salesforce Marketing Cloud] -doelen tot stand gebracht. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren, moet u de juiste `auth` -specificatie behouden en de andere gegevens verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Salesforce Marketing Cloud",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Voorbeeld van een verzoek om verbinding te maken met SFTP met wachtwoorddoelen

In het onderstaande verzoek wordt een basisverbinding met SFTP-bestemmingen tot stand gebracht.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to SFTP with password",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
}'
```

+++

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `name` | Geef een naam op voor de basisverbinding met de batchbestemming. |
| `description` | U kunt desgewenst een beschrijving voor de basisverbinding opgeven. |
| `connectionSpec.id` | Gebruik de verbindingsspecificatie-id voor het gewenste batchdoel. U verwierf dit identiteitskaart in de stap [ krijgt de lijst van beschikbare bestemmingen ](#get-the-list-of-available-destinations). |
| `auth.specname` | Wijst op het authentificatieformaat voor de bestemming. Om te weten te komen specName voor uw bestemming, voer de vraag van a [ GET aan het eindpunt van verbindingsspecificaties ](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) uit, die de verbindingsspecificatie van uw gewenste bestemming verstrekken. Zoek de parameter `authSpec.name` in de reactie. <br> Voor Adobe Campaign-doelen kunt u bijvoorbeeld `S3` , `SFTP with Password` of `SFTP with SSH Key` gebruiken. |
| `params` | Afhankelijk van het doel waarmee u verbinding maakt, moet u verschillende vereiste verificatieparameters opgeven. Voor Amazon S3-verbindingen moet u uw toegangs-id en geheime sleutel opgeven op de opslaglocatie van Amazon S3. <br> om de vereiste parameters voor uw bestemming te weten te komen, voer de vraag van a [ GET aan het eindpunt van verbindingsspecificaties ](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) uit, verstrekkend de verbindingsspecificatie van uw gewenste bestemming. Zoek de parameter `authSpec.spec.required` in de reactie. |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie bevat het unieke herkenningsteken van de basisverbinding (`id`). Sla deze waarde op zoals vereist in de volgende stap om een doelverbinding te maken.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Opslaglocatie en gegevensindeling opgeven {#specify-storage-location-data-format}

[!DNL Adobe Experience Platform] exporteert gegevens voor batch-e-mailmarketing en cloudopslagdoelen in de vorm van [!DNL CSV] -bestanden. In deze stap kunt u het pad in uw opslaglocatie bepalen waar de bestanden worden geëxporteerd.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] splitst de exportbestanden automatisch op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel.
>
>Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking: `filename.csv` , `filename_2.csv` , `filename_3.csv` .

**API formaat**

```http
POST /targetConnections
```

**Verzoek**

In het onderstaande verzoek wordt een doelverbinding met [!DNL Adobe Campaign] -doelen vastgelegd om te bepalen waar de geëxporteerde bestanden op uw opslaglocatie worden aangevoerd. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren, moet u de juiste `params` -specificatie behouden en de andere gegevens verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

Zie de onderstaande voorbeeldaanvragen voor een opslaglocatie voor andere ondersteunde batch-cloudopslag- en e-mailmarketingdoelen.

+++ Voorbeeld van een verzoek om een opslaglocatie voor [!DNL Amazon S3] -doelen in te stellen

In het onderstaande verzoek wordt een doelverbinding met [!DNL Amazon S3] -doelen vastgelegd om te bepalen waar de geëxporteerde bestanden op uw opslaglocatie worden aangevoerd.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Amazon S3",
    "description": "Connection to Amazon S3",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
}'
```

+++

+++ Voorbeeld van een verzoek om een opslaglocatie voor [!DNL Azure Blob] -doelen in te stellen

In het onderstaande verzoek wordt een doelverbinding met [!DNL Azure Blob] -doelen vastgelegd om te bepalen waar de geëxporteerde bestanden op uw opslaglocatie worden aangevoerd.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Azure Blob",
    "description": "Connection to Azure Blob",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
}'
```

+++

+++ Voorbeeld van een verzoek om een opslaglocatie voor [!DNL Oracle Eloqua] -doelen in te stellen

In het onderstaande verzoek wordt een doelverbinding met [!DNL Oracle Eloqua] -doelen vastgelegd om te bepalen waar de geëxporteerde bestanden op uw opslaglocatie worden aangevoerd. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren, moet u de juiste `params` -specificatie behouden en de andere gegevens verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Eloqua",
    "description": "Connection to Oracle Eloqua",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

+++

+++ Voorbeeld van een verzoek om een opslaglocatie voor [!DNL Oracle Responsys] -doelen in te stellen

In het onderstaande verzoek wordt een doelverbinding met [!DNL Oracle Responsys] -doelen vastgelegd om te bepalen waar de geëxporteerde bestanden op uw opslaglocatie worden aangevoerd. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren, moet u de juiste `params` -specificatie behouden en de andere gegevens verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Responsys",
    "description": "Connection to Oracle Responsys",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

+++

+++ Voorbeeld van een verzoek om een opslaglocatie voor [!DNL Salesforce Marketing Cloud] -doelen in te stellen

In het onderstaande verzoek wordt een doelverbinding met [!DNL Salesforce Marketing Cloud] -doelen vastgelegd om te bepalen waar de geëxporteerde bestanden op uw opslaglocatie worden aangevoerd. Afhankelijk van de opslaglocatie waarnaar u bestanden wilt exporteren, moet u de juiste `params` -specificatie behouden en de andere gegevens verwijderen.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Salesforce Marketing Cloud",
    "description": "Connection to Salesforce Marketing Cloud",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

+++

+++ Voorbeeld van een verzoek om een opslaglocatie voor SFTP-doelen in te stellen

In het onderstaande verzoek wordt een doelverbinding met SFTP-doelen vastgelegd om te bepalen waar de geëxporteerde bestanden in uw opslaglocatie worden geland.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for SFTP",
    "description": "Connection to SFTP",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
}'
```

+++


| Eigenschap | Beschrijving |
| --------- | ----------- |
| `name` | Geef een naam op voor de doelverbinding met de batchbestemming. |
| `description` | U kunt desgewenst een beschrijving voor de doelverbinding opgeven. |
| `baseConnectionId` | Gebruik de id van de basisverbinding die u in de bovenstaande stap hebt gemaakt. |
| `connectionSpec.id` | Gebruik de verbindingsspecificatie-id voor het gewenste batchdoel. U verwierf dit identiteitskaart in de stap [ krijgt de lijst van beschikbare bestemmingen ](#get-the-list-of-available-destinations). |
| `params` | Afhankelijk van het doel waarmee u verbinding maakt, moet u verschillende vereiste parameters opgeven voor de opslaglocatie. Voor Amazon S3-verbindingen moet u uw toegangs-id en geheime sleutel opgeven op de opslaglocatie van Amazon S3. <br> om de vereiste parameters voor uw bestemming te weten te komen, voer de vraag van a [ GET aan het eindpunt van verbindingsspecificaties ](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) uit, verstrekkend de verbindingsspecificatie van uw gewenste bestemming. Zoek de parameter `targetSpec.spec.required` in de reactie. |
| `params.mode` | Afhankelijk van de ondersteunde modus voor uw doel moet u hier een andere waarde opgeven. Om de vereiste parameters voor uw bestemming te weten te komen, voer de vraag van a [ GET aan het eindpunt van verbindingsspecificaties ](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec) uit, die de verbindingsspecificatie van uw gewenste bestemming verstrekken. Zoek de parameter `targetSpec.spec.properties.mode.enum` in de reactie en selecteer de gewenste modus. |
| `params.bucketName` | Geef voor S3-verbindingen de naam op van het emmertje waar de bestanden worden geëxporteerd. |
| `params.path` | Geef voor S3-verbindingen het bestandspad op in de opslaglocatie waar de bestanden worden geëxporteerd. |
| `params.format` | `CSV` is momenteel het enige ondersteunde exporttype voor bestanden. |
| `params.includeFileManifest` | *Facultatief*. Ingesteld op `true` om het genereren van manifestbestanden voor uw doel in te schakelen. Wanneer deze optie is ingeschakeld, wordt naast de geëxporteerde gegevensbestanden een manifestbestand gemaakt met metagegevens over de geëxporteerde bestanden. Bekijk a [ steekproef manifestdossier ](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). |

{style="table-layout:auto"}

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) voor de pas gecreëerde doelverbinding aan uw partijbestemming terug. Sla deze waarde op zoals deze in latere stappen wordt vereist.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Een gegevensstroom maken {#create-dataflow}

![ stap overzicht van de stappen van de Bestemming 4 ](../assets/api/batch-destination/step4.png)

Met de flowspecificatie, bronverbinding en doel-verbindings-id&#39;s die u in de vorige stappen hebt verkregen, kunt u nu een gegevensstroom maken tussen de [!DNL Experience Platform] -gegevens en de bestemming waar u gegevensbestanden wilt exporteren. Beschouw deze stap als het construeren van de pijpleiding waardoor de gegevens later tussen [!DNL Experience Platform] en uw gewenste bestemming zullen stromen.

Als u een gegevensstroom wilt maken, voert u een POST-aanvraag uit zoals hieronder wordt weergegeven, terwijl u de hieronder vermelde waarden opgeeft binnen de payload.

**API formaat**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "activate audiences to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate audiences to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `name` | Geef een naam op voor de gegevensstroom die u maakt. |
| `description` | U kunt desgewenst een beschrijving voor de gegevensstroom opgeven. |
| `flowSpec.Id` | Gebruik de flow-specificatie-id voor de batchbestemming waarmee u verbinding wilt maken. Om stroom specifieke identiteitskaart terug te winnen, voer een verrichting van GET op het `flowspecs` eindpunt, zoals aangetoond in de [ stroom specs API verwijzingsdocumentatie ](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec) uit. Zoek in de reactie naar `upsTo` en kopieer de bijbehorende id van de batchbestemming waarmee u verbinding wilt maken. Zoek in Adobe Campaign bijvoorbeeld naar `upsToCampaign` en kopieer de parameter `id` . |
| `sourceConnectionIds` | Gebruik bron identiteitskaart u in de stap [ werd verkregen verbind met uw gegevens van Experience Platform ](#connect-to-your-experience-platform-data). |
| `targetConnectionIds` | Gebruik identiteitskaart van de doelverbinding u in de stap [ werd verkregen verbind met partijbestemming ](#connect-to-batch-destination). |
| `transformations` | In de volgende stap vult u deze sectie met het publiek en de profielkenmerken die moeten worden geactiveerd. |

Voor uw verwijzing, bevat de lijst hieronder de stroom specifieke IDs voor algemeen gebruikte partijbestemmingen:

| Bestemming | Stroom-specificatie-id |
---------|----------|
| Alle cloudopslagbestemmingen ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]) en [!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**Reactie**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom en een `etag` . Noteer beide waarden op dezelfde manier als u ze in de volgende stap nodig hebt om het publiek te activeren en gegevensbestanden te exporteren.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Gegevens activeren naar uw nieuwe bestemming {#activate-data}

![ stap overzicht van de stappen van de Bestemming 5 ](../assets/api/batch-destination/step5.png)

Nadat u alle verbindingen en de gegevensstroom hebt gemaakt, kunt u nu uw profielgegevens activeren op het doelplatform. In deze stap selecteert u welk publiek en welke profielkenmerken u naar het doel wilt exporteren.

U kunt het dossier ook bepalen noemend formaat van de uitgevoerde dossiers en welke attributen als [ deduplicatietoetsen ](../ui/activate-batch-profile-destinations.md#mandatory-keys) of [ verplichte attributen ](../ui/activate-batch-profile-destinations.md#mandatory-attributes) zouden moeten worden gebruikt. In deze stap, kunt u het programma ook bepalen om gegevens naar de bestemming te verzenden.

Als u een publiek naar uw nieuwe bestemming wilt activeren, moet u een JSON PATCH-bewerking uitvoeren, vergelijkbaar met het onderstaande voorbeeld. U kunt veelvoudige publiek en profielattributen in één vraag activeren. Meer over JSON PATCH leren, zie de [ specificatie RFC ](https://tools.ietf.org/html/rfc6902).

**API formaat**

```http
PATCH /flows
```

**Verzoek**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                } 
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "triggerType": "SCHEDULED",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                },   
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `{DATAFLOW_ID}` | Gebruik in de URL de id van de gegevensstroom die u in de vorige stap hebt gemaakt. |
| `{ETAG}` | Krijg `{ETAG}` van de reactie in de vorige stap, [ een dataflow ](#create-dataflow) creëren. De antwoordindeling in de vorige stap heeft escape-aanhalingstekens. U moet de niet-beschermde waarden in de kopbal van het verzoek gebruiken. Zie het onderstaande voorbeeld: <br> <ul><li>Voorbeeld van reactie: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Waarde die u in uw verzoek wilt gebruiken: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> De labelwaarde wordt bijgewerkt bij elke geslaagde update van een gegevensstroom. |
| `{SEGMENT_ID}` | Geef de gebruikers-id op die u naar dit doel wilt exporteren. Om publiek IDs voor het publiek terug te winnen dat u wilt activeren, zie [ een publieksdefinitie ](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) in de verwijzing van Experience Platform API terugwinnen. |
| `{PROFILE_ATTRIBUTE}` | Bijvoorbeeld: `"person.lastName"` |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . Als u een publiek aan een gegevensstroom wilt toevoegen, gebruikt u de bewerking `add` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. Wanneer u een publiek aan een gegevensstroom toevoegt, gebruikt u het pad dat in het voorbeeld is opgegeven. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |
| `id` | Geef de id op van het publiek dat u aan de doelgegevensstroom toevoegt. |
| `name` | *Facultatief*. Geef de naam op van het publiek dat u aan de doelgegevensstroom toevoegt. Dit veld is niet verplicht en u kunt een publiek toevoegen aan de doelgegevensstroom zonder de naam ervan op te geven. |
| `filenameTemplate` | Dit veld bepaalt de bestandsnaamindeling van de bestanden die naar uw doel worden geëxporteerd. <br> De volgende opties zijn beschikbaar: <br> <ul><li>`%DESTINATION_NAME%`: verplicht. De geëxporteerde bestanden bevatten de doelnaam.</li><li>`%SEGMENT_ID%`: verplicht. De geëxporteerde bestanden bevatten de id van het geëxporteerde publiek.</li><li>`%SEGMENT_NAME%`: optioneel. De geëxporteerde bestanden bevatten de naam van het geëxporteerde publiek.</li><li>`DATETIME(YYYYMMdd_HHmmss)` of `%TIMESTAMP%` : optioneel. Selecteer een van deze twee opties voor uw bestanden om de tijd op te nemen waarop deze door Experience Platform worden gegenereerd.</li><li>`custom-text`: optioneel. Vervang deze tijdelijke aanduiding door aangepaste tekst die u aan het einde van de bestandsnamen wilt toevoegen.</li></ul> <br> voor meer informatie over het vormen van dossiernamen, verwijs naar [ vormen dossiernamen ](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) sectie in de de activeringsleerprogramma van partijbestemmingen. |
| `exportMode` | Verplicht. Selecteer `"DAILY_FULL_EXPORT"` of `"FIRST_FULL_THEN_INCREMENTAL"` . Voor meer informatie over de twee opties, verwijs naar [ uitvoer volledige dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) en [ de uitvoer stijgende dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) in het leerprogramma van de de activering van partijbestemmingen. |
| `startDate` | Selecteer de datum waarop het publiek moet beginnen met het exporteren van profielen naar uw bestemming. |
| `frequency` | Verplicht. <br> <ul><li>Voor de exportmodus `"DAILY_FULL_EXPORT"` kunt u `ONCE` , `DAILY` , `WEEKLY` of `MONTHLY` selecteren.</li><li>Voor de exportmodus `"FIRST_FULL_THEN_INCREMENTAL"` kunt u `"DAILY"` , `"EVERY_3_HOURS"` , `"EVERY_6_HOURS"` , `"EVERY_8_HOURS"` en `"EVERY_12_HOURS"` selecteren.</li></ul> |
| `triggerType` | Voor *partijbestemmingen* slechts. Dit veld is alleen vereist wanneer u de modus `"DAILY_FULL_EXPORT"` in de kiezer van `frequency` selecteert. <br> Verplicht. <br> <ul><li>Selecteer `"AFTER_SEGMENT_EVAL"` om de activeringstaak direct uit te voeren nadat de dagelijkse segmentatietaak van de Experience Platform-batch is voltooid. Dit zorgt ervoor dat wanneer de activeringstaak wordt uitgevoerd, de meest recente profielen naar uw bestemming worden uitgevoerd.</li><li>Selecteer `"SCHEDULED"` om de activeringstaak op een vast tijdstip uit te voeren. Dit zorgt ervoor dat Experience Platform-profielgegevens elke dag op hetzelfde tijdstip worden geëxporteerd, maar dat de profielen die u exporteert mogelijk niet de meest actuele zijn, afhankelijk van het feit of de batchsegmentatietaak is voltooid voordat de activeringstaak wordt gestart. Als u deze optie selecteert, moet u ook een `startTime` toevoegen om aan te geven op welk tijdstip in UTC de dagelijkse export moet plaatsvinden.</li></ul> |
| `endDate` | Voor *partijbestemmingen* slechts. Dit veld is alleen vereist wanneer u een publiek toevoegt aan een gegevensstroom in exportdoelen voor batchbestanden, zoals Amazon S3, SFTP of Azure Blob. <br> Niet van toepassing bij het selecteren van `"exportMode":"DAILY_FULL_EXPORT"` en `"frequency":"ONCE"` . <br> Hiermee stelt u de datum in waarop publieksleden stoppen met exporteren naar het doel. |
| `startTime` | Voor *partijbestemmingen* slechts. Dit veld is alleen vereist wanneer u een publiek toevoegt aan een gegevensstroom in exportdoelen voor batchbestanden, zoals Amazon S3, SFTP of Azure Blob. <br> Verplicht. Selecteer het tijdstip waarop bestanden met leden van het publiek moeten worden gegenereerd en geëxporteerd naar uw bestemming. |

{style="table-layout:auto"}

>[!TIP]
>
> Zie [ componenten van de Update van een publiek in een dataflow ](/help/destinations/api/update-destination-dataflows.md#update-segment) leren hoe te om diverse componenten (dossier naammalplaatje, uitvoertijd, etc.) van uitgevoerd publiek bij te werken.

**Reactie**

Zoek naar een 202 Geaccepteerde reactie. Er wordt geen responsorgaan geretourneerd. Om te bevestigen dat het verzoek correct was, zie de volgende stap, [ dataflow ](#validate-dataflow) bevestigen.

## De gegevensstroom valideren {#validate-dataflow}

![ stap overzicht van de stappen van de Bestemming 6 ](../assets/api/batch-destination/step6.png)

Als laatste stap in de zelfstudie moet u controleren of het publiek en de profielkenmerken correct zijn toegewezen aan de gegevensstroom.

Voer de volgende GET-aanvraag uit om dit te valideren:

**API formaat**

```http
GET /flows
```

**Verzoek**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: gebruik de gegevensstroom uit de vorige stap.
* `{ETAG}`: gebruik het label van de vorige stap.

**Reactie**

De geretourneerde reactie moet in de parameter `transformations` het publiek en de profielkenmerken bevatten die u in de vorige stap hebt verzonden. Een sample `transformations` -parameter in de reactie kan er als volgt uitzien:

```json
"transformations":[
   {
      "name":"GeneralTransform",
      "params":{
         "profileSelectors":{
            "selectors":[
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"homeAddress.countryCode",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"homeAddress.countryCode",
                        "destination":"homeAddress.countryCode",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"homeAddress.countryCode",
                        "destinationXdmPath":"homeAddress.countryCode"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.firstName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.firstName",
                        "destination":"person.name.firstName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.firstName",
                        "destinationXdmPath":"person.name.firstName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.lastName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.lastName",
                        "destination":"person.name.lastName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.lastName",
                        "destinationXdmPath":"person.name.lastName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"personalEmail.address",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"personalEmail.address",
                        "destination":"personalEmail.address",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"personalEmail.address",
                        "destinationXdmPath":"personalEmail.address"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"segmentMembership.status",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"segmentMembership.status",
                        "destination":"segmentMembership.status",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"segmentMembership.status",
                        "destinationXdmPath":"segmentMembership.status"
                     }
                  }
               }
            ],
            "mandatoryFields":[
               "person.name.firstName",
               "person.name.lastName"
            ],
            "primaryFields":[
               {
                  "fieldType":"ATTRIBUTE",
                  "attributePath":"personalEmail.address"
               }
            ]
         },
         "segmentSelectors":{
            "selectors":[
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                     "name":"Interested in Mountain Biking",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"DAILY_FULL_EXPORT",
                     "schedule":{
                        "frequency":"ONCE",
                        "startDate":"2021-12-20",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               },
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"25768be6-ebd5-45cc-8913-12fb3f348613",
                     "name":"Loyalty Segment",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                     "schedule":{
                        "frequency":"EVERY_6_HOURS",
                        "startDate":"2021-12-22",
                        "endDate":"2021-12-31",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               }
            ]
         }
      }
   }
]
```

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het Experience Platform API-foutbericht. Verwijs naar [ API statuscodes ](/help/landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](/help/landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform voor meer informatie bij het interpreteren van foutenreacties.

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, hebt u Experience Platform verbonden met een van uw voorkeursbestemmingen voor e-mailmarketing via een bestand en een gegevensstroom ingesteld naar de respectievelijke bestemming om gegevensbestanden te exporteren. De uitgaande gegevens kunnen nu in de bestemming voor e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen worden gebruikt. Zie de volgende pagina&#39;s voor meer informatie, zoals hoe u bestaande gegevensstromen kunt bewerken met de Flow Service API:

* [Overzicht van doelen](../home.md)
* [Overzicht van de doelcatalogus](../catalog/overview.md)
* [Doelgegevens bijwerken met de Flow Service API](../api/update-destination-dataflows.md)
