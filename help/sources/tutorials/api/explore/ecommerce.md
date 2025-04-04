---
keywords: Experience Platform;home;populaire onderwerpen;e-commerce
solution: Experience Platform
title: Ontdek een eCommerce-verbinding met behulp van de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om eCommerce-verbindingen te verkennen.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# Een eCommerce-verbinding verkennen met de API [!DNL Flow Service]

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API om een verbinding van derden met **[!UICONTROL eCommerce]** te verkennen.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md) [!DNL Experience Platform] : hiermee kunt u gegevens uit verschillende bronnen invoegen en binnenkomende gegevens structureren, labelen en verbeteren met [!DNL Experience Platform] -services.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Experience Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten als u verbinding wilt maken met een **[!UICONTROL eCommerce]** -verbinding met de [!DNL Flow Service] API.

### Verbindings-id verkrijgen

Als u de **[!UICONTROL eCommerce]** -verbinding wilt verkennen met [!DNL Experience Platform] -API&#39;s, moet u over een geldige verbinding-id beschikken. Als u nog geen verbinding hebt voor de **[!UICONTROL eCommerce]** -verbinding waarmee u wilt werken, kunt u een verbinding maken via de volgende zelfstudie:

* [Schopify](../create/ecommerce/shopify.md)

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief bronnen die tot [!DNL Flow Service] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* `Content-Type: application/json`

## Uw gegevenstabellen verkennen

Met de **[!UICONTROL eCommerce]** -verbindings-id kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende aanroep om het pad te zoeken van de tabel die u wilt inspecteren of waarin u wilt opnemen [!DNL Experience Platform].

**API formaat**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONNECTION_ID}` | Uw **[!UICONTROL eCommerce]** verbinding-id. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord retourneert een array met tabellen van uw **[!UICONTROL eCommerce]** -verbinding. Zoek de tabel die u wilt opnemen in [!DNL Experience Platform] en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet opgeven om de structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een tabel controleren

Als u de structuur van een tabel wilt inspecteren vanuit uw **[!UICONTROL eCommerce]** -verbinding, voert u een GET-aanvraag uit terwijl u het pad van een tabel opgeeft binnen een `object` -queryparameter.

**API formaat**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De verbinding-id van uw **[!UICONTROL eCommerce]** -verbinding. |
| `{TABLE_PATH}` | Het pad van een tabel binnen uw **[!UICONTROL eCommerce]** -verbinding. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
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
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u de **[!UICONTROL eCommerce]** -verbinding verkend, het pad gevonden van de tabel waarin u wilt opnemen in [!DNL Experience Platform] en informatie verkregen over de structuur ervan. U kunt deze informatie in het volgende leerprogramma gebruiken [ eCommerce-gegevens verzamelen en het brengen in Experience Platform ](../collect/ecommerce.md).
