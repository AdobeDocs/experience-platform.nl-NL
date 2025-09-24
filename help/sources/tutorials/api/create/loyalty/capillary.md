---
title: Connect Capillary aan Experience Platform met behulp van de Flow Service API
description: Leer hoe u Capillary kunt verbinden met Experience Platform via API's.
hide: true
hidefromtoc: true
badge: Beta
exl-id: 763792d0-d5dc-40ac-b86a-6a0d26463b71
source-git-commit: b3b1542f7e297f4ca872a155ac3801266bc1e6a6
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Capillary Streaming Events] API[!DNL Flow Service]

>[!AVAILABILITY]
>
>De bron [!DNL Capillary Streaming Events] is in bèta. Lees de [ termijnen en voorwaarden ](../../../../home.md#terms-and-conditions) in het bronoverzicht voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Lees deze gids om te leren hoe te om [!DNL Capillary Streaming Events] en [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/) te gebruiken om gegevens van uw [!DNL Capillary] rekening aan Adobe Experience Platform te stromen.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste referenties verzamelen

Lees het [[!DNL Capillary Streaming Events]  overzicht ](../../../../connectors/loyalty/capillary.md) voor informatie over authentificatie.

### Experience Platform API&#39;s gebruiken

Lees de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md) voor informatie over hoe te met succes vraag aan Experience Platform APIs maken.

>[!BEGINSHADEBOX]

## Controlelijst voor ontwikkelproces

1. Creeer of kies uw doel **Model van de Gegevens van de Ervaring (XDM) schema** gebruikend de Registratie van het Schema. Gebruik dit schema XDM om **een dataset** in de Dienst van de Catalogus tot stand te brengen.
2. Creeer a **basisverbinding** om uw [!DNL Capillary] geloofsbrieven op te slaan.
3. Creeer a **bronverbinding** om aan uw `baseConnectionId` te binden.
4. Creeer a **doelverbinding** om ervoor te zorgen dat uw gegevens in gegevens meer landen.
5. Met Gegevensvoorinstelling kunt u toewijzingen maken die uw [!DNL Capillary] -bronvelden toewijzen aan de juiste XDM-velden.
6. Een gegevensstroom maken met de `sourceConnectionId` , `targetConnectionId` en `mappingID`
7. Testen met één voorbeeldprofiel/transactiegebeurtenissen om uw gegevensstroom te controleren.

>[!ENDSHADEBOX]

## Een basisverbinding maken {#base-connection}

Een basisverbinding behoudt referenties en verbindingsdetails. Als u een basisverbinding voor [!DNL Capillary] wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt van de [!DNL Flow Service] API en geeft u de [!DNL Capillary] -gegevens op in de hoofdtekst van de aanvraag.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Capillary] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**Reactie**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Een bronverbinding maken

Om een bronverbinding tot stand te brengen, doe een POST- verzoek aan het `/sourceConnections` eindpunt terwijl het verstrekken van uw identiteitskaart van de basisverbinding.

**API formaat**

```http
POST /flowservice/sourceConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**Reactie**

Een succesvolle reactie keert status 201 van HTTP met gedetailleerde van de pas gecreëerde bronverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### Schema-configuraties

>[!BEGINTABS]

>[!TAB  Inname van het Profiel ]

Profielen bevatten identiteits- en loyaliteitskenmerken. Bekijk de volgende lading voor een voorbeeld dat op het [!DNL Capillary] profielschema wordt gebaseerd. U kunt dit schema vormen en in kaart brengen aan een Individueel Profiel XDM.

**Verzoek**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**Reactie**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB  Inname van de Transactie ]

Transacties maken handelsactiviteiten vast. Bekijk de volgende lading voor een voorbeeld dat op het [!DNL Capillary] gebeurtenisschema wordt gebaseerd. U kunt dit schema configureren en toewijzen aan een XDM Experience-gebeurtenis.

**Verzoek**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**Reactie**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

<!--### Supported Events

The [!DNL Capillary] source supports the following events:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`-->

### Historische gegevensmigratie

Je kunt je historische loyaliteit en transactiegegevens naar Experience Platform brengen. Exporteer uw gegevens gewoon als gestructureerde CSV-bestanden vanuit [!DNL Capillary], breng ze veilig over met [!DNL SFTP] en neem ze op in uw Experience Platform-gegevenssets. Na de eerste migratie blijven uw gegevens in real-time up-to-date via de gebeurtenisgestuurde connector.

### Een doel-XDM-schema maken {#target-schema}

Een schema van de Gegevens van de Ervaring van het Model (XDM) verstrekt een gestandaardiseerde manier om gegevens van de klantenervaring binnen Experience Platform te organiseren en te beschrijven. Om uw brongegevens in Experience Platform in te voeren, moet u eerst een doelXDM schema tot stand brengen dat de structuur en de soorten gegevens bepaalt u wilt opnemen. Dit schema dient als blauwdruk voor de dataset van Experience Platform waar uw opgenomen gegevens zullen verblijven.

Een doelXDM schema kan worden gecreeerd door een POST- verzoek aan de [ Registratie API van het Schema ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) uit te voeren. Lees de volgende hulplijnen voor gedetailleerde stappen over het maken van een doel-XDM-schema:

* [ creeer een schema gebruikend API ](../../../../../xdm/api/schemas.md).
* [ creeer een schema gebruikend UI ](../../../../../xdm/tutorials/create-schema-ui.md).

Zodra gecreeerd, zal het doelXDM schema `$id` later voor uw doeldataset en afbeelding worden vereist.

## Een doelgegevensset maken {#target-dataset}

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch gestructureerd zoals een lijst met kolommen (schema) en rijen (gebieden). De gegevens die met succes in Experience Platform worden opgenomen worden opgeslagen binnen het gegevensmeer als datasets. Tijdens deze stap, kunt u of een nieuwe dataset tot stand brengen of bestaande gebruiken.

U kunt een doeldataset tot stand brengen door een POST- verzoek aan de [ Dienst API van de Catalogus ](https://developer.adobe.com/experience-platform-apis/references/catalog/) te doen, terwijl het verstrekken van identiteitskaart van het doelschema binnen de nuttige lading. Voor gedetailleerde stappen op hoe te om een doeldataset tot stand te brengen, lees de gids bij [ het creëren van een dataset gebruikend API ](../../../../../catalog/api/create-dataset.md).


## Een doelverbinding maken {#target}

Een doelverbinding vertegenwoordigt de verbinding aan de bestemming waar de ingesloten gegevens binnen landen. Om een doelverbinding tot stand te brengen, moet u vaste identiteitskaart van de verbindingsspecificatie verstrekken verbonden aan het gegevens meer. Deze verbindingsspecificatie-id is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` .

**API formaat**

```http
POST /targetConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### Een toewijzing maken {#mapping}

Daarna, kaart uw brongegevens aan het doelschema dat uw doeldataset volgt aan. Om een afbeelding tot stand te brengen, doe een POST verzoek aan het `mappingSets` eindpunt van [[!DNL Data Prep]  API ](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Neem de doel-XDM-schema-id op en de details van de toewijzingssets die u wilt maken.

Wijs de Capillaire gebieden aan de overeenkomstige XDM schemagebieden als volgt toe:

| Source-schema | Doelschema |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email[0].id` |
| `loyalty.points` | `xdm:loyalty.points` |
| `loyalty.tier` | `xdm:loyalty.tier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

>[!TIP]
>
>U kunt de [ Gebeurtenissen en afbeeldingen van het Profiel ](../../../../images/tutorials/create/capillary/mappings.zip) voor [!DNL Capillary] downloaden en [ de dossiers invoeren aan Prep van Gegevens ](../../../../../data-prep/ui/mapping.md#import-mapping) wanneer u bereid bent om uw gegevens in kaart te brengen.

### Een gegevensstroom maken {#flow}

Nadat u de bronverbinding, toewijzing en doelverbinding hebt gemaakt, kunt u een gegevensstroom configureren om gegevens van [!DNL Capillary] naar Experience Platform te verplaatsen.

De meest gangbare gegevensstromen zijn:

* **dataflow van het Profiel**: Maakt [!DNL Capillary] profielgegevens in een individuele dataset van het Profiel XDM op.
* **Dataflow van de Transactie**: Maakt [!DNL Capillary] transactiegegevens in een dataset XDM ExperienceEvent op.

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime` wordt in UNIX-epoch seconden weergegeven.

**Reactie**

Een succesvolle reactie keert uw gegevensstroom met zijn overeenkomstige dataflow ID terug.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## Foutafhandeling

De schakelaar omvat robuuste fout behandeling voor de volgende scenario&#39;s:

* **de fouten van de Authentificatie**: Verfrist automatisch de geloofsbrieven van Adobe wanneer de authentificatie ontbreekt.
* **de beperkingsfouten van het Tarief**: Implementeert opnieuw probeert met exponentiële backoff wanneer API tariefgrenzen worden bereikt.
* **de fouten van het Netwerk**: Logs en probeert ontbroken netwerkverzoeken opnieuw.
* **de bevestigingsfouten van Gegevens**: Logs ongeldige ladingen voor handrevisie en resolutie.

Alle fouten worden geregistreerd met details zoals fouttype, timestamp, request payload, en Adobe API reactie om het oplossen van problemen en het zuiveren te vergemakkelijken.

## De verbinding testen

Voer de onderstaande stappen uit om te leren hoe u uw verbinding kunt testen:

* Voer een GET-aanvraag in bij `/connections/{BASE_CONNECTION_ID}` en geef uw basis-verbindings-id op om te controleren of uw basisverbinding bestaat. Tijdens deze stap kunt u ook controleren of de status van de basisverbinding is ingesteld op `active` .
* Voer een GET-aanvraag in bij `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}` en geef uw bron-verbindings-id op om uw bronverbinding te verifiëren.
* Gebruik de URL van het streamingeindpunt om een voorbeeldprofiellading te verzenden (gebruik de profielopname JSON).
* Navigeer naar uw dataset in Experience Platform UI en stel een vraag op de dataset in werking om uw verslagen te bevestigen.
* Gebruik de logboeken van de Prep van Gegevens om fouten te inspecteren.
* Als u een steunkaartje moet openen, zorg ervoor dat u het volgende hebt:
   * Vragen om lading
   * Responsinstantie
   * Request-id
   * tijdstempel
   * Resource ID&#39;s.

## Bijlage

Bezoek de volgende documentatie voor hulplijnen voor extra bewerkingen

* [ Dataflows van de Monitor ](../../../../../dataflows/ui/monitor-sources.md)
* [ Update dataflows ](../../../ui/update-dataflows.md)
* [ schrapping dataflows ](../../../ui/delete.md)
* [ Bron van de Update rekening ](../../../ui/update.md)
