---
keywords: Experience Platform;home;populaire onderwerpen;betaling
solution: Experience Platform
title: Een betalingssysteem verkennen met de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om betalingstoepassingen te verkennen.
exl-id: 7d0231de-46c0-49df-8a10-aeb42a2c8822
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Een betalingssysteem verkennen met de API van [!DNL Flow Service]

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om betalingstoepassingen te verkennen.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een betalingstoepassing met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

U moet een actieve verbinding met een betalingstoepassing hebben om de bestanden en de bestandsstructuur van uw bron te kunnen bekijken. Lees de volgende documenten voor meer informatie:

* [[!DNL Square]](../create/payments/square.md)
* [[!DNL Stripe]](../create/payments/stripe.md)

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

Met de verbindings-id voor uw betalingssysteem kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende aanroep om het pad te zoeken van de tabel die u wilt inspecteren of waarin u wilt opnemen [!DNL Experience Platform].

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van een verbinding met een betalingsbasis. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert een array met tabellen van uw betalingssysteem. Zoek de tabel die u wilt opnemen in [!DNL Experience Platform] en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet opgeven om de structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "Stripe.Billing_Plans",
        "path": "Stripe.Billing_Plans",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition",
        "path": "Stripe.Billing_Plans_Payment_Definition",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "path": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Catalog_Products",
        "path": "Stripe.Catalog_Products",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een tabel controleren

Om de structuur van een lijst van uw betalingssysteem te inspecteren, voer een verzoek van GET terwijl het specificeren van de weg van een lijst als vraagparameter uit.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | De verbinding-id van uw betalingssysteem. |
| `{TABLE_PATH}` | Het pad van een tabel in uw betalingssysteem. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
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
                "name": "Product_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Product_Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Description",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Type",
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

Aan de hand van deze zelfstudie hebt u uw betalingssysteem verkend, het pad van de tabel gevonden waarin u de gegevens wilt invoeren [!DNL Experience Platform] en hebt u informatie ontvangen over de structuur ervan. U kunt deze informatie in het volgende leerprogramma gebruiken [ gegevens van uw betalingssysteem verzamelen en het brengen in Experience Platform ](../collect/payments.md).
