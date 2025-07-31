---
solution: Experience Platform
title: Doelverbindingen bewerken met de Flow Service API
type: Tutorial
description: Leer hoe u verschillende componenten van een doelverbinding kunt bewerken met de Flow Service API.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: ea397360e5277bef478b2173bfb5e4be4ac1fab4
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 2%

---

# Doelverbindingen bewerken met de Flow Service API

Deze zelfstudie behandelt de stappen voor het bewerken van verschillende componenten van een doelverbinding. Leer hoe te om authentificatiegeloofsbrieven, de uitvoerplaats, en meer bij te werken door [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/) te gebruiken.

>[!NOTE]
>
> De bewerkingen die in deze zelfstudie worden beschreven, worden ook ondersteund in de gebruikersinterface van Experience Platform. Lees het leerprogramma op hoe te [ bestemmingen in UI ](/help/destinations/ui/edit-destination.md) voor meer informatie uitgeven.

## Aan de slag {#get-started}

Voor deze zelfstudie moet u een geldige gegevensstroom-id hebben. Als u geen geldige dataflow identiteitskaart hebt, selecteer uw bestemming van keus van de [ bestemmingscatalogus ](../catalog/overview.md) en volg de stappen die aan [ worden geschetst verbinden met de bestemming ](../ui/connect-destination.md) en [ activeren gegevens ](../ui/activation-overview.md) alvorens dit leerprogramma te proberen.

>[!NOTE]
>
> De termen *stroom* en *dataflow* worden gebruikt onderling verwisselbaar in dit leerprogramma. In de context van deze zelfstudie hebben ze dezelfde betekenis.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Doelen ](../home.md): [!DNL Destinations] zijn pre-gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.
* [ Sandboxes ](../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om uw gegevensstroom met de [!DNL Flow Service] API te kunnen bijwerken.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van Experience Platform te lezen.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Om vraag aan Experience Platform APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in Experience Platform, inclusief die van [!DNL Flow Service] , zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen aan Experience Platform API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Als de header `x-sandbox-name` niet is opgegeven, worden aanvragen opgelost onder de sandbox `prod` .

Alle verzoeken die een payload (`POST`, `PUT`, `PATCH`) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Gegevens over gegevensstroom opzoeken {#look-up-dataflow-details}

De eerste stap bij het bewerken van uw doelverbinding is het ophalen van gegevens over de gegevensstroom met uw flow-id. U kunt de huidige details van een bestaande gegevensstroom bekijken door een GET- verzoek aan het `/flows` eindpunt te doen.

>[!TIP]
>
>U kunt de gebruikersinterface van Experience Platform gebruiken om de gewenste gegevensstroom-id van een doel op te halen. Ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en selecteer de gewenste doelgegevensstroom en zoek de doel-id in de rechtertrack. De doel-id is de waarde die u in de volgende stap als stroom-id wilt gebruiken.
>
> ![ krijgt bestemmingsidentiteitskaart gebruikend Experience Platform UI ](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API formaat**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de doelgegevensstroom die u wilt ophalen. |

**Verzoek**

Met het volgende verzoek wordt informatie over uw flow-id opgehaald.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de huidige details van uw gegevensstroom met inbegrip van zijn versie, uniek herkenningsteken (`id`), en andere relevante informatie terug. Het meest relevant voor deze zelfstudie zijn de doel-verbinding en basis-verbindings-id&#39;s die in de onderstaande reactie worden gemarkeerd. U gebruikt deze id&#39;s in de volgende secties om verschillende componenten van de doelverbinding bij te werken.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## Doelverbindingscomponenten bewerken (opslaglocatie en andere componenten) {#patch-target-connection}

De componenten van een doelverbinding verschillen door bestemming. Voor [!DNL Amazon S3] -doelen kunt u bijvoorbeeld het emmertje en het pad bijwerken waar bestanden worden geëxporteerd. Voor [!DNL Pinterest] -doelen kunt u [!DNL Pinterest Advertiser ID] bijwerken en voor [!DNL Google Customer Match] kunt u [!DNL Pinterest Account ID] bijwerken.

Als u componenten van een doelverbinding wilt bijwerken, voert u een `PATCH` -aanvraag uit naar het `/targetConnections/{TARGET_CONNECTION_ID}` -eindpunt terwijl u uw doel-verbindings-id, -versie en de nieuwe waarden opgeeft die u wilt gebruiken. Herinner me, kreeg u uw identiteitskaart van de doelverbinding in de vorige stap, toen u een bestaande gegevensstroom aan uw gewenste bestemming inspecteerde.

>[!IMPORTANT]
>
>De header `If-Match` is vereist wanneer u een `PATCH` -aanvraag indient. De waarde voor deze header is de unieke versie van de doelverbinding die u wilt bijwerken. De etag waarde werkt met elke succesvolle update van een stroomentiteit zoals dataflow, doelverbinding, en anderen bij.
>
> Als u de laatste versie van de etag-waarde wilt ophalen, voert u een GET-aanvraag uit naar het `/targetConnections/{TARGET_CONNECTION_ID}` -eindpunt, waarbij `{TARGET_CONNECTION_ID}` de doel-verbindings-id is die u wilt bijwerken.
>
> Zorg ervoor dat u de waarde van de header `If-Match` tussen dubbele aanhalingstekens plaatst, zoals in de onderstaande voorbeelden, wanneer u `PATCH` -aanvragen maakt.

Hieronder staan enkele voorbeelden van het bijwerken van parameters in de specificaties van de doelverbinding voor verschillende typen doelen. Maar de algemene regel om parameters voor om het even welke bestemming bij te werken is als volgt:

Haal de gegevensstroom-id op van de verbinding > verkrijg de doel-verbindings-id > `PATCH` de doelverbinding met bijgewerkte waarden voor de gewenste parameters.

>[!BEGINSHADEBOX]

**API formaat**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

Met de volgende aanvraag worden de parameters `bucketName` en `path` van een [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) -doelverbinding bijgewerkt.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een geslaagde reactie retourneert uw doel-verbindings-id en een bijgewerkte Etag. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijkertijd uw doel-verbindings-id op te geven.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB  de Manager van de Advertentie van Google en Manager 360 van Google ]

**Verzoek**

Het volgende verzoek werkt de parameters van a [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) of [[!DNL Google Ad Manager 360]  bestemmings ](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) verbinding bij om het nieuwe [**[!UICONTROL Append audience ID to audience name]**](/help/release-notes/2023/april-2023.md#destinations) gebied toe te voegen.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een geslaagde reactie retourneert uw doel-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijkertijd uw doel-verbindings-id op te geven.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB  Pinterest ]

**Verzoek**

Het volgende verzoek werkt de `advertiserId` parameter van a [[!DNL Pinterest]  bestemmingsverbinding ](/help/destinations/catalog/advertising/pinterest.md#parameters) bij.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een geslaagde reactie retourneert uw doel-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijkertijd uw doel-verbindings-id op te geven.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Basisverbindingscomponenten bewerken (verificatieparameters en andere componenten) {#patch-base-connection}

Bewerk de basisverbinding wanneer u de referenties van een doel wilt bijwerken. De componenten van een basisverbinding verschillen door bestemming. Voor [!DNL Amazon S3] -doelen kunt u bijvoorbeeld de toegangstoets en de geheime sleutel bijwerken naar uw [!DNL Amazon S3] -locatie.

Als u componenten van een basisverbinding wilt bijwerken, voert u een `PATCH` -aanvraag uit naar het `/connections` -eindpunt terwijl u de id, versie en de nieuwe waarden voor de basisverbinding opgeeft die u wilt gebruiken.

Herinner me, u uw identiteitskaart van de basisverbinding in a [ vorige stap ](#look-up-dataflow-details) kreeg, toen u een bestaande dataflow aan uw gewenste bestemming voor de parameter `baseConnection` inspecteerde.

>[!IMPORTANT]
>
>De header `If-Match` is vereist wanneer u een `PATCH` -aanvraag indient. De waarde voor deze header is de unieke versie van de basisverbinding die u wilt bijwerken. De etag waarde werkt met elke succesvolle update van een stroomentiteit zoals dataflow, basisverbinding, en anderen bij.
>
> Als u de meest recente versie van de Etag-waarde wilt ophalen, voert u een GET-aanvraag uit naar het `/connections/{BASE_CONNECTION_ID}` -eindpunt, waarbij `{BASE_CONNECTION_ID}` de basis-verbindings-id is die u wilt bijwerken.
>
> Zorg ervoor dat u de waarde van de header `If-Match` tussen dubbele aanhalingstekens plaatst, zoals in de onderstaande voorbeelden, wanneer u `PATCH` -aanvragen maakt.

Hieronder staan enkele voorbeelden van het bijwerken van parameters in de specificatie van de basisverbinding voor verschillende soorten doelen. Maar de algemene regel om parameters voor om het even welke bestemming bij te werken is als volgt:

Haal de gegevensstroom-id op van de verbinding > verkrijg de id van de basisverbinding > `PATCH` de basisverbinding met bijgewerkte waarden voor de gewenste parameters.

>[!BEGINSHADEBOX]

**API formaat**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

Met de volgende aanvraag worden de parameters `accessId` en `secretKey` van een [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) -doelverbinding bijgewerkt.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een geslaagde reactie retourneert uw basis-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijk uw basis-verbindings-id op te geven.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB  Azure Blob ]

**Verzoek**

Het volgende verzoek werkt de parameters van een [[!DNL Azure Blob]  bestemmings ](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) verbinding bij om het verbindingskoord bij te werken dat wordt vereist om met een Azure instantie van Blob te verbinden.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen zijn: `add` , `replace` en `remove` . |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Reactie**

Een geslaagde reactie retourneert uw basis-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en tegelijk uw basis-verbindings-id op te geven.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het Experience Platform API-foutbericht. Verwijs naar [ API statuscodes ](/help/landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](/help/landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform voor meer informatie bij het interpreteren van foutenreacties.

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u geleerd hoe u verschillende componenten van een doelverbinding kunt bijwerken met de [!DNL Flow Service] API. Voor meer informatie over bestemmingen, zie het [ overzicht van bestemmingen ](../home.md).
