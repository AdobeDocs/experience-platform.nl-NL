---
keywords: Experience Platform;thuis;populaire onderwerpen;Apache-bijenkorf;hive;Hive
solution: Experience Platform
title: Een Apache Hive maken op Azure HDInsights Base Connection met behulp van de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Apache Hive op Azure HDInsights kunt aansluiten op Adobe Experience Platform met behulp van de Flow Service API.
exl-id: e1469a29-6f61-47ba-995e-39f06ee4a4a4
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# Een [!DNL Apache Hive] op [!DNL Azure HDInsights] basisverbinding met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Apache Hive] op [!DNL Azure HDInsights] -connector bevindt zich in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Apache Hive] op [!DNL Azure HDInsights] (hierna &quot;[!DNL Hive]&quot;) het gebruik van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Hive] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Hive]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Hive] server. |
| `username` | De gebruikersnaam die u gebruikt om toegang te krijgen tot [!DNL Hive] server. |
| `password` | Het wachtwoord dat overeenkomt met de gebruiker. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Hive] is: `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

Zie voor meer informatie over het aan de slag gaan [dit Hive-document](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Hive] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Hive]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL Hive] account. |
| `connectionSpec.id` | De [!DNL Hive] Verbindingsspecificatie-id: `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`. |

**Antwoord**

Een succesvol antwoord retourneert details van de zojuist gemaakte verbinding, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Apache Hive] op [!DNL Azure HDInsights] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het Platform te brengen met de [!DNL Flow Service] API](../../collect/database-nosql.md)
