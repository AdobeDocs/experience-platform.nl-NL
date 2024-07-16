---
title: Een Microsoft SQL Server Base Connection maken met de Flow Service API
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een Microsoft SQL Server met behulp van de Flow Service API.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Een [!DNL Microsoft] SQL Server-basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees dit leerprogramma leren hoe te om een basisverbinding voor [!DNL Microsoft SQL Server] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Microsoft SQL Server] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen {#gather-required-credentials}

Als u verbinding wilt maken met [!DNL Microsoft SQL Server] , moet u de volgende eigenschap voor verbinding opgeven:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL Microsoft SQL Server] account is gekoppeld. Het patroon van de verbindingstekenreeks is afhankelijk van de servernaam of de instantienaam van de gegevensbron:<ul><li>Verbindingstekenreeks met servernaam: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Verbindingstekenreeks met instantienaam:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Microsoft SQL Server] is `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` . |

Voor meer informatie over het verkrijgen van een verbindingskoord, verwijs naar dit [[!DNL Microsoft SQL Server]  document ](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Microsoft SQL Server] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Microsoft SQL Server] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for sql-server",
      "description": "Base connection for sql-server",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL Microsoft SQL Server] account is gekoppeld. Lees de sectie over [ verzamelen vereiste geloofsbrieven ](#gather-required-credentials) voor meer informatie. |
| `connectionSpec.id` | De [!DNL Microsoft SQL Server] -id van de verbindingsspecificatie is: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw database te verkennen in de volgende zelfstudie.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Microsoft SQL Server] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)