---
keywords: Experience Platform;home;populaire onderwerpen;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Een PostSQL-basisverbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform met de Flow Service API verbindt met PostgreSQL.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# Een [!DNL PostgreSQL] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL PostgreSQL] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL PostgreSQL] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL PostgreSQL]moet u de volgende eigenschap voor de verbinding opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die aan uw [!DNL PostgreSQL] account. De [!DNL PostgreSQL] patroon verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL PostgreSQL] is `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Raadpleeg deze voor meer informatie over het verkrijgen van een verbindingstekenreeks [[!DNL PostgreSQL] document](https://www.postgresql.org/docs/9.2/app-psql.html).

#### SSL-versleuteling inschakelen voor uw verbindingstekenreeks

U kunt SSL-codering inschakelen voor uw [!DNL PostgreSQL] verbindingstekenreeks door uw verbindingstekenreeks toe te voegen met de volgende eigenschappen:

| Eigenschap | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `EncryptionMethod` | Hiermee kunt u SSL-codering inschakelen op uw [!DNL PostgreSQL] gegevens. | <uL><li>`EncryptionMethod=0`(Uitgeschakeld)</li><li>`EncryptionMethod=1`(Ingeschakeld)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valideert het certificaat dat door uw [!DNL PostgreSQL] database wanneer `EncryptionMethod` wordt toegepast. | <uL><li>`ValidationServerCertificate=0`(Uitgeschakeld)</li><li>`ValidationServerCertificate=1`(Ingeschakeld)</li></ul> |

Hier volgt een voorbeeld van een [!DNL PostgreSQL] verbindingstekenreeks toegevoegd met SSL-codering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL PostgreSQL] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL PostgreSQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL PostgreSQL] account. De [!DNL PostgreSQL] patroon verbindingstekenreeks is: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | De [!DNL PostgreSQL] Verbindingsspecificatie-id&#39;s: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe basisverbinding. Deze id is vereist om uw [!DNL PostgreSQL] in de volgende zelfstudie.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL PostgreSQL] verbinding als verbindingsbasis gebruiken [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het Platform te brengen met de [!DNL Flow Service] API](../../collect/database-nosql.md)
