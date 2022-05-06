---
keywords: Experience Platform;huis;populaire onderwerpen;derdegegevensbestand;de dienst van de gegevensbestandstroom
solution: Experience Platform
title: Een database verkennen met de Flow Service API
topic-legacy: overview
description: Deze zelfstudie gebruikt de Flow Service API om de inhoud en de bestandsstructuur van een database van derden te verkennen.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Een database verkennen met de opdracht [!DNL Flow Service] API

Deze zelfstudie gebruikt de [!DNL Flow Service] API voor het verkennen van de inhoud en de bestandsstructuur van een database van derden.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes met een derdegegevensbestand te verbinden gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Deze zelfstudie vereist dat u een geldige verbinding hebt met de database van derden waarvan u gegevens wilt invoeren. Een geldige verbinding heeft betrekking op de verbindingsspecificatie-id en de verbinding-id van uw database. Meer informatie over het maken van een databaseverbinding en het ophalen van deze waarden vindt u in de [overzicht van bronconnectors](./../../../home.md#database).

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Voltooiend de authentificatieleerprogramma verstrekt de waarden voor elk van de vereiste kopballen in alle E[!DNL xperience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Uw gegevenstabellen verkennen

Met de verbindings-id voor uw database kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende vraag om de weg van de lijst te vinden u wenst om te inspecteren of in te gaan [!DNL Platform].

**API-indeling**

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

**Antwoord**

Een geslaagde reactie retourneert een array met tabellen uit uw database. Zoek de tabel waarin u wilt plaatsen [!DNL Platform] en neemt nota van zijn `path` eigenschap, aangezien u het in de volgende stap moet verstrekken om zijn structuur te inspecteren.

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

## De structuur van een tabel Inspect

Om de structuur van een lijst van uw gegevensbestand te inspecteren, voer een verzoek van de GET uit terwijl het specificeren van de weg van een lijst als vraagparameter.

**API-indeling**

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

**Antwoord**

Een geslaagde reactie retourneert de structuur van de opgegeven tabel. De details betreffende elk van de kolommen van de lijst worden gevestigd binnen elementen van `columns` array.

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

Door deze zelfstudie te volgen, hebt u uw database verkend, hebt u het pad gevonden van de tabel waarin u wilt opnemen [!DNL Platform]en heeft informatie over de structuur ervan verkregen. U kunt deze informatie in de volgende zelfstudie gebruiken om [gegevens van uw database verzamelen en in Platform brengen](../collect/database-nosql.md).
