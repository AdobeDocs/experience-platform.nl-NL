---
keywords: Experience Platform;thuis;populaire onderwerpen;advertentiesysteem;Reclamesysteem
solution: Experience Platform
title: Een advertentiesysteem verkennen met de Flow Service API
topic-legacy: overview
description: De Flow Service wordt gebruikt om klantgegevens te verzamelen en te centraliseren uit verschillende bronnen binnen Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten. Deze zelfstudie gebruikt de Flow Service API om advertentiesystemen te verkennen.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Een reclamesysteem verkennen met de [!DNL Flow Service] API

Als er een basisverbinding is gemaakt, kunt u nu de unieke basis-verbindings-id gebruiken om te navigeren en de gegevensstructuur en inhoud van uw bron te verkennen. Zo kunt u de specifieke items en hun respectievelijke gegevenstypen en indelingen identificeren voordat u een gegevensstroom maakt en deze naar Adobe Experience Platform overbrengt.

Deze zelfstudie gebruikt de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) het verkennen van reclamesystemen.

## Aan de slag

>[!IMPORTANT]
>
>Voor deze zelfstudie moet u beschikken over de unieke basis-verbindings-id voor uw advertentiebron. Als u deze id niet hebt, raadpleegt u de zelfstudie op [een reclamebron verbinden met Platform](../../api/create/advertising/ads.md) zelfstudie.

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om een verbinding met een advertentiesysteem tot stand te brengen met het [!DNL Flow Service] API.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../landing/api-guide.md).

## Uw gegevenstabellen verkennen

Met de basisverbinding voor uw advertentiesysteem kunt u uw gegevenstabellen verkennen door GET-aanvragen uit te voeren. Gebruik de volgende vraag om de weg van de lijst te vinden u wenst om te inspecteren of in te gaan [!DNL Platform].

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord is een serie van lijsten van aan uw reclamesysteem. Zoek de tabel waarin u wilt plaatsen [!DNL Platform] en neemt nota van zijn `path` eigenschap, aangezien u het in de volgende stap moet verstrekken om zijn structuur te inspecteren.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de structuur van een tabel. De details betreffende elk van de kolommen van de lijst worden gevestigd binnen elementen van `columns` array.

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

Door deze zelfstudie te volgen, hebt u uw advertentiesysteem verkend, vond de weg van de lijst u binnen wilt brengen [!DNL Platform]en heeft informatie over de structuur ervan verkregen. U kunt deze informatie in de volgende zelfstudie gebruiken om [gegevens van uw advertentiesysteem verzamelen en in Platform brengen](../collect/advertising.md).
