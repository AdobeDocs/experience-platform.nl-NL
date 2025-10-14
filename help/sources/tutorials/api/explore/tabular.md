---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;API;verkennen;flowservice
title: Een Source in tabelvorm verkennen met de Flow Service API
description: Deze zelfstudie gebruikt de Flow Service API om de inhoud en structuur van een op tabellen gebaseerde bron te verkennen.
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 1%

---

# Gegevenstabellen verkennen met de API [!DNL Flow Service]

Deze zelfstudie biedt stappen voor het verkennen en voorvertonen van de structuur en inhoud van uw gegevenstabellen met behulp van de [[!DNL Flow Service] &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
> Als u uw gegevenstabellen wilt verkennen, moet u al over een geldige basis-verbindings-id voor een tabelbron beschikken. Als u deze id niet hebt, raadpleegt u de volgende zelfstudies voor stappen voor het maken van een basis-verbindings-id voor een tabelbron: <ul><li>[&#x200B; Advertising &#x200B;](../../../home.md#advertising)</li><li>[&#x200B; CRM &#x200B;](../../../home.md#customer-relationship-management)</li><li>[&#x200B; succes van de Klant &#x200B;](../../../home.md#customer-success)</li><li>[Database](../../../home.md#database)</li><li>[&#x200B; e-commerce &#x200B;](../../../home.md#ecommerce)</li><li>[&#x200B; de automatisering van de Marketing &#x200B;](../../../home.md#marketing-automation)</li><li>[&#x200B; Betalingen &#x200B;](../../../home.md#payments)</li><li>[&#x200B; Protocollen &#x200B;](../../../home.md#protocols)</li></ul>

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../landing/api-guide.md).

## Uw gegevenstabellen verkennen

U kunt informatie over de structuur van uw gegevenstabellen ophalen door een GET-aanvraag in te dienen bij de [!DNL Flow Service] API en de basis-verbindings-id van uw bron op te geven.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbindings-id van uw bron. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert een array met tabellen uit uw bron. Zoek de tabel die u naar Experience Platform wilt brengen en neem nota van de eigenschap `path` ervan, aangezien u deze in de volgende stap moet verstrekken om de structuur te inspecteren.

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## De structuur van een tabel controleren

Om de inhoud van uw gegevenslijsten te inspecteren, voer een verzoek van GET aan [!DNL Flow Service] API uit terwijl het specificeren van de weg van een lijst als vraagparameter.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbindings-id van uw bron. |
| `{TABLE_PATH}` | De eigenschap path van de tabel die u wilt inspecteren. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie retourneert informatie over de inhoud en structuur van de opgegeven tabel. De details betreffende elk van de kolommen van de lijst worden gevestigd binnen elementen van de `columns` serie.

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
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## Volgende stappen

Door dit leerprogramma te volgen, hebt u informatie over de structuur en de inhoud van uw gegevenslijsten verzameld. Bovendien hebt u het pad naar de tabel opgehaald dat u in Experience Platform wilt opnemen. Met deze informatie kunt u een bronverbinding en een gegevensstroom maken om uw gegevens over te brengen naar Experience Platform. Zie de volgende zelfstudies voor specifieke stappen voor het maken van een bronverbinding en een gegevensstroom met de [!DNL Flow Service] API:

* [Advertising-bronnen](../collect/advertising.md)
* [CRM-bronnen](../collect/crm.md)
* [Klantsuccesbronnen](../collect/customer-success.md)
* [Databasebronnen](../collect/database-nosql.md)
* [E-commercebronnen](../collect/ecommerce.md)
* [Marketingautomatiseringsbronnen](../collect/marketing-automation.md)
* [Betalingsbronnen](../collect/payments.md)
* [Bronnen voor protocollen](../collect/protocols.md)
