---
keywords: Experience Platform;home;popular topics;ecommerce;eCommerce
solution: Experience Platform
title: Ontdek een eCommerce-verbinding met de Flow Service API
topic: overview
description: Deze zelfstudie gebruikt de Flow Service API om eCommerce-verbindingen te verkennen.
translation-type: tm+mt
source-git-commit: 4696bcb17427bb50549a315294baf7fbd87ac01d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# Een eCommerce-verbinding verkennen met de [!DNL Flow Service] API

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

In deze zelfstudie wordt de [!DNL Flow Service] API gebruikt om een externe **[!UICONTROL eCommerce]** -verbinding te verkennen.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de [!DNL Platform] diensten.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met een **[!UICONTROL eCommerce]** -verbinding met behulp van de [!DNL Flow Service] API.

### Verbindings-id verkrijgen

Als u de **[!UICONTROL eCommerce]** -verbinding wilt verkennen met [!DNL Platform] API&#39;s, moet u over een geldige verbinding-id beschikken. Als u nog geen verbinding hebt voor de **[!UICONTROL eCommerce]** -verbinding waarmee u wilt werken, kunt u er een maken aan de hand van de volgende zelfstudie:

* [Schopify](../create/ecommerce/shopify.md)

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van [!DNL Experience Platform] problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot [!DNL Flow Service]behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* `Content-Type: application/json`

## Uw gegevenstabellen verkennen

Gebruikend uw **[!UICONTROL eCommerce]** verbindingsidentiteitskaart, kunt u uw gegevenslijsten onderzoeken door verzoeken van de GET uit te voeren. Gebruik de volgende vraag om de weg van de lijst te vinden u wenst om te inspecteren of in te nemen [!DNL Platform].

**API-indeling**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONNECTION_ID}` | Je **[!UICONTROL eCommerce]** -verbindings-id. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een array met tabellen van uw **[!UICONTROL eCommerce]** -verbinding. Zoek de tabel die u wilt invoegen [!DNL Platform] en neem nota van de `path` eigenschap ervan, aangezien u deze in de volgende stap moet opgeven om de structuur te controleren.

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

## De structuur van een tabel Inspect

Om de structuur van een lijst van uw verbinding van de **[!UICONTROL Handel]** te inspecteren, voer een verzoek van de GET uit terwijl het specificeren van de weg van een lijst binnen een `object` vraagparameter.

**API-indeling**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{CONNECTION_ID}` | De verbinding-id van uw **[!UICONTROL eCommerce]** -verbinding. |
| `{TABLE_PATH}` | Het pad van een tabel in uw **[!UICONTROL eCommerce]** -verbinding. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

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

Door deze zelfstudie te volgen, hebt u uw verbinding van de **[!UICONTROL eCommerce]** onderzocht, het weg van de lijst gevonden u wenst in te nemen [!DNL Platform], en informatie over zijn structuur verkregen. U kunt deze informatie in de volgende zelfstudie gebruiken om eCommerce-gegevens te [verzamelen en in Platform](../collect/ecommerce.md)te brengen.
