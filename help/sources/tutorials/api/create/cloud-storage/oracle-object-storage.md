---
keywords: Experience Platform;home;populaire onderwerpen;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Een Oracle Object Storage Base-verbinding maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform met de Flow Service API kunt verbinden met Oracle Object Storage.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 1%

---

# Een [!DNL Oracle Object Storage] basisverbinding maken met de [!DNL Flow Service]-API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL Oracle Object Storage] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met [!DNL Oracle Object Storage] met de [!DNL Flow Service]-API tot stand te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL Oracle Object Storage], moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUrl` | Het [!DNL Oracle Object Storage] eindpunt dat voor authentificatie wordt vereist. De eindpuntnotatie is: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | De [!DNL Oracle Object Storage] toegangs zeer belangrijke identiteitskaart die voor authentificatie wordt vereist. |
| `secretKey` | Het [!DNL Oracle Object Storage] wachtwoord vereist voor authentificatie. |
| `bucketName` | De toegestane emmernaam wordt vereist als de gebruiker toegang beperkt heeft. De naam van het emmertje moet tussen drie en 63 lange karakters zijn, moet beginnen en met of een brief of een aantal beëindigen, en kan slechts kleine letters, aantallen, of koppeltekens (`-`) bevatten. De emmernaam kan niet als IP adres worden geformatteerd. |
| `folderPath` | Het toegestane mappad dat is vereist als de gebruiker de toegang heeft beperkt. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Oracle Object Storage] is: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Voor meer informatie over hoe te om deze waarden te verkrijgen, verwijs naar [de authentificatiegids van de Opslag van de Objecten van het Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Oracle Object Storage] authentificatiegeloofsbrieven als deel van de verzoekparameters.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.accessKey` | De [!DNL Oracle Object Storage] toegangs zeer belangrijke identiteitskaart die voor authentificatie wordt vereist. |
| `auth.params.secretKey` | Het [!DNL Oracle Object Storage] wachtwoord vereist voor authentificatie. |
| `auth.params.bucketName` | De toegestane emmernaam wordt vereist als de gebruiker toegang beperkt heeft. |
| `auth.params.folderPath` | Het toegestane mappad dat is vereist als de gebruiker de toegang heeft beperkt. |
| `connectionSpec.id` | De [!DNL Oracle Object Storage]-verbindings-ID: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Antwoord**

Een geslaagde reactie retourneert de verbinding-id van de nieuwe verbinding. Deze id is vereist voor het verkennen van uw gegevens voor cloudopslag in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Oracle Object Storage] verbinding gebruikend [!DNL Flow Service] API gecreeerd, en zijn unieke verbindingsidentiteitskaart verkregen. U kunt deze verbindings-id gebruiken om met de Flow Service API](../../explore/cloud-storage.md) cloudopslag te verkennen.[
