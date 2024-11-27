---
keywords: Experience Platform;home;populaire onderwerpen;couchbase;Couchbase
solution: Experience Platform
title: Een Couchbase-verbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Couchbase aan Adobe Experience Platform koppelt met behulp van de Flow Service API.
exl-id: 625e3acf-fc27-44cf-b4e6-becf1d107ff2
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Een [!DNL Couchbase] basisverbinding maken met de [!DNL Flow Service] API

>[!WARNING]
>
>De bron [!DNL Couchbase] wordt eind juni 2025 vervangen.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Couchbase] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Couchbase] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Couchbase] . Het patroon van de verbindingstekenreeks voor [!DNL Couchbase] is `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];` . Voor meer informatie bij het verwerven van een verbindingskoord, verwijs naar [ dit document van Couchbase ](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Couchbase] is `1fe283f6-9bec-11ea-bb37-0242ac130002` . |

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Couchbase] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Couchbase] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Couchbase test connection",
        "description": "A test connection for a Couchbase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks waarmee verbinding wordt gemaakt met een [!DNL Couchbase] -account. Het patroon van de verbindingstekenreeks is: `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];` . |
| `connectionSpec.id` | The [!DNL Couchbase] connection specification ID: `1fe283f6-9bec-11ea-bb37-0242ac130002` . |

**Reactie**

Een succesvolle reactie keert de details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Couchbase] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
