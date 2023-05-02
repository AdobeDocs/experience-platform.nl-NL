---
solution: Experience Platform
title: Doelverbindingen bewerken met de Flow Service API
type: Tutorial
description: Leer hoe u verschillende componenten van een doelverbinding kunt bewerken met de Flow Service API.
source-git-commit: 52fe0ef2ab195756c381b3ef0a5792dffe459b8d
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---

# Doelverbindingen bewerken met de Flow Service API

Deze zelfstudie behandelt de stappen voor het bewerken van verschillende componenten van een doelverbinding. Leer hoe u verificatiereferenties, exportlocatie en meer kunt bijwerken met de opdracht [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> De bewerkingen die in deze zelfstudie worden beschreven, worden momenteel alleen ondersteund via de Flow Service API.

## Aan de slag {#get-started}

Voor deze zelfstudie moet u een geldige gegevensstroom-id hebben. Als u geen geldige dataflow-id hebt, selecteert u de gewenste bestemming in het menu [doelcatalogus](../catalog/overview.md) en voert u de volgende stappen uit: [verbinden met de bestemming](../ui/connect-destination.md) en [gegevens activeren](../ui/activation-overview.md) voordat u deze zelfstudie probeert.

>[!NOTE]
>
> De voorwaarden *stroom* en *dataflow* worden onderling verwisselbaar gebruikt in deze zelfstudie. In de context van deze zelfstudie hebben ze dezelfde betekenis.

Voor deze zelfstudie hebt u ook een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Doelen](../home.md): [!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.
* [Sandboxen](../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om uw gegevensstroom met succes bij te werken met de [!DNL Flow Service] API.

### API-voorbeeldaanroepen lezen {#reading-sample-api-calls}

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

### Waarden verzamelen voor vereiste koppen {#gather-values-for-required-headers}

Als u aanroepen wilt uitvoeren naar Platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle middelen in Experience Platform, met inbegrip van die welke toebehoren aan [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Als de `x-sandbox-name` header is niet opgegeven, aanvragen worden opgelost onder de `prod` sandbox.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Gegevens over gegevensstroom opzoeken {#look-up-dataflow-details}

De eerste stap bij het bewerken van uw doelverbinding is het ophalen van gegevens over de gegevensstroom met uw flow-id. U kunt de huidige details van een bestaande gegevensstroom bekijken door een verzoek van de GET aan `/flows` eindpunt.

>[!TIP]
>
>U kunt Experience Platform UI gebruiken om gewenste dataflow identiteitskaart van een bestemming te krijgen. Ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**, selecteert u de gewenste doelgegevensstroom en zoekt u de doel-id in de rechtertrack. De doel-id is de waarde die u in de volgende stap als stroom-id wilt gebruiken.
>
> ![Doel-id ophalen met de gebruikersinterface van het Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API-indeling**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{FLOW_ID}` | De unieke `id` -waarde voor de doelgegevensstroom die u wilt ophalen. |

**Verzoek**

Het volgende verzoek wint informatie betreffende uw stroom ID terug.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de huidige details van uw gegevensstroom inclusief de versie, unieke id (`id`) en andere relevante informatie. Het meest relevant voor deze zelfstudie zijn de doel-verbinding en basis-verbindings-id&#39;s die in de onderstaande reactie worden gemarkeerd. U gebruikt deze id&#39;s in de volgende secties om verschillende componenten van de doelverbinding bij te werken.

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

De componenten van een doelverbinding verschillen door bestemming. Bijvoorbeeld: [!DNL Amazon S3] doelen, kunt u het emmertje en pad bijwerken waar bestanden worden geëxporteerd. Voor [!DNL Pinterest] doelen, kunt u uw [!DNL Pinterest Advertiser ID] en voor [!DNL Google Customer Match] u kunt uw [!DNL Pinterest Account ID].

Als u componenten van een doelverbinding wilt bijwerken, voert u een PATCH-verzoek uit naar de `/targetConnections/{TARGET_CONNECTION_ID}` eindpunt terwijl het verstrekken van uw identiteitskaart van de doelverbinding, versie, en de nieuwe waarden u wilt gebruiken. Herinner me, kreeg u uw identiteitskaart van de doelverbinding in de vorige stap, toen u een bestaande gegevensstroom aan uw gewenste bestemming inspecteerde.

>[!IMPORTANT]
>
>De `If-Match` header is required when making a PATCH request. De waarde voor deze header is de unieke versie van de doelverbinding die u wilt bijwerken. De etag waarde werkt met elke succesvolle update van een stroomentiteit zoals dataflow, doelverbinding, en anderen bij.
>
> Om de recentste versie van de etiketwaarde te krijgen, doe een verzoek van de GET aan `/targetConnections/{TARGET_CONNECTION_ID}` eindpunt, waarbij `{TARGET_CONNECTION_ID}` Dit is de doel-verbindings-id die u wilt bijwerken.

Hieronder staan enkele voorbeelden van het bijwerken van parameters in de specificaties van de doelverbinding voor verschillende typen doelen. Maar de algemene regel om parameters voor om het even welke bestemming bij te werken is als volgt:

Haal de gegevensstroom-id op van de verbinding > verkrijg de doel-verbindings-id > PATCH de doelverbinding met bijgewerkte waarden voor de gewenste parameters.

>[!BEGINSHADEBOX]

**API-indeling**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!ENDSHADEBOX]


>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

De volgende aanvraag werkt de `bucketName` en `path` parameters van een [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) doelverbinding.

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
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw doel-verbindings-id en een bijgewerkte Etag. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl het verstrekken van uw doel verbindings identiteitskaart

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager 360]

**Verzoek**

Met het volgende verzoek worden de parameters van een [[!DNL Google Ad Manager 360] doel](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) verbinding om nieuwe toevoegings segmentidentiteitskaart aan het gebied van de segmentnaam toe te voegen.

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
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw doel-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl het verstrekken van uw doel verbindings identiteitskaart

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Verzoek**

De volgende aanvraag werkt de `advertiserId` parameter van een [[!DNL Pinterest] doelverbinding](/help/destinations/catalog/advertising/pinterest.md#parameters).

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
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw doel-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl het verstrekken van uw doel verbindings identiteitskaart

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

## Basisverbindingscomponenten bewerken (verificatieparameters en andere componenten) {#patch-base-connection}

De componenten van een basisverbinding verschillen door bestemming. Bijvoorbeeld: [!DNL Amazon S3] bestemmingen, kunt u de toegangssleutel en geheime sleutel aan uw bijwerken [!DNL Amazon S3] locatie.

Als u componenten van een basisverbinding wilt bijwerken, voert u een PATCH-verzoek uit aan de `/connections` eindpunt terwijl het verstrekken van uw identiteitskaart van de basisverbinding, versie, en de nieuwe waarden u wilt gebruiken.

Herinner me, kreeg u uw identiteitskaart van de basisverbinding in een vorige stap, toen u een bestaande gegevensstroom aan uw gewenste bestemming inspecteerde.

>[!IMPORTANT]
>
>De `If-Match` header is required when making a PATCH request. De waarde voor deze header is de unieke versie van de basisverbinding die u wilt bijwerken. De etag waarde werkt met elke succesvolle update van een stroomentiteit zoals dataflow, basisverbinding, en anderen bij.
>
> Om de recentste versie van de etiketwaarde te krijgen, doe een verzoek van de GET aan `/connections/{BASE_CONNECTION_ID}` eindpunt, waarbij `{BASE_CONNECTION_ID}` Dit is de basisverbindings-id die u wilt bijwerken.

Hieronder staan enkele voorbeelden van het bijwerken van parameters in de specificatie van de basisverbinding voor verschillende soorten doelen. Maar de algemene regel om parameters voor om het even welke bestemming bij te werken is als volgt:

Krijg dataflow identiteitskaart van de verbinding > verkrijg identiteitskaart van de basisverbinding > PATCH de basisverbinding met bijgewerkte waarden voor de gewenste parameters.

**API-indeling**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Verzoek**

De volgende aanvraag werkt de `accessId` en `secretKey` parameters van een [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) doelverbinding.

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
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw basis-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl het verstrekken van uw identiteitskaart van de basisverbinding.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Verzoek**

Met het volgende verzoek worden de parameters van een [[!DNL Azure Blob] doel](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) verbinding om de verbindingstekenreeks bij te werken die is vereist om verbinding te maken met een Azure Blob-instantie.

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
| `op` | De verrichtingsvraag die wordt gebruikt om de actie te bepalen nodig om dataflow bij te werken. Bewerkingen omvatten: `add`, `replace`, en `remove`. |
| `path` | Definieert het deel van de flow dat moet worden bijgewerkt. |
| `value` | De nieuwe waarde waarmee u de parameter wilt bijwerken. |

**Antwoord**

Een geslaagde reactie retourneert uw basis-verbindings-id en een bijgewerkt label. U kunt de update verifiëren door een verzoek van de GET aan [!DNL Flow Service] API, terwijl het verstrekken van uw identiteitskaart van de basisverbinding.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

## API-foutafhandeling {#api-error-handling}

De API-eindpunten in deze zelfstudie volgen de algemene beginselen van het API-foutbericht voor Experience Platforms. Zie [API-statuscodes](/help/landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](/help/landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van de Platform voor meer informatie over het interpreteren van foutenreacties.

## Volgende stappen {#next-steps}

Door dit leerprogramma te volgen, hebt u geleerd hoe te om diverse componenten van een bestemmingsverbinding bij te werken gebruikend [!DNL Flow Service] API. Voor meer informatie over bestemmingen, zie [Overzicht van doelen](../home.md).
