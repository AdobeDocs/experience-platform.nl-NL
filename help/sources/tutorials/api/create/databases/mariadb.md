---
title: Verbinding maken met MariaDB naar Experience Platform met behulp van de Flow Service API
description: Leer hoe u uw MariaDB-account met Experience Platform kunt verbinden via API's.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: d5d47f9ca3c01424660fe33f8310586a70a32875
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL MariaDB]

Lees deze gids om te leren hoe te om uw [!DNL MariaDB] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL MariaDB] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Lees het [[!DNL MariaDB]  overzicht ](../../../../connectors/databases/mariadb.md#prerequisites) voor informatie over authentificatie.

### Experience Platform API&#39;s gebruiken

Lees de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md) voor informatie over hoe te met succes vraag aan Experience Platform APIs maken.

## Verbind [!DNL MariaDB] met Experience Platform op Azure {#azure}

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL MariaDB] -account kunt verbinden met Experience Platform on Azure.

### Een basisverbinding maken voor [!DNL MariaDB] op Experience Platform in Azure {#azure-base}

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

**API formaat**

```https
POST /connections
```

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de juiste verificatiegegevens voor uw [!DNL MariaDB] -account op.

>[!BEGINTABS]

>[!TAB  Reeks gebaseerde authentificatie van de Verbinding ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor een [!DNL MariaDB] -bron gemaakt met verificatie op basis van een verbindingstekenreeks.

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
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL MariaDB] -verificatie is gekoppeld. Het patroon van de [!DNL MariaDB] verbindingstekenreeks is: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` . |
| `connectionSpec.id` | De [!DNL MariaDB] -id van de verbindingsspecificatie is: `3000eb99-cd47-43f3-827c-43caf170f015` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB  Basisauthentificatie ]

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor een [!DNL MariaDB] -bron gemaakt met behulp van basisverificatie.

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
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.server` | De naam of IP van uw [!DNL MariaDB] database. |
| `auth.params.database` | De naam van uw database. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw database. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw database. |
| `auth.params.sslMode` | De methode waarmee gegevens tijdens gegevensoverdracht worden gecodeerd. |
| `connectionSpec.id` | De [!DNL MariaDB] -id van de verbindingsspecificatie is: `3000eb99-cd47-43f3-827c-43caf170f015` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

>[!ENDTABS]

## Verbinden [!DNL MariaDB] met Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../../landing/multi-cloud.md).

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL MariaDB] -account kunt verbinden met Experience Platform op AWS.

### Een basisverbinding maken voor [!DNL MariaDB] op Experience Platform op AWS {#aws-base}

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL MariaDB] gemaakt om verbinding te maken met Experience Platform op AWS.

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
      "name": "MariaDB on Experience Platform AWS",
      "description": "MariaDB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.server` | De naam of IP van uw [!DNL MariaDB] database. |
| `auth.params.database` | De naam van uw database. |
| `auth.params.username` | De gebruikersnaam die overeenkomt met uw database. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw database. |
| `auth.params.sslMode` | De methode waarmee gegevens tijdens gegevensoverdracht worden gecodeerd. |
| `connectionSpec.id` | De [!DNL MariaDB] -id van de verbindingsspecificatie is: `3000eb99-cd47-43f3-827c-43caf170f015` . |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Respons voorbeeld weergeven

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL MariaDB] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
