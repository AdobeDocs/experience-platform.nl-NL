---
title: Een database verkennen met de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om de inhoud en de bestandsstructuur van een database van derden te verkennen.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 46e1a62e558a209ffed4a693cfd71ad5e76d7d98
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---

# Een database verkennen met de API van [!DNL Flow Service]

In deze zelfstudie wordt de API van [!DNL Flow Service] gebruikt om de inhoud en de bestandsstructuur van een database van derden te bekijken.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een database van derden met de [!DNL Flow Service] API.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../landing/api-guide.md).

## Uw gegevenstabellen verkennen

Met de verbindings-id voor uw database kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende vraag om de weg van de lijst te vinden u wenst om te inspecteren of in Experience Platform in te gaan.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De verbinding-id van uw databasebron. |

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert een array met tabellen uit uw database. Zoek de tabel die u naar Experience Platform wilt brengen en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet verstrekken om de structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een tabel controleren

Om de structuur van een lijst van uw gegevensbestand te inspecteren, voer een verzoek van GET terwijl het specificeren van de weg van een lijst als vraagparameter uit.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van een databaseverbinding. |
| `{TABLE_PATH}` | Het pad van een tabel. |

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert de structuur van de opgegeven tabel. De details betreffende elk van de kolommen van de lijst worden gevestigd binnen elementen van de `columns` serie.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [],
    "cdcMetadata": {
      "columnDetected": true
    }
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u uw database verkend, het pad van de tabel gevonden die u in Experience Platform wilt opnemen en hebt u informatie gekregen over de structuur ervan. U kunt deze informatie in het volgende leerprogramma gebruiken [&#x200B; gegevens van uw gegevensbestand verzamelen en het brengen in Experience Platform &#x200B;](../collect/database-nosql.md).
