---
keywords: Experience Platform;home;populaire onderwerpen;redshift;Opnieuw verschuiven;Amazon Opnieuw verschuiven;amazon opnieuw verschuiven
solution: Experience Platform
title: Een Amazon Redshift Base-verbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met Amazon Redshift met behulp van de Flow Service API.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: c0d750ef61ad2e295568cccabca5c52a758997c2
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Een [!DNL Amazon Redshift] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Amazon Redshift] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Amazon Redshift] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Amazon Redshift]moet u de volgende eigenschappen voor de verbinding opgeven:

| **Credentials** | **Beschrijving** |
| -------------- | --------------- |
| `server` | De server die aan uw [!DNL Amazon Redshift] account. |
| `username` | De gebruikersnaam die aan uw [!DNL Amazon Redshift] account. |
| `password` | Het wachtwoord dat aan uw [!DNL Amazon Redshift] account. |
| `database` | De [!DNL Amazon Redshift] database die u opent. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Amazon Redshift] is `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Raadpleeg voor meer informatie over aan de slag gaan [[!DNL Amazon Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!NOTE]
>
>De standaard coderingsstandaard voor [!DNL Redshift] is Unicode. Dit kan niet worden gewijzigd.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Amazon Redshift] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Amazon Redshift]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| ------------- | --------------- |
| `auth.params.server` | Uw [!DNL Amazon Redshift] server. |
| `auth.params.database` | De database die aan uw [!DNL Amazon Redshift] account. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Amazon Redshift] account. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Amazon Redshift] account. |
| `connectionSpec.id` | De [!DNL Amazon Redshift] Verbindingsspecificatie-id: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Amazon Redshift] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om databasegegevens naar het Platform te brengen met de [!DNL Flow Service] API](../../collect/database-nosql.md)
