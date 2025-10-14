---
title: Azure Synapse-analyse met behulp van de Flow Service-API verbinden met Experience Platform
description: Leer hoe u uw Azure Synapse Analytics-account met Experience Platform kunt verbinden via API's.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>De [!DNL Azure Synapse Analytics] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze gids om te leren hoe te om uw [!DNL Azure Synapse Analytics] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Azure Synapse Analytics] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Lees het [[!DNL Azure Synapse Analytics]  overzicht &#x200B;](../../../../connectors/databases/synapse-analytics.md#prerequisites) voor informatie over authentificatie.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

## Verbinden [!DNL Azure Synapse Analytics] met Experience Platform

Lees het volgende voor meer informatie over het maken van een basisverbinding en het verbinden van uw [!DNL Azure Synapse Analytics] -account met Experience Platform.

### Een basisverbinding maken

A **basisverbinding** slaat zeer belangrijke informatie op die uw bronsysteem met Adobe Experience Platform verbindt. Dit omvat het volgende:

* Verificatiegegevens van uw bron
* De huidige status van de verbinding
* Een unieke **identiteitskaart van de basisverbinding**

De **identiteitskaart van de basisverbinding** staat u toe om dossiers van uw bron te doorbladeren en te onderzoeken, die u helpen welke punten identificeren om in te voeren, samen met hun gegevenstypen en formaten.

Als u een basis-verbindings-id wilt maken, verzendt u een POST-aanvraag naar het `/connections` -eindpunt, inclusief de [!DNL Azure Synapse Analytics] -verificatiereferenties in de aanvraagparameters.

**API formaat**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB  Reeks Gebaseerde Authentificatie van de Verbinding ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Azure Synapse Analytics] gemaakt met verificatie op basis van een verbindingstekenreeks.

+++Voorbeeldverzoek weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks waarmee verbinding wordt gemaakt met [!DNL Azure Synapse Analytics] . Het patroon van de [!DNL Azure Synapse Analytics] verbindingstekenreeks is `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30` . |
| `connectionSpec.id` | De [!DNL Azure Synapse Analytics] -id van de verbindingsspecificatie is: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Voorbeeldreactie van weergave

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB  Belangrijkste Belangrijke Gebaseerde Authentificatie van de Dienst ]

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Azure Synapse Analytics] gemaakt met behulp van op servicetoets gebaseerde verificatie.

**Verzoek**

+++Voorbeeldverzoek weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| Credentials | Beschrijving |
| --- | --- |
| `auth.params.server` | De volledig gekwalificeerde domeinnaam van het SQL-eindpunt van [!DNL Azure Synapse Analytics] . |
| `auth.params.database` | De naam van de specifieke database in de [!DNL Azure Synapse Analytics] -werkruimte. |
| `auth.params.tenant` | De [!DNL Azure Active Directory] huurder-id die aan uw [!DNL Azure] -abonnement is gekoppeld. |
| `auth.params.servicePrincipalId` | De client-id van een [!DNL Azure Active Directory] -toepassing. |
| `auth.params.servicePrincipalKey` | Het cliëntgeheim of wachtwoord verbonden aan het de diensthoofd. |
| `connectSpec.id` | De verbindingsspecificatie-id van [!DNL Azure Synapse Analytics] . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Voorbeeldreactie van weergave

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Azure Synapse Analytics] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
