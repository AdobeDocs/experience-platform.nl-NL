---
keywords: Experience Platform;thuis;populaire onderwerpen;servicenow;ServiceNow
solution: Experience Platform
title: Creeer een Verbinding van de Basis ServiceNow gebruikend de Dienst API van de Stroom
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met een ServiceNow-server met behulp van de Flow Service API.
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: ff0f6bc6b8a57b678b329fe2b47c53919e0e2d64
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Een [!DNL ServiceNow] basisverbinding maken met de [!DNL Flow Service]-API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL Google ServiceNow] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met een [!DNL ServiceNow]-server met de [!DNL Flow Service]-API tot stand te kunnen brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL ServiceNow], moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `endpoint` | Het eindpunt van de [!DNL ServiceNow]-server. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de [!DNL ServiceNow]-server voor verificatie. |
| `password` | Het wachtwoord om verbinding te maken met de [!DNL ServiceNow]-server voor verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL ServiceNow] is: `eb13cb25-47ab-407f-ba89-c0125281c563`. |

Raadpleeg [dit document ServiceNow](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET) voor meer informatie over aan de slag gaan.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL ServiceNow] authentificatiegeloofsbrieven als deel van de verzoekparameters.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL ServiceNow]:

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.server` | Het eindpunt van uw [!DNL ServiceNow]-server. |
| `auth.params.username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de [!DNL ServiceNow]-server voor verificatie. |
| `auth.params.password` | Het wachtwoord om verbinding te maken met de [!DNL ServiceNow]-server voor verificatie. |
| `connectionSpec.id` | De [!DNL ServiceNow] ID van de verbindingsspecificatie: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**Antwoord**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen hebt u een [!DNL ServiceNow]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsID in de volgende zelfstudie gebruiken aangezien u leert hoe te om [systemen van het klantensucces te onderzoeken gebruikend de Dienst API van de Stroom](../../explore/customer-success.md).
