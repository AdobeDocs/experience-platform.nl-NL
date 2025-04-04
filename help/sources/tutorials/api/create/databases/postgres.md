---
keywords: Experience Platform;home;populaire onderwerpen;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Een PostSQL-basisverbinding maken met de Flow Service API
type: Tutorial
description: Leer hoe u Adobe Experience Platform met de Flow Service API verbindt met PostgreSQL.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Een [!DNL PostgreSQL] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL PostgreSQL] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL PostgreSQL] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL PostgreSQL] als u de volgende eigenschap voor verbinding opgeeft:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL PostgreSQL] account is gekoppeld. Het patroon van de [!DNL PostgreSQL] verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL PostgreSQL] is `74a1c565-4e59-48d7-9d67-7c03b8a13137` . |

Voor meer informatie over het verkrijgen van een verbindingskoord, verwijs naar dit [[!DNL PostgreSQL]  document ](https://www.postgresql.org/docs/9.2/app-psql.html).

#### SSL-versleuteling inschakelen voor uw verbindingstekenreeks

U kunt SSL-codering inschakelen voor de [!DNL PostgreSQL] -verbindingstekenreeks door uw verbindingstekenreeks toe te voegen met de volgende eigenschappen:

| Eigenschap | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `EncryptionMethod` | Hiermee kunt u SSL-codering inschakelen voor uw [!DNL PostgreSQL] -gegevens. | <uL><li>`EncryptionMethod=0` (Uitgeschakeld)</li><li>`EncryptionMethod=1` (Ingeschakeld)</li><li>`EncryptionMethod=6` (RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Hiermee wordt het certificaat gevalideerd dat door de [!DNL PostgreSQL] -database wordt verzonden wanneer `EncryptionMethod` wordt toegepast. | <uL><li>`ValidationServerCertificate=0` (Uitgeschakeld)</li><li>`ValidationServerCertificate=1` (Ingeschakeld)</li></ul> |

Hier volgt een voorbeeld van een [!DNL PostgreSQL] verbindingstekenreeks die is toegevoegd met SSL-codering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1` .

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL PostgreSQL] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL PostgreSQL] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| ------------- | --------------- |
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL PostgreSQL] account is gekoppeld. Het patroon van de [!DNL PostgreSQL] verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}` . |
| `connectionSpec.id` | De [!DNL PostgreSQL] verbindingsspecificatie-id&#39;s: `74a1c565-4e59-48d7-9d67-7c03b8a13137` . |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde basisverbinding terug. Deze id is vereist om uw [!DNL PostgreSQL] -database in de volgende zelfstudie te verkennen.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL PostgreSQL] verbinding met het verbindingsbestand gemaakt met de API van [!DNL Flow Service] . U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
