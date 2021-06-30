---
keywords: Experience Platform;thuis;populaire onderwerpen;advertentiesysteem;Reclamesysteem
solution: Experience Platform
title: Een advertentiesysteem verkennen met de Flow Service API
topic-legacy: overview
description: De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten. Deze zelfstudie gebruikt de Flow Service API om advertentiesystemen te verkennen.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 8aa8dfcc4f8a36d0898a9cc079bd98b89e3589a1
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# Een advertentiesysteem verkennen met de API [!DNL Flow Service]

Als er een basisverbinding is gemaakt, kunt u nu de unieke basis-verbindings-id gebruiken om te navigeren en de gegevensstructuur en inhoud van uw bron te verkennen. Zo kunt u de specifieke items en hun respectievelijke gegevenstypen en indelingen identificeren voordat u een gegevensstroom maakt en deze naar Adobe Experience Platform overbrengt.

Deze zelfstudie gebruikt de [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). het verkennen van reclamesystemen.

## Aan de slag

>[!IMPORTANT]

Voor deze zelfstudie moet u beschikken over de unieke basis-verbindings-id voor uw advertentiebron. Als u deze id niet hebt, raadpleegt u de zelfstudie [Een advertentiebron verbinden met Platform](../../api/create/advertising/ads.md).

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om verbinding te kunnen maken met een advertentiesysteem met de API [!DNL Flow Service].

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../landing/api-guide.md).

## Uw gegevenstabellen verkennen

Met de basisverbinding voor uw advertentiesysteem kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende vraag om de weg van de lijst te vinden u wenst om te inspecteren of in [!DNL Platform] in te gaan.

**API-indeling**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding voor uw advertentiesysteem. |

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord is een serie van lijsten van aan uw reclamesysteem. Zoek de lijst u in [!DNL Platform] wilt brengen en nota nemen van zijn `path` bezit, aangezien u het in de volgende stap moet verstrekken om zijn structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een tabel Inspect

Om de structuur van een lijst van uw reclamesysteem te inspecteren, voer een verzoek van de GET uit terwijl het specificeren van de weg van een lijst als vraagparameter.

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De verbinding-id voor uw advertentiesysteem. |
| `{TABLE_PATH}` | Het pad van een tabel in uw advertentiesysteem. |

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de structuur van een tabel. De details betreffende elk van de kolommen van de lijst worden gevestigd binnen elementen van `columns` serie.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
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

Aan de hand van deze zelfstudie hebt u uw advertentiesysteem verkend, het pad van de tabel gevonden die u wilt doorgeven naar [!DNL Platform] en hebt u informatie gekregen over de structuur ervan. U kunt deze informatie in de volgende zelfstudie gebruiken om gegevens van uw advertentiesysteem te verzamelen en in Platform te brengen](../collect/advertising.md).[
