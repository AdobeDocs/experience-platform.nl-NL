---
keywords: Experience Platform;home;populaire onderwerpen;MySQL;mysql
solution: Experience Platform
title: Een [!DNL MySQL] Basisverbinding met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform met MySQL kunt verbinden met behulp van de Flow Service API.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Een [!DNL MySQL] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL MySQL] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL MySQL] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om verbinding te maken met uw [!DNL MySQL] opslag, moet u de waarde voor het volgende verbindingsbezit verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De [!DNL MySQL] verbindingstekenreeks die aan uw account is gekoppeld. De [!DNL MySQL] patroon verbindingstekenreeks is: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL MySQL] is `26d738e0-8963-47ea-aadf-c60de735468a`. |

Raadpleeg deze voor meer informatie over het verkrijgen van een verbindingstekenreeks [[!DNL MySQL] document](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL MySQL] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL MySQL]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL MySQL] Test Connection",
        "description": "[!DNL MySQL] Test Connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "26d738e0-8963-47ea-aadf-c60de735468a",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De [!DNL MySQL] verbindingstekenreeks die aan uw account is gekoppeld. De [!DNL MySQL] patroon verbindingstekenreeks is: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | De [!DNL MySQL] Verbindingsspecificatie-id: `26d738e0-8963-47ea-aadf-c60de735468a`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist om uw database te verkennen in de volgende zelfstudie.

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL MySQL]basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het Platform te brengen met de [!DNL Flow Service] API](../../collect/database-nosql.md)

