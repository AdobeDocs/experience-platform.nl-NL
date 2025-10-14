---
title: Oracle DB verbinden met Experience Platform met behulp van de Flow Service API
description: Leer hoe u Oracle DB met API's kunt verbinden met Experience Platform.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Oracle DB] API[!DNL Flow Service]

Lees deze gids om te leren hoe te om uw [!DNL Oracle DB] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Oracle] via de [!DNL Flow Service] API.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

### Vereiste referenties verzamelen

Lees het [[!DNL Oracle DB]  overzicht &#x200B;](../../../../connectors/databases/oracle.md#prerequisites) voor informatie over authentificatie.

## Verbind [!DNL Oracle DB] met Experience Platform op Azure {#azure}

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL Oracle DB] -account kunt verbinden met Experience Platform on Azure.

### Een basisverbinding maken voor [!DNL Oracle DB] op Experience Platform in Azure {#azure-base}

Een basisverbinding koppelt uw bron aan Experience Platform, die authentificatiedetails, verbindingsstatus, en een unieke identiteitskaart opslaat. Met deze id kunt u door bronbestanden bladeren en specifieke items identificeren die u wilt invoeren, inclusief de gegevenstypen en indelingen.

**API formaat**

```https
POST /connections
```

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de verificatiegegevens van [!DNL Oracle DB] op als onderdeel van de aanvraagparameters.

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Oracle DB] gemaakt via verificatie van verbindingstekenreeksen.

+++verzoek weergeven


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks waarmee verbinding wordt gemaakt met [!DNL Oracle DB] . Het patroon van de [!DNL Oracle DB] verbindingstekenreeks is: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}` . |
| `connectionSpec.id` | The [!DNL Oracle] connection specification ID: `d6b52d86-f0f8-475f-89d4-ce54c8527328` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++reactie weergeven

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Verbinden [!DNL Oracle DB] met Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../../../landing/multi-cloud.md).

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL Oracle DB] -account kunt verbinden met Experience Platform op AWS.

### Een basisverbinding maken voor [!DNL Oracle DB] op Experience Platform op AWS {#aws-base}

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Oracle DB] gemaakt om verbinding te maken met Experience Platform op AWS.

+++verzoek weergeven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.server` | Het IP-adres of de hostnaam van de [!DNL Oracle DB] -server. |
| `auth.params.port` | Het poortnummer van de [!DNL Oracle DB] -server. |
| `auth.params.database` | De naam van de instantie [!DNL Oracle DB] waarmee u verbinding maakt. |
| `auth.params.username` | De gebruikersaccount die aan uw [!DNL Oracle DB] -instantie is gekoppeld. |
| `auth.prams.password` | Het wachtwoord dat overeenkomt met uw [!DNL Oracle DB] -gebruikersaccount. |
| `auth.params.schema` | Het schema dat uw databaseobjecten bevat. |
| `auth.params.sslMode` | Een booleaanse waarde die aangeeft of SSL-maatregelen worden afgedwongen of niet. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met de bron [!DNL Oracle DB] . Deze ID-waarde is vast als: `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) en het overeenkomstige terug. U kunt identiteitskaart gebruiken om [&#x200B; bronverbinding &#x200B;](../../collect/database-nosql.md#create-a-source-connection) tot stand te brengen en `etag` om [&#x200B; uw rekening &#x200B;](../../update.md) bij te werken.

+++reactie weergeven

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Een gegevensstroom maken voor [!DNL Oracle DB] -gegevens

Nu u met succes uw [!DNL Oracle DB] rekening hebt verbonden, kunt u [&#x200B; nu tot een dataflow leiden en gegevens van uw gegevensbestand in Experience Platform &#x200B;](../../collect/database-nosql.md) opnemen.