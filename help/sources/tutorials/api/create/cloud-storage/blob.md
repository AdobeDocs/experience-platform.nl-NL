---
title: Connect Azure Blob Storage naar Experience Platform met behulp van de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Azure Blob met behulp van de Flow Service API.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Verbind [!DNL Azure Blob Storage] met Experience Platform gebruikend API

Lees deze gids om te leren hoe te om uw [!DNL Azure Blobg Storage] rekening met Adobe Experience Platform te verbinden gebruikend [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

### Vereiste referenties verzamelen

Lees het [[!DNL Azure Blob Storage]  overzicht ](../../../../connectors/cloud-storage/blob.md#authentication) voor informatie over authentificatie.

## Sluit uw [!DNL Azure Blob Storage] -account aan op Experience Platform {#connect}

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL Azure Blob Storage] -account kunt verbinden met Experience Platform.

### Een basisverbinding maken

>[!NOTE]
>
>Nadat u een [!DNL Azure Blob Storage] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Een basisverbinding koppelt uw bron aan Experience Platform, die authentificatiedetails, verbindingsstatus, en een unieke identiteitskaart opslaat. Met deze id kunt u door bronbestanden bladeren en specifieke items identificeren die u wilt invoeren, inclusief de gegevenstypen en indelingen.

U kunt uw [!DNL Azure Blob Storage] -account verbinden met Experience Platform door de volgende verificatietypen te gebruiken:

* **de belangrijkste authentificatie van de Rekening**: Gebruikt de toegangssleutel van de opslagrekening om met uw [!DNL Azure Blob Storage] rekening voor authentiek te verklaren en te verbinden.
* **Gedeelde toegangshandtekening (SAS)**: Gebruikt een SAS URI om gedelegeerde, tijd-beperkte toegang tot middelen in uw [!DNL Azure Blob Storage] rekening te verlenen.
* **de hoofd gebaseerde authentificatie van de Dienst**: Gebruikt een Azure Actieve de dienstprincipal van de Folder (AAD) (cliënt identiteitskaart en geheim) om aan uw rekening van de Opslag van Azure Blob veilig voor authentiek te verklaren.

**API formaat**

```https
POST /connections
```

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een POST- verzoek aan het `/connections` eindpunt en verstrek uw authentificatiegeloofsbrieven als deel van de verzoekparameters.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Geef waarden op voor uw `connectionString` , `container` en `folderPath` om verificatie met de accountsleutel te gebruiken.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `connectionString` | De verbindingstekenreeks voor uw [!DNL Azure Blob Storage] -account. Het patroon van de verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` . |
| `container` | De naam van de [!DNL Azure Blob Storage] -container waarin uw gegevensbestanden zijn opgeslagen. |
| `folderPath` | Het pad binnen de opgegeven container waarin de bestanden zich bevinden. |
| `connectionSpec.id` | De verbindingsspecificatie-id van de [!DNL Azure Blob Storage] -bron. Deze id is vast als: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB  Gedeelde toegangshandtekening ]

Als u een handtekening voor gedeelde toegang wilt gebruiken, geeft u waarden op voor de tekens `sasUri`, `container` en `folderPath` .

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `sasUri` | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw account te verbinden. Het patroon van SAS URI is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | De naam van de [!DNL Azure Blob Storage] -container waarin uw gegevensbestanden zijn opgeslagen. |
| `folderPath` | Het pad binnen de opgegeven container waarin de bestanden zich bevinden. |
| `connectionSpec.id` | De verbindingsspecificatie-id van de [!DNL Azure Blob Storage] -bron. Deze id is vast als: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB  de dienst belangrijkste gebaseerde authentificatie ]

Als u verbinding wilt maken via verificatie op basis van serviceprincipal, geeft u waarden op voor uw: `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` en `folderPath` .

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `serviceEndpoint` | Het eindpunt-URL van uw [!DNL Azure Blob Storage] -account. Doorgaans in de notatie: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `servicePrincipalId` | De client/toepassings-id van de Azure Active Directory (AAD) service principal die voor verificatie wordt gebruikt. |
| `servicePrincipalKey` | Het clientgeheim of wachtwoord dat aan de Azure service principal is gekoppeld. |
| `accountKind` | Het type van uw [!DNL Azure Blob Storage] account. Veelvoorkomende waarden zijn `StorageV2` , `BlobStorage` of `Storage` . |
| `tenant` | De Azure Active Directory (AAD) huurder-id waar de serviceprincipal is geregistreerd. |
| `container` | De naam van de [!DNL Azure Blob Storage] -container waarin uw gegevensbestanden zijn opgeslagen. |
| `folderPath` | Het pad binnen de opgegeven container waarin de bestanden zich bevinden. |
| `connectionSpec.id` | De verbindingsspecificatie-id van de [!DNL Azure Blob Storage] -bron. Deze id is vast als: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!ENDTABS]

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Blob] -verbinding gemaakt met behulp van API&#39;s en is een unieke id verkregen als onderdeel van de hoofdtekst van de reactie. U kunt deze verbindingsidentiteitskaart gebruiken om [ wolkenopslag te onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
