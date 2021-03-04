---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Verbinding maken met marketingdoelen voor e-mail en gegevens activeren via API-aanroepen
description: Dit document behandelt het maken van e-mailmarketingdoelen met de Adobe Experience Platform API
topic: zelfstudie
type: Zelfstudie
translation-type: tm+mt
source-git-commit: 789534c02746ed24dfa01c7b471cdf3be407711e
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 0%

---


# Verbinding maken met marketingdoelen voor e-mail en gegevens activeren via API-aanroepen

Deze zelfstudie laat zien hoe u API-aanroepen kunt gebruiken om verbinding te maken met uw Adobe Experience Platform-gegevens, een [e-mailmarketingbestemming](../catalog/email-marketing/overview.md) te maken, een gegevensstroom naar uw nieuwe gemaakte bestemming te maken en gegevens te activeren voor uw nieuwe gemaakte bestemming.

In deze zelfstudie wordt de Adobe Campaign-bestemming in alle voorbeelden gebruikt, maar de stappen zijn identiek voor alle marketingdoelen per e-mail.

![Overzicht - de stappen om een bestemming tot stand te brengen en segmenten te activeren](../assets/api/email-marketing/overview.png)

Zie de [Zelfstudies Een doel verbinden](../ui/connect-destination.md) en [Profielen en segmenten activeren aan een doel](../ui/activate-destinations.md) als u liever de gebruikersinterface in Platform gebruikt.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.
* [[!DNL Catalog Service]](../../catalog/home.md):  [!DNL Catalog] is het registratiesysteem voor gegevenslocatie en -lijn binnen  [!DNL Experience Platform].
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om gegevens aan e-mail marketing bestemmingen in Platform te activeren.

### Vereiste referenties verzamelen

Om de stappen in dit leerprogramma te voltooien, zou u de volgende geloofsbrieven klaar moeten hebben, afhankelijk van het type van bestemmingen dat u verbindt en segmenten aan activeert.

* Voor [!DNL Amazon] S3 verbindingen aan e-mailmarketing platforms: `accessId`, `secretKey`
* Voor SFTP-verbindingen met e-mailmarketingplatforms: `domain`, `port`, `username`, `password` of `ssh key` (afhankelijk van de verbindingsmethode met de FTP-locatie)

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste en optionele koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Bronnen in [!DNL Experience Platform] kunnen worden geïsoleerd naar specifieke virtuele sandboxen. In aanvragen voor [!DNL Platform] API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Experience Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

### Documentatie voor de wagenbak

In deze zelfstudie in Swagger vindt u begeleidende referentiedocumentatie voor alle API-aanroepen. Zie de [documentatie van de Dienst API van de Stroom op Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). We raden u aan deze zelfstudie en de documentatiepagina van Swagger parallel te gebruiken.

## Hiermee wordt de lijst met beschikbare doelen opgehaald {#get-the-list-of-available-destinations}

![Overzicht doelstappen 1](../assets/api/email-marketing/step1.png)

Als eerste stap moet u bepalen naar welke e-mailmarketingbestemming de gegevens moeten worden geactiveerd. Om met te beginnen, voer een vraag uit om een lijst van beschikbare bestemmingen te verzoeken die u segmenten kunt verbinden en activeren aan. Voer het volgende GET verzoek aan het `connectionSpecs` eindpunt uit om een lijst van beschikbare bestemmingen terug te keren:

**API-indeling**

```http
GET /connectionSpecs
```

**Verzoek**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Antwoord**

Een succesvolle reactie bevat een lijst van beschikbare bestemmingen en hun unieke herkenningstekens (`id`). Sla de waarde op van het doel dat u wilt gebruiken, zoals in verdere stappen wordt vereist. Als u bijvoorbeeld segmenten wilt verbinden en leveren aan Adobe Campaign, zoekt u het volgende fragment in het antwoord:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Verbind met uw [!DNL Experience Platform] gegevens {#connect-to-your-experience-platform-data}

![Overzicht doelstappen 2](../assets/api/email-marketing/step2.png)

Vervolgens moet u verbinding maken met uw [!DNL Experience Platform]-gegevens, zodat u profielgegevens kunt exporteren en activeren op de gewenste bestemming. Deze bestaat uit twee substappen die hieronder worden beschreven.

1. Eerst, moet u een vraag uitvoeren om toegang tot uw gegevens in [!DNL Experience Platform] toe te staan, door opstelling een basisverbinding.
2. Dan, gebruikend identiteitskaart van de basisverbinding, zult u een andere vraag maken waarin u een bronverbinding creeert, die de verbinding aan uw [!DNL Experience Platform] gegevens vestigt.


### Toegang tot uw gegevens toestaan in [!DNL Experience Platform]

**API-indeling**

```http
POST /connections
```

**Verzoek**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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


* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsSpatiespecificatieidentiteitskaart voor de Verenigde Dienst van het Profiel -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwoord**

Een succesvolle reactie bevat het unieke herkenningsteken van de basisverbinding (`id`). Sla deze waarde op zoals vereist in de volgende stap om de bronverbinding te maken.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Verbind met uw [!DNL Experience Platform] gegevens {#connect-to-platform-data}

**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

```shell
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
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Gebruik de id die u in de vorige stap hebt gekregen.
* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsspecificatie-id voor  [!DNL Unified Profile Service] -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) voor de nieuwe bronverbinding naar [!DNL Unified Profile Service]. Dit bevestigt dat u verbinding hebt gemaakt met uw [!DNL Experience Platform] gegevens. Sla deze waarde op zoals deze in een latere stap wordt vereist.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Verbinding maken met marketingdoel voor e-mail {#connect-to-email-marketing-destination}

![Overzicht doelstappen 3](../assets/api/email-marketing/step3.png)

In deze stap stelt u een verbinding in met uw gewenste e-mailmarketingbestemming. Deze bestaat uit twee substappen die hieronder worden beschreven.

1. Eerst, moet u een vraag uitvoeren om toegang tot de e-maildienstverlener toe te staan, door opstelling een basisverbinding.
2. Vervolgens doet u met de id van de basisverbinding een volgende aanroep waarin u een doelverbinding maakt. Hiermee geeft u in uw opslagaccount de locatie op waar de geëxporteerde gegevens worden geleverd en de indeling van de gegevens die worden geëxporteerd.

### Toegang tot de e-mailmarketingbestemming toestaan

**API-indeling**

```http
POST /connections
```

**Verzoek**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsSpeciaal identiteitskaart u in de stap verkrijgt  [krijgt de lijst van beschikbare bestemmingen](#get-the-list-of-available-destinations).
* `{S3 or SFTP}`: Vul het gewenste verbindingstype voor deze bestemming in. Blader in de doelcatalogus [a1/> naar de gewenste bestemming om te zien of de S3- en/of SFTP-verbindingstypen worden ondersteund.](../catalog/overview.md)
* `{ACCESS_ID}`: Uw toegangs-id voor uw  [!DNL Amazon] S3-opslaglocatie.
* `{SECRET_KEY}`: Uw geheime sleutel voor uw  [!DNL Amazon] S3 opslagplaats.

**Antwoord**

Een succesvolle reactie bevat het unieke herkenningsteken van de basisverbinding (`id`). Sla deze waarde op zoals vereist in de volgende stap om een doelverbinding te maken.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Opslaglocatie en gegevensindeling opgeven

[!DNL Adobe Experience Platform] Hiermee exporteert u gegevens voor e-mailmarketing en cloudopslagbestemmingen in de vorm van  [!DNL CSV] bestanden.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] Hiermee worden de exportbestanden automatisch gesplitst op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel.
>
>Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking, als zodanig: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

**API-indeling**

```http
POST /targetConnections
```

**Verzoek**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
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
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Gebruik de basisverbindings-id die u in de bovenstaande stap hebt verkregen.
* `{CONNECTION_SPEC_ID}`: Gebruik de verbindingsspecificatie u in de stap verkrijgt  [krijgt de lijst van beschikbare bestemmingen](#get-the-list-of-available-destinations).
* `{BUCKETNAME}`: Uw  [!DNL Amazon] S3 emmertje, waar het Platform de gegevensuitvoer zal deponeren.
* `{FILEPATH}`: Het pad in uw  [!DNL Amazon] S3 emmerdirectory waar Platform de gegevensexport zal neerzetten.

**Antwoord**

Een succesvol antwoord keert het unieke herkenningsteken (`id`) voor de pas gecreëerde doelverbinding aan uw e-mailmarketing bestemming terug. Sla deze waarde op zoals deze in latere stappen wordt vereist.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Een gegevensstroom maken

![Overzicht doelstappen 4](../assets/api/email-marketing/step4.png)

Met de id&#39;s die u in de vorige stappen hebt opgehaald, kunt u nu een gegevensstroom maken tussen uw [!DNL Experience Platform]-gegevens en de bestemming waar u de gegevens naartoe wilt activeren. Beschouw deze stap als het construeren van de pijpleiding, waardoor de gegevens later, tussen [!DNL Experience Platform] en uw gewenste bestemming zullen stromen.

Om een gegevensstroom tot stand te brengen, voer een verzoek van de POST uit, zoals hieronder getoond, terwijl het verstrekken van de hieronder vermelde waarden binnen de lading.

Voer het volgende verzoek van de POST uit om een gegevensstroom tot stand te brengen.

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
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
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

* `{FLOW_SPEC_ID}`: Gebruik de stroom voor de e-mailmarketingbestemming waarmee u verbinding wilt maken. Om de stroomspecificatie te krijgen, voer een verrichting van de GET op het `flowspecs` eindpunt uit. Zie hier de documentatie van Swagger: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. In de reactie, zoek `upsTo` en kopieer overeenkomstige identiteitskaart van de e-mailmarketing bestemming die u wilt verbinden met. Zoek in Adobe Campaign bijvoorbeeld naar `upsToCampaign` en kopieer de parameter `id`.
* `{SOURCE_CONNECTION_ID}`: Gebruik de bronverbindings-id die u hebt verkregen in de stap  [Verbinding maken met uw Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Gebruik de doel-verbindings-id die u hebt verkregen in de stap  [Verbinding maken met e-mailmarketingdoel](#connect-to-email-marketing-destination).

**Antwoord**

Een succesvolle reactie keert identiteitskaart (`id`) van nieuw gecreeerd dataflow en `etag` terug. Noteer beide waarden. om segmenten te activeren, zoals u dat in de volgende stap doet.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Gegevens activeren naar uw nieuwe bestemming

![Overzicht doelstappen 5](../assets/api/email-marketing/step5.png)

Nadat u alle verbindingen en de gegevensstroom hebt gemaakt, kunt u nu uw profielgegevens activeren naar het e-mailmarketingplatform. In deze stap selecteert u welke segmenten en welke profielkenmerken u naar de bestemming verzendt en kunt u gegevens plannen en naar de bestemming verzenden.

Als u segmenten naar uw nieuwe bestemming wilt activeren, moet u een JSON PATCH-bewerking uitvoeren, vergelijkbaar met het onderstaande voorbeeld. U kunt veelvoudige segmenten en profielattributen in één vraag activeren. Voor meer informatie over JSON PATCH, zie [RFC specificatie](https://tools.ietf.org/html/rfc6902).

**API-indeling**

```http
PATCH /flows
```

**Verzoek**

```shell
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
    }
]
```

* `{DATAFLOW_ID}`: Gebruik de gegevensstroom die u in de vorige stap hebt verkregen.
* `{ETAG}`: Gebruik het label dat u in de vorige stap hebt verkregen.
* `{SEGMENT_ID}`: Geef de segment-id op die u naar dit doel wilt exporteren. Als u segment-id&#39;s wilt ophalen voor de segmenten die u wilt activeren, gaat u naar **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, selecteert u **[!UICONTROL Segmenteringsservice-API]** in het linkernavigatiemenu en zoekt u de `GET /segment/definitions`-bewerking in **[!UICONTROL Segmentdefinities]**.
* `{PROFILE_ATTRIBUTE}`: Bijvoorbeeld, `"person.lastName"`

**Antwoord**

Kijk naar een 202 OK-antwoord. Er wordt geen responsorgaan geretourneerd. Om te bevestigen dat het verzoek correct was, zie de volgende stap, de gegevensstroom bevestigen.

## De gegevensstroom valideren

![Overzicht doelstappen 6](../assets/api/email-marketing/step6.png)

Als laatste stap in de zelfstudie moet u controleren of de segmenten en profielkenmerken correct zijn toegewezen aan de gegevensstroom.

Om dit te bevestigen, voer het volgende verzoek van de GET uit:

**API-indeling**

```http
GET /flows
```

**Verzoek**

```shell
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

De geretourneerde reactie moet in de parameter `transformations` de segmenten en profielkenmerken opnemen die u in de vorige stap hebt verzonden. Een voorbeeld `transformations` parameter in de reactie zou als hieronder kunnen kijken:

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
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

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes Platform met één van uw aangewezen e-mailmarketing bestemmingen verbonden en opstelling een gegevensstroom aan de respectieve bestemming. De uitgaande gegevens kunnen nu in de bestemming voor e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen worden gebruikt. Raadpleeg de volgende pagina&#39;s voor meer informatie:

* [Overzicht van doelen](../home.md)
* [Overzicht van de doelcatalogus](../catalog/overview.md)