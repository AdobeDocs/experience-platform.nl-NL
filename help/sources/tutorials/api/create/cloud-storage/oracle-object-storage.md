---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Creeer een Verbinding van de Basis van de Opslag van de Objecten van het Oracle gebruikend de Dienst API van de Stroom
type: Tutorial
description: Leer hoe u Adobe Experience Platform met de Flow Service API kunt verbinden met Oracle Object Storage.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Een [!DNL Oracle Object Storage] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Oracle Object Storage] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Oracle Object Storage] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Oracle Object Storage] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUrl` | Het [!DNL Oracle Object Storage] eindpunt dat voor authentificatie wordt vereist. De eindpuntnotatie is: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | De toegangssleutel-id van [!DNL Oracle Object Storage] die is vereist voor verificatie. |
| `secretKey` | Het [!DNL Oracle Object Storage] -wachtwoord dat is vereist voor verificatie. |
| `bucketName` | De toegestane emmernaam wordt vereist als de gebruiker toegang beperkt heeft. De naam van het emmertje moet tussen drie en 63 lange karakters zijn, moet beginnen en met of een brief of een aantal beëindigen, en kan kleine letters, aantallen, of koppeltekens slechts bevatten (`-`). De emmernaam kan niet als IP adres worden geformatteerd. |
| `folderPath` | Het toegestane mappad dat is vereist als de gebruiker de toegang heeft beperkt. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Oracle Object Storage] is: `c85f9425-fb21-426c-ad0b-405e9bd8a46c` . |

Voor meer informatie over hoe te om deze waarden te verkrijgen, verwijs naar de [ de authentificatiegids van de Opslag van de Objecten van het Oracle ](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Oracle Object Storage] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Oracle Object Storage] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.serviceUrl` | Het [!DNL Oracle Object Storage] eindpunt dat voor authentificatie wordt vereist. |
| `auth.params.accessKey` | De toegangssleutel-id van [!DNL Oracle Object Storage] die is vereist voor verificatie. |
| `auth.params.secretKey` | Het [!DNL Oracle Object Storage] -wachtwoord dat is vereist voor verificatie. |
| `auth.params.bucketName` | De toegestane emmernaam wordt vereist als de gebruiker toegang beperkt heeft. |
| `auth.params.folderPath` | Het toegestane mappad dat is vereist als de gebruiker de toegang heeft beperkt. |
| `connectionSpec.id` | De [!DNL Oracle Object Storage] connection spec ID: `c85f9425-fb21-426c-ad0b-405e9bd8a46c` . |

**Reactie**

Een geslaagde reactie retourneert de verbinding-id van de nieuwe verbinding. Deze id is vereist voor het verkennen van uw gegevens voor cloudopslag in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Oracle Object Storage] -verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke verbindings-id ervan opgehaald. U kunt deze verbindingsidentiteitskaart gebruiken om [ wolkenopslag te onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
