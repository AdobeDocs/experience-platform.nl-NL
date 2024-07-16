---
keywords: Experience Platform;thuis;populaire onderwerpen;advertentiesysteem;Advertising-systeem
solution: Experience Platform
title: Een Advertising-systeem verkennen met de Flow Service API
description: De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten. Deze zelfstudie gebruikt de Flow Service API om advertentiesystemen te verkennen.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Een advertentiesysteem verkennen met de API van [!DNL Flow Service]

Als er een basisverbinding is gemaakt, kunt u nu de unieke basis-verbindings-id gebruiken om te navigeren en de gegevensstructuur en inhoud van uw bron te verkennen. Zo kunt u de specifieke items en hun respectievelijke gegevenstypen en indelingen identificeren voordat u een gegevensstroom maakt en deze naar Adobe Experience Platform overbrengt.

Dit leerprogramma gebruikt [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/) om reclamesystemen te onderzoeken.

## Aan de slag

>[!IMPORTANT]
>
>Voor deze zelfstudie moet u beschikken over de unieke basis-verbindings-id voor uw advertentiebron. Als u dit identiteitskaart niet hebt, zie het leerprogramma op [ verbindend een reclamebron aan Platform ](../../api/create/advertising/ads.md) leerprogramma.

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een advertentiesysteem met de API [!DNL Flow Service] .

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../landing/api-guide.md).

## Uw gegevenstabellen verkennen

Met de basisverbinding voor uw advertentiesysteem kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende aanroep om het pad te zoeken van de tabel die u wilt inspecteren of waarin u wilt opnemen [!DNL Platform].

**API formaat**

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord is een serie van lijsten van aan uw reclamesysteem. Zoek de tabel die u wilt opnemen in [!DNL Platform] en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet opgeven om de structuur te inspecteren.

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

**API formaat**

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert de structuur van een tabel. De details betreffende elk van de kolommen van de lijst worden gevestigd binnen elementen van de `columns` serie.

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

Aan de hand van deze zelfstudie hebt u uw advertentiesysteem verkend, het pad van de tabel gevonden die u wilt doorgeven aan [!DNL Platform] en hebt u informatie gekregen over de structuur ervan. U kunt deze informatie in het volgende leerprogramma gebruiken [ gegevens van uw reclamesysteem verzamelen en het in Platform ](../collect/advertising.md) brengen.
