---
keywords: Experience Platform;home;populaire onderwerpen;marketingautomatisering
solution: Experience Platform
title: Ontdek een Systeem van de Automatisering van de Marketing gebruikend de Dienst API van de Stroom
topic-legacy: overview
description: Deze zelfstudie gebruikt de Flow Service API om op zoek te gaan naar systemen voor marketingautomatisering.
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Een systeem voor marketingautomatisering verkennen met de [!DNL Flow Service] API

[!DNL Flow Service] wordt gebruikt voor het verzamelen en centraliseren van klantgegevens uit verschillende bronnen in Adobe Experience Platform. De service biedt een gebruikersinterface en RESTful API waaruit alle ondersteunde bronnen kunnen worden aangesloten.

Deze zelfstudie gebruikt de [!DNL Flow Service] API voor het verkennen van systemen voor marketingautomatisering.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om een verbinding met een marketingautomatiseringssysteem tot stand te brengen met het [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Deze zelfstudie vereist dat u een geldige verbinding hebt met de marketingtoepassing van derden waarvan u gegevens wilt invoeren. Een geldige verbinding heeft betrekking op de verbindingsspecificatie-id en de verbinding-id van uw toepassing. Meer informatie over het maken van een verbinding voor marketingautomatisering en het ophalen van deze waarden vindt u in de [een marketingautomatiseringsbron aansluiten op Platform](../../api/create/marketing-automation/hubspot.md) zelfstudie.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke [!DNL Flow Service], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Uw gegevenstabellen verkennen

Gebruikend de basisverbinding voor uw systeem van de marketing automatisering, kunt u uw gegevenslijsten onderzoeken door verzoeken van de GET uit te voeren. Gebruik de volgende vraag om de weg van de lijst te vinden u wenst om te inspecteren of in te gaan [!DNL Platform].

**API-indeling**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding voor uw marketingautomatiseringssysteem. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie is een serie van lijsten van aan uw systeem van de marketing automatisering. Zoek de tabel waarin u wilt plaatsen [!DNL Platform] en neemt nota van zijn `path` eigenschap, aangezien u het in de volgende stap moet verstrekken om zijn structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## De structuur van een tabel Inspect

Om de structuur van een lijst van uw marketing automatiseringssysteem te inspecteren, voer een verzoek van de GET uit terwijl het specificeren van de weg van een lijst als vraagparameter.

**API-indeling**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De verbinding-id voor uw marketingautomatiseringssysteem. |
| `{TABLE_PATH}` | Het pad van een tabel in uw marketingautomatiseringssysteem. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
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
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
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

Aan de hand van deze zelfstudie hebt u uw systeem voor marketingautomatisering verkend en hebt u het pad gevonden van de tabel waarnaar u wilt verwijzen [!DNL Platform]en heeft informatie over de structuur ervan verkregen. U kunt deze informatie in de volgende zelfstudie gebruiken om [gegevens van uw systeem voor marketingautomatisering verzamelen en in Platform brengen](../collect/marketing-automation.md).
