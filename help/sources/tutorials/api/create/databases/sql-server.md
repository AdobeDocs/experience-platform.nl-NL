---
title: Een Microsoft SQL Server Base Connection maken met de Flow Service API
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een Microsoft SQL Server met behulp van de Flow Service API.
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Een [!DNL Microsoft] SQL Server-basisverbinding met behulp van [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees deze zelfstudie om te leren hoe u een basisverbinding maakt voor [!DNL Microsoft SQL Server] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Microsoft SQL Server] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen {#gather-required-credentials}

Als u verbinding wilt maken met [!DNL Microsoft SQL Server]moet u de volgende eigenschap voor de verbinding opgeven:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL Microsoft SQL Server] account. Het patroon van de verbindingstekenreeks is afhankelijk van de servernaam of de instantienaam van de gegevensbron:<ul><li>Verbindingstekenreeks met servernaam: `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>Verbindingstekenreeks met instantienaam:`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Microsoft SQL Server] is `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

Raadpleeg deze voor meer informatie over het verkrijgen van een verbindingstekenreeks [[!DNL Microsoft SQL Server] document](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL Microsoft SQL Server] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Microsoft SQL Server]:

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
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL Microsoft SQL Server] account. De sectie lezen op [het verzamelen vereiste geloofsbrieven](#gather-required-credentials) voor meer informatie . |
| `connectionSpec.id` | De [!DNL Microsoft SQL Server] Verbindingsspecificatie-id is: `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**Antwoord**

Een succesvol antwoord retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw database te verkennen in de volgende zelfstudie.

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Microsoft SQL Server] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/database-nosql.md)