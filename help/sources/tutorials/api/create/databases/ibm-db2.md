---
keywords: Experience Platform;home;populaire onderwerpen;IBM  [!DNL IBM DB2];IBM;ibm  [!DNL IBM DB2];[!DNL IBM DB2];[!DNL IBM DB2]
solution: Experience Platform
title: Creeer een Verbinding van de Basis van IBM  [!DNL IBM DB2]  Gebruikend de Dienst API van de Stroom
type: Tutorial
description: Leer hoe te om IBM  [!DNL IBM DB2]  met Adobe Experience Platform te verbinden gebruikend de Dienst API van de Stroom.
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Een IBM [!DNL IBM DB2] -basisverbinding maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De IBM [!DNL IBM DB2] -connector bevindt zich in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL IBM DB2] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL IBM DB2] via de [!DNL Flow Service] API.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `server` | De naam van de [!DNL IBM DB2] -server. U kunt het poortnummer opgeven na de servernaam die is gescheiden door een dubbele punt. Bijvoorbeeld: server:poort. |
| `database` | De naam van de [!DNL IBM DB2] -database. |
| `username` | De gebruikersnaam die wordt gebruikt om verbinding te maken met de [!DNL IBM DB2] -database. |
| `password` | Het wachtwoord voor de gebruikersaccount die u voor de gebruikersnaam hebt opgegeven. |
| `connectionSpec.id` | De unieke id die nodig is om een verbinding te maken. De verbindingsspecificatie-id voor [!DNL IBM DB2] is `09182899-b429-40c9-a15a-bf3ddbc8ced7` . |

Voor meer informatie over begonnen worden verwijs naar [ dit  [!DNL IBM DB2]  document ](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL IBM DB2] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL IBM DB2] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die aan uw [!DNL IBM DB2] account is gekoppeld. |
| `connectionSpec.id` | The [!DNL IBM DB2] connection specification ID: `09182899-b429-40c9-a15a-bf3ddbc8ced7` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL IBM DB2] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)

