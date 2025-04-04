---
keywords: Experience Platform;home;populaire onderwerpen;database van derden;databasestroom-service
solution: Experience Platform
title: Een database verkennen met de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om de inhoud en de bestandsstructuur van een database van derden te verkennen.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Een database verkennen met de API van [!DNL Flow Service]

In deze zelfstudie wordt de API van [!DNL Flow Service] gebruikt om de inhoud en de bestandsstructuur van een database van derden te bekijken.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een database van derden met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Deze zelfstudie vereist dat u een geldige verbinding hebt met de database van derden waarvan u gegevens wilt invoeren. Een geldige verbinding heeft betrekking op de verbindingsspecificatie-id en de verbinding-id van uw database. Meer informatie over het creëren van een gegevensbestandverbinding en het terugwinnen van deze waarden kan in het [ overzicht van bronschakelaars ](./../../../home.md#database) worden gevonden.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Het voltooien van het authentificatieleerprogramma verstrekt de waarden voor elk van de vereiste kopballen in alle vraag E [!DNL xperience Experience Platform] API, zoals hieronder getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* `Content-Type: application/json`

## Uw gegevenstabellen verkennen

Met de verbindings-id voor uw database kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende aanroep om het pad te zoeken van de tabel die u wilt inspecteren of waarin u wilt opnemen [!DNL Experience Platform].

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

Een geslaagde reactie retourneert een array met tabellen uit uw database. Zoek de tabel die u wilt opnemen in [!DNL Experience Platform] en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet opgeven om de structuur te inspecteren.

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
    }
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u uw database verkend, het pad van de tabel gevonden waarin u de gegevens wilt invoeren [!DNL Experience Platform] en informatie verkregen over de structuur ervan. U kunt deze informatie in het volgende leerprogramma gebruiken [ gegevens van uw gegevensbestand verzamelen en het brengen in Experience Platform ](../collect/database-nosql.md).
