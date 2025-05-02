---
title: Connect Azure-databases naar Experience Platform met behulp van de Flow Service API
description: Leer hoe u Azure Databricks met behulp van API's verbindt met Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 5637a12d5f9cc14b6cf3d88f018aa92de06ab739
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL Azure Databricks]

>[!IMPORTANT]
>
>De [!DNL Azure Databricks] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.

Lees deze gids om te leren hoe te om uw [!DNL Azure Databricks] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Lees de gids op [ hoe te beginnen met Experience Platform APIs ](../../../../../landing/api-guide.md) voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken.

### Voorwaarden configureren

Lees het [[!DNL Databricks]  overzicht ](../../../../connectors/databases/databricks.md) voor informatie de in de eerste plaats vereiste configuraties die eerst moeten worden voltooid, alvorens u uw rekening met Experience Platform kunt verbinden.

### Vereiste referenties verzamelen

Geef waarden op voor de volgende referenties om [!DNL Databricks] te verbinden met Experience Platform.

| Credentials | Beschrijving |
| --- | --- |
| `domain` | De URL van de [!DNL Databricks] -werkruimte. Bijvoorbeeld `https://adb-1234567890123456.7.azuredatabricks.net` . |
| `clusterId` | De id van uw cluster in [!DNL Databricks] . Deze cluster moet al een bestaande cluster zijn en moet een interactief cluster zijn. |
| `accessToken` | Het toegangstoken dat uw [!DNL Databricks] account verifieert. U kunt uw toegangstoken produceren gebruikend de [!DNL Databricks] werkruimte. |
| `database` | De naam van uw database in het delta-meer. |
| `connectionSpec.Id` | De verbindingsSPEC identiteitskaart keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Databricks] is `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b` . |

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de juiste verificatiegegevens voor uw [!DNL Databricks] -account op.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor een [!DNL Databricks] -bron gemaakt met behulp van toegangstoken-verificatie.

+++aanvraagvoorbeeld weergeven

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.domain` | De URL van de [!DNL Databricks] -werkruimte. |
| `auth.params.clusterId` | De id van uw cluster in [!DNL Databricks] . Deze cluster moet al een bestaande cluster zijn en moet een interactief cluster zijn |
| `auth.params.accessToken` | Het toegangstoken dat uw [!DNL Databricks] account verifieert. |
| `auth.params.database` | De naam van uw database in het delta-meer. |
| `connectionSpec.id` | De [!DNL Databricks] connection spec ID. |

+++

**Reactie**

Een geslaagde reactie retourneert de zojuist gemaakte verbinding, inclusief de id van de basisverbinding.

+++Respons voorbeeld weergeven

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding gemaakt tussen uw [!DNL Databricks] -account en Experience Platform. U kunt de zojuist gegenereerde basis verbindings-id gebruiken in de volgende zelfstudies:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
