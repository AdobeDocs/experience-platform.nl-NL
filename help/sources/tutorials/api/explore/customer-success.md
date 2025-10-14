---
keywords: Experience Platform;home;populaire onderwerpen;cs;CS;systeem voor klantsucces
solution: Experience Platform
title: Ontdek een systeem met succes van de Klant met behulp van de Flow Service API
description: In deze zelfstudie wordt de Flow Service API gebruikt om de systemen van Customer Success (CS) te verkennen.
exl-id: 453be69d-3d72-4987-81cd-67fa3be7ee59
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Ontdek het successysteem van een klant met de API van [!DNL Flow Service]

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de [!DNL Flow Service] API gebruikt om de systemen voor Klantsucces (CS) te verkennen.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een CS-systeem met de API [!DNL Flow Service] .

### Een basisverbinding verkrijgen

Als u uw CS-systeem wilt verkennen met API&#39;s van [!DNL Experience Platform] , moet u beschikken over een geldige basis-verbindings-id. Als u nog geen basisverbinding hebt voor het CS-systeem waarmee u wilt werken, kunt u een verbinding maken via de volgende zelfstudies:

* [Salesforce Service Cloud](../create/customer-success/salesforce-service-cloud.md)
* [ServiceNow](../create/customer-success/servicenow.md)

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [&#x200B; hoe te om voorbeeld API vraag &#x200B;](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [&#x200B; authentificatieleerprogramma &#x200B;](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Uw gegevenstabellen verkennen

Met de basisverbinding voor uw CS-systeem kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende aanroep om het pad te zoeken van de tabel die u wilt inspecteren of waarin u wilt opnemen [!DNL Experience Platform].

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van een CS-basisverbinding. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een serie van lijsten van uw systeem terug CS. Zoek de tabel die u wilt opnemen in [!DNL Experience Platform] en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet opgeven om de structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "Accepted Event Relation",
        "path": "AcceptedEventRelation",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account",
        "path": "Account",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Change Event",
        "path": "AccountChangeEvent",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Clean Info",
        "path": "AccountCleanInfo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een tabel controleren

Om de structuur van een lijst van uw systeem te inspecteren CS, voer een verzoek van GET terwijl het specificeren van de weg van een lijst als vraagparameter uit.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van een CS-basisverbinding. |
| `{TABLE_PATH}` | Het pad van een tabel. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=table&object=test1.Mytable' \
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
                "name": "Id",
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
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u uw CS-systeem verkend, het pad gevonden van de tabel waarin u wilt opnemen [!DNL Experience Platform] en informatie verkregen over de structuur ervan. U kunt deze informatie in het volgende leerprogramma gebruiken [&#x200B; gegevens van uw systeem van CS verzamelen en het brengen in Experience Platform &#x200B;](../collect/customer-success.md).
