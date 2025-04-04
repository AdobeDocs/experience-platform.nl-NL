---
keywords: Experience Platform;home;populaire onderwerpen;protocol
solution: Experience Platform
title: Ontdek een protocolsysteem met behulp van de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om protocoltoepassingen te verkennen.
exl-id: e4b24312-543e-4014-aa53-e8ca9c620950
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Een protocolsysteem verkennen met de API van [!DNL Flow Service]

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om protocoltoepassingen te verkennen.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een protocoltoepassing met de [!DNL Flow Service] API.

### Een basisverbinding verkrijgen

Als u uw protocolsysteem wilt verkennen met behulp van [!DNL Experience Platform] API&#39;s, moet u over een geldige basis-verbindings-id beschikken. Als u nog geen basisverbinding hebt voor het protocolsysteem waarmee u wilt werken, kunt u een verbinding maken aan de hand van de volgende zelfstudie:

* [Generic OData](../create/protocols/odata.md)

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Uw gegevenstabellen verkennen

Met de verbindings-id voor uw protocoltoepassing kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende aanroep om het pad te zoeken van de tabel die u wilt inspecteren of waarin u wilt opnemen [!DNL Experience Platform].

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van een protocolbasisverbinding. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/a5c6b647-e784-4b58-86b6-47e784ab580b/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een serie van lijsten van uw protocoltoepassing terug. Zoek de tabel die u wilt opnemen in [!DNL Experience Platform] en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet opgeven om de structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "Categories",
        "path": "Categories",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "CustomerDemographics",
        "path": "CustomerDemographics",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Customers",
        "path": "Customers",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Orders",
        "path": "Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een tabel controleren

Om de structuur van een lijst van uw protocoltoepassing te inspecteren, voer een verzoek van GET terwijl het specificeren van de weg van een lijst als vraagparameter uit.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De verbindings-id van uw protocoltoepassing. |
| `{TABLE_PATH}` | Het pad van een tabel in uw protocoltoepassing. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/a5c6b647-e784-4b58-86b6-47e784ab580b/explore?objectType=table&object=Orders' \
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
                "name": "OrderID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "CustomerID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "EmployeeID",
                "type": "integer",
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "OrderDate",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de protocoltoepassing verkend, het pad van de tabel gevonden waarin u de code wilt opnemen [!DNL Experience Platform] en informatie verkregen over de structuur ervan. U kunt deze informatie in het volgende leerprogramma gebruiken [ gegevens van uw protocoltoepassing verzamelen en het brengen in Experience Platform ](../collect/protocols.md).
