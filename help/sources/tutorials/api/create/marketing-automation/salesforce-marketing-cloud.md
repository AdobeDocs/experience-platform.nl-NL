---
title: Salesforce Marketing Cloud met Experience Platform verbinden met behulp van de Flow Service API
description: Leer hoe u uw Salesforce Marketing Cloud-account met Experience Platform kunt verbinden via API's.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Salesforce Marketing Cloud] API[!DNL Flow Service]

>[!WARNING]
>
>De [!DNL Salesforce Marketing Cloud] -bron wordt afgekeurd in januari 2026. Later dit jaar zal een nieuwe bron worden vrijgegeven als alternatief. Zodra de nieuwe bron wordt vrijgegeven, moet u van plan zijn om aan de nieuwe bron te migreren door nieuwe rekeningsverbindingen en dataflows vóór eind Januari 2026 te creëren.

Lees deze gids om te leren hoe te om uw [!DNL Salesforce Marketing Cloud] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Azure Synapse Analytics] via de [!DNL Flow Service] API.


### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

In de volgende sectie vindt u aanvullende informatie die u moet weten als u verbinding wilt maken met [!DNL Salesforce Marketing Cloud] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Lees het [[!DNL Salesforce Marketing Cloud]  authentificatieoverzicht &#x200B;](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md) voor informatie over authentificatie.

### Experience Platform API&#39;s gebruiken

Lees de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md) voor informatie over hoe te met succes vraag aan Experience Platform APIs maken.

## Verbinding maken [!DNL Salesforce Marketing Cloud] met Experience Platform op [!DNL Azure]

Lees het volgende voor meer informatie over het maken van een basisverbinding en het verbinden van uw [!DNL Salesforce Marketing Cloud] -account met Experience Platform op [!DNL Azure] .

### Een basisverbinding maken {#azure-base}

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de bronintegratie van [!DNL Salesforce Marketing Cloud] .

A **basisverbinding** slaat zeer belangrijke informatie op die uw bronsysteem met Adobe Experience Platform verbindt. Dit omvat het volgende:

* Verificatiegegevens van uw bron
* De huidige status van de verbinding
* Een unieke **identiteitskaart van de basisverbinding**

De **identiteitskaart van de basisverbinding** staat u toe om dossiers van uw bron te doorbladeren en te onderzoeken, die u helpen welke punten identificeren om in te voeren, samen met hun gegevenstypen en formaten.

Als u een basis-verbindings-id wilt maken, verzendt u een POST-aanvraag naar het `/connections` -eindpunt, inclusief de [!DNL Salesforce Marketing Cloud] -verificatiereferenties in de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Salesforce Marketing Cloud] gemaakt.

+++Voorbeeldverzoek weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.host` |  |
| `auth.params.clientId` | De client-id die aan uw [!DNL Salesforce Marketing Cloud] -toepassing is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan de toepassing [!DNL Salesforce Marketing Cloud] is gekoppeld. |
| `connectionSpec.id` | The [!DNL Salesforce Marketing Cloud] connection specification ID: `ea1c2a08-b722-11eb-8529-0242ac130003` . |

+++

+++Voorbeeldreactie weergeven

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Verbinden [!DNL Salesforce Marketing Cloud] met Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../../../landing/multi-cloud.md).

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL Salesforce Marketing Cloud] -account kunt verbinden met Experience Platform op AWS.

### Een basisverbinding maken {#aws-base}

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Salesforce Service Cloud] gemaakt om verbinding te maken met Experience Platform op AWS.

+++Voorbeeld van een aanvraag weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Reactievoorbeeld weergeven

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## Een gegevensstroom maken voor [!DNL Salesforce Marketing Cloud] -gegevens

Nu u met succes uw [!DNL Salesforce Marketing Cloud] rekening hebt verbonden, kunt u [&#x200B; nu tot een dataflow en gegevens van uw marketing automatiseringsleverancier in Experience Platform &#x200B;](../../collect/marketing-automation.md) leiden.