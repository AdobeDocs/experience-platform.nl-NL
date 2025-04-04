---
keywords: Experience Platform;home;populaire onderwerpen;Apache Hadoop Distributed File System;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: Een Apache HDFS-basisverbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u een Apache Hadoop Distributed File System met de Flow Service API kunt verbinden.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Een [!DNL Apache] HDFS-basisverbinding maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De Apache HDFS-connector is in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Apache Hadoop Distributed File System] tot stand te brengen (verder die als &quot; [!DNL HDFS] wordt bedoeld&quot;) gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL HDFS] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

| Credentials | Beschrijving |
| ---------- | ----------- |
| `url` | De URL definieert de auteparams die vereist zijn om anoniem verbinding te maken met [!DNL HDFS] . Voor meer informatie over hoe te om deze waarde te verkrijgen, verwijs naar [ dit  [!DNL HDFS]  document ](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL AdWords] is: `54e221aa-d342-4707-bcff-7a4bceef0001` . |

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL HDFS] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL HDFS] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.url` | De URL die automatische parameters definieert die vereist zijn voor anoniem verbinden met [!DNL HDFS] |
| `connectionSpec.id` | The [!DNL HDFS] connection specification ID: `54e221aa-d342-4707-bcff-7a4bceef0001` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL HDFS] -verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze identiteitskaart in het volgende leerprogramma gebruiken aangezien u leert [ een opslag van de derdewolk onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
