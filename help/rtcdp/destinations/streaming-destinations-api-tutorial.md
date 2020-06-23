---
keywords: Experience Platform;home;popular topics; API tutorials; streaming destinations API; Real-time CDP
solution: Experience Platform
title: Verbinding maken met streaming doelen en gegevens activeren
topic: tutorial
translation-type: tm+mt
source-git-commit: ed9d6eadeb00db51278ea700f7698a1b5590632f
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 0%

---


# Verbinding maken met streamingdoelen en gegevens activeren in het realtime Platform voor klantgegevens van Adobe met behulp van API&#39;s

>[!NOTE]
>
>De [!DNL Amazon Kinesis] en de [!DNL Azure Event Hubs] bestemmingen in Echte Adobe CDP in tijd zijn momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

Deze zelfstudie laat zien hoe u API-aanroepen kunt gebruiken om verbinding te maken met uw Adobe Experience Platform-gegevens, een verbinding tot stand te brengen met een streamingbestemming voor cloudopslag ([Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) of [Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md)), een dataflow te maken naar uw nieuwe bestemming en gegevens te activeren naar uw nieuwe bestemming.

In deze zelfstudie wordt het [!DNL Amazon Kinesis] doel in alle voorbeelden gebruikt, maar de stappen zijn identiek voor [!DNL Azure Event Hubs].

![Overzicht - de stappen om een het stromen bestemming tot stand te brengen en segmenten te activeren](/help/rtcdp/destinations/assets/flow-prelim.png)

Raadpleeg de zelfstudies voor [Connect a destination](../../rtcdp/destinations/connect-destination.md) en [Activate profielen and segments to a destination](../../rtcdp/destinations/activate-destinations.md) als u liever de gebruikersinterface in CDP in real-time van Adobe gebruikt om verbinding te maken met een doel en gegevens te activeren.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Adobe Experience Platform:

* [XDM-systeem](../../xdm/home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Catalogusservice](../../catalog/home.md): Catalog is het systeem van verslagen voor gegevensplaats en lijn binnen Experience Platform.
* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om gegevens aan het stromen bestemmingen in Echte Adobe CDP te activeren.

### Vereiste referenties verzamelen

Om de stappen in dit leerprogramma te voltooien, zou u de volgende geloofsbrieven klaar moeten hebben, afhankelijk van het type van bestemmingen dat u verbindt en segmenten aan activeert.

* Voor [!DNL Amazon Kinesis] verbindingen: `accessKeyId`, `secretKey`, `region` of `connectionUrl`
* Voor [!DNL Azure Event Hubs] verbindingen: `sasKeyName`, `sasKey`, `namespace`

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

### Waarden verzamelen voor vereiste en optionele koppen {#gather-values}

Om vraag aan Platform APIs te maken, moet u eerst het [authentificatieleerprogramma](/help/tutorials/authentication.md)voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

De middelen in Experience Platform kunnen aan specifieke virtuele zandbakken worden geïsoleerd. In aanvragen voor Platform-API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!Nofferte]
>Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Experience Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

### Documentatie voor de wagenbak {#swagger-docs}

In deze zelfstudie in Swagger vindt u begeleidende referentiedocumentatie voor alle API-aanroepen. Zie de documentatie van de [Flow Service API op Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). We raden u aan deze zelfstudie en de documentatiepagina van Swagger parallel te gebruiken.

## Hiermee wordt de lijst met beschikbare streamingdoelen opgehaald {#get-the-list-of-available-streaming-destinations}

![Overzicht doelstappen 1](/help/rtcdp/destinations/assets/step1-create-streaming-destination-api.png)

Als eerste stap moet u bepalen naar welke streamingbestemming de gegevens moeten worden geactiveerd. Om met te beginnen, voer een vraag uit om een lijst van beschikbare bestemmingen te verzoeken die u segmenten kunt verbinden en activeren aan. Voer het volgende GET verzoek aan het `connectionSpecs` eindpunt uit om een lijst van beschikbare bestemmingen terug te keren:

**API-indeling**

```http
GET /connectionSpecs
```

**Verzoek**

```
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Antwoord**

Een succesvolle reactie bevat een lijst met beschikbare bestemmingen en hun unieke herkenningstekens (`id`). Sla de waarde op van het doel dat u wilt gebruiken, zoals in verdere stappen wordt vereist. Als u bijvoorbeeld segmenten wilt verbinden en leveren aan [!DNL Amazon Kinesis] of [!DNL Azure Event Hubs], zoekt u het volgende fragment in de reactie:

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Verbinden met uw Experience Platform gegevens {#connect-to-your-experience-platform-data}

![Overzicht doelstappen 2](/help/rtcdp/destinations/assets/step2-create-streaming-destination-api.png)

Vervolgens moet u verbinding maken met de gegevens van uw Experience Platform, zodat u profielgegevens kunt exporteren en activeren op de gewenste bestemming. Deze bestaat uit twee substappen die hieronder worden beschreven.

1. Eerst, moet u een vraag uitvoeren om toegang tot uw gegevens in Experience Platform toe te staan, door opstelling een basisverbinding.
2. Dan, gebruikend identiteitskaart van de basisverbinding, zult u een andere vraag maken waarin u een bronverbinding creeert, die de verbinding aan uw gegevens van het Experience Platform vestigt.


### Toegang tot uw gegevens in Experience Platform toestaan

**API-indeling**

```http
POST /connections
```

**Verzoek**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME} \
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


* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsSpatiespecificatieidentiteitskaart voor de Verenigde Dienst van het Profiel - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwoord**

Een geslaagde reactie bevat de unieke id (`id`) van de basisverbinding. Sla deze waarde op zoals vereist in de volgende stap om de bronverbinding te maken.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Verbinden met uw Experience Platform gegevens

**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Gebruik de id die u in de vorige stap hebt gekregen.
* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsSpatiespecificatieidentiteitskaart voor de Verenigde Dienst van het Profiel - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) voor de pas gecreëerde bronverbinding aan de Verenigde Dienst van het Profiel terug. Hiermee bevestigt u dat u verbinding hebt gemaakt met de gegevens van uw Experience Platform. Sla deze waarde op zoals deze in een latere stap wordt vereist.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Verbinding maken met streamingdoel {#connect-to-streaming-destination}

![Overzicht doelstappen 3](/help/rtcdp/destinations/assets/step3-create-streaming-destination-api.png)

In deze stap stelt u een verbinding in met uw gewenste streamingdoel. Deze bestaat uit twee substappen die hieronder worden beschreven.

1. Eerst, moet u een vraag uitvoeren om toegang tot de het stromen bestemming toe te staan, door opstelling een basisverbinding.
2. Vervolgens doet u met de id van de basisverbinding een volgende aanroep waarin u een doelverbinding maakt. Hiermee geeft u in uw opslagaccount de locatie op waar de geëxporteerde gegevens worden geleverd en de indeling van de gegevens die worden geëxporteerd.

### Toegang tot de streamingbestemming autoriseren

**API-indeling**

```http
POST /connections
```

**Verzoek**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "your company's holiday campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsSpeciaal identiteitskaart u in de stap verkrijgt [krijgt de lijst van beschikbare bestemmingen](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: Vul de naam van uw streaming bestemming in, bijvoorbeeld: `Amazon Kinesis authentication credentials` of `Azure Event Hubs authentication credentials`.
* `{ACCESS_ID}`: *Voor Amazon Kinesis-verbindingen.* Uw toegangs-id voor de opslaglocatie van Amazon Kinesis.
* `{SECRET_KEY}`: *Voor Amazon Kinesis-verbindingen.* Uw geheime sleutel voor uw opslaglocatie van Amazon Kinesis.
* `{REGION}`: *Voor Amazon Kinesis-verbindingen.* Het gebied in uw Amazon Kinesis-account waar Adobe Real-time CDP uw gegevens streamt.
* `{SAS_KEY_NAME}`: *Voor Azure Event Hubs-verbindingen.* Vul uw SAS-sleutelnaam in. Meer informatie over verificatie [!DNL Azure Event Hubs] met SAS-toetsen vindt u in de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* `{SAS_KEY}`: *Voor Azure Event Hubs-verbindingen.* Vul uw SAS-sleutel in. Meer informatie over verificatie [!DNL Azure Event Hubs] met SAS-toetsen vindt u in de documentatie [van](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* `{EVENT_HUB_NAMESPACE}`: *Voor Azure Event Hubs-verbindingen.* Vul de Azure Event Hubs-naamruimte in waar Adobe Real-time CDP uw gegevens streamt. Voor meer informatie, zie [Create een de hubs van de Gebeurtenis namespace](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) in de documentatie van Microsoft.

**Antwoord**

Een geslaagde reactie bevat de unieke id (`id`) van de basisverbinding. Sla deze waarde op zoals vereist in de volgende stap om een doelverbinding te maken.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Opslaglocatie en gegevensindeling opgeven

**API-indeling**

```http
POST /targetConnections
```

**Verzoek**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnection": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Gebruik de basisverbindings-id die u in de bovenstaande stap hebt verkregen.
* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsspecificatie u in de stap verkrijgt [krijgt de lijst van beschikbare bestemmingen](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *Voor Amazon Kinesis-verbindingen.* Geef de naam van uw bestaande gegevensstroom op in uw Amazon Kinesis-account. Adobe Real-time CDP exporteert gegevens naar deze stream.
* `{REGION}`: *Voor Amazon Kinesis-verbindingen.* Het gebied in uw Amazon Kinesis-account waarin Adobe Real-time CDP uw gegevens streamt.
* `{EVENT_HUB_NAME}`: *Voor Azure Event Hubs-verbindingen.* Vul de Azure-naam van de gebeurtenishub in, waarbij Adobe Real-time CDP uw gegevens streamt. Voor meer informatie, zie [Create een gebeurtenishub](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) in de documentatie van Microsoft.

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) voor de nieuwe doelverbinding naar uw streamingbestemming. Sla deze waarde op zoals deze in latere stappen wordt vereist.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Een gegevensstroom maken

![Overzicht doelstappen 4](/help/rtcdp/destinations/assets/step4-create-streaming-destination-api.png)

Met de id&#39;s die u in de vorige stappen hebt opgehaald, kunt u nu een gegevensstroom maken tussen de gegevens van het Experience Platform en de bestemming waarnaar u de gegevens wilt activeren. Beschouw deze stap als het construeren van de pijpleiding, waardoor de gegevens, tussen Experience Platform en uw gewenste bestemming later zullen stromen.

Als u een gegevensstroom wilt maken, voert u een POST-verzoek uit, zoals hieronder wordt weergegeven, terwijl u de hieronder vermelde waarden opgeeft binnen de laadtijd.

Voer het volgende POST- verzoek uit om een gegevensstroom tot stand te brengen.

**API-indeling**

```http
POST /flows
```

**Verzoek**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "Create dataflow to Amazon Kinesis/ Azure Event Hubs",
        "description": "This operation creates a dataflow to Amazon Kinesis/ Azure Event Hubs",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ]
    }
```

* `{FLOW_SPEC_ID}`: De flow-specificatie-id voor op profielen gebaseerde doelen is `71471eba-b620-49e4-90fd-23f1fa0174d8`. Gebruik deze waarde in de vraag.
* `{SOURCE_CONNECTION_ID}`: Gebruik de bronverbindings-id die u hebt verkregen in de stap [Verbinding maken met uw Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Gebruik de doel-verbindings-id die u hebt verkregen in de stap [Verbinden met streamingdoel](#connect-to-streaming-destination).

**Antwoord**

Een geslaagde reactie retourneert de id (`id`) van de nieuwe gegevensstroom en een `etag`. Noteer beide waarden. om segmenten te activeren, zoals u dat in de volgende stap doet.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Gegevens activeren naar uw nieuwe bestemming {#activate-data}

![Overzicht doelstappen 5](/help/rtcdp/destinations/assets/step5-create-streaming-destination-api.png)

Nadat u alle verbindingen en de gegevensstroom hebt gemaakt, kunt u nu uw profielgegevens activeren op het streamingplatform. In deze stap selecteert u welke segmenten en welke profielkenmerken u naar de bestemming verzendt en kunt u gegevens plannen en naar de bestemming verzenden.

Als u segmenten naar uw nieuwe bestemming wilt activeren, moet u een JSON PATCH-bewerking uitvoeren, vergelijkbaar met het onderstaande voorbeeld. U kunt veelvoudige segmenten en profielattributen in één vraag activeren. Zie de [RFC-specificatie](https://tools.ietf.org/html/rfc6902)voor meer informatie over JSON PATCH.

**API-indeling**

```http
PATCH /flows
```

**Verzoek**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "operator": "EXISTS",
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    },
        },
        {
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "operator": "EXISTS",
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

* `{DATAFLOW_ID}`: Gebruik de gegevensstroom die u in de vorige stap hebt verkregen.
* `{ETAG}`: Gebruik het label dat u in de vorige stap hebt verkregen.
* `{SEGMENT_ID}`: Geef de segment-id op die u naar dit doel wilt exporteren. Als u segment-id&#39;s wilt ophalen voor de segmenten die u wilt activeren, gaat u naar https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/, selecteert u **Segmenteringsservice-API** in het navigatiemenu links en zoekt u de `GET /segment/jobs` bewerking.
* `{PROFILE_ATTRIBUTE}`: Bijvoorbeeld, `personalEmail.address` of `person.lastName`

**Antwoord**

Kijk naar een 202 OK-antwoord. Er wordt geen responsorgaan geretourneerd. Om te bevestigen dat het verzoek correct was, zie de volgende stap, de gegevensstroom bevestigen.

## De gegevensstroom valideren

![Overzicht doelstappen 6](/help/rtcdp/destinations/assets/step6-create-streaming-destination-api.png)

Als laatste stap in de zelfstudie moet u controleren of de segmenten en profielkenmerken correct zijn toegewezen aan de gegevensstroom.

Om dit te bevestigen, voer het volgende GET verzoek uit:

**API-indeling**

```http
GET /flows
```

**Verzoek**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Gebruik de gegevensstroom uit de vorige stap.
* `{ETAG}`: Gebruik het label van de vorige stap.

**Antwoord**

De geretourneerde reactie moet in de `transformations` parameter de segmenten en profielkenmerken bevatten die u in de vorige stap hebt verzonden. Een voorbeeldparameter in de reactie kan er als volgt uitzien: `transformations`

```
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**Geëxporteerde gegevens**

>[!IMPORTANT]
>
> Naast de profielattributen en de segmenten in de stap [activeer gegevens aan uw nieuwe bestemming](#activate-data), zullen de uitgevoerde gegevens in Kinesis AWS en de Azure Gebeurtenishubs ook informatie over de identiteitskaart omvatten. Dit geeft de identiteiten van de geëxporteerde profielen aan (bijvoorbeeld [ECID](https://docs.adobe.com/content/help/en/id-service/using/intro/id-request.html), mobiele id, Google-id, e-mailadres, enz.). Zie een voorbeeld hieronder.

```
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes CDP in real time met één van uw aangewezen het stromen bestemmingen verbonden en opstelling een gegevensstroom aan de respectieve bestemming. De uitgaande gegevens kunnen nu in de bestemming voor klantenanalyse of om het even welke andere gegevensverrichtingen worden gebruikt u zou willen uitvoeren. Raadpleeg de volgende pagina&#39;s voor meer informatie:

* [Overzicht van doelen](../../rtcdp/destinations/destinations-overview.md)
* [Overzicht van de doelcatalogus](../../rtcdp/destinations/destinations-catalog.md)