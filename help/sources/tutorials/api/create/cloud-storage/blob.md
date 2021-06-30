---
keywords: Experience Platform;home;populaire onderwerpen;Azure;azure blob;blob;Blob
solution: Experience Platform
title: Een Azure Blob Base Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met Azure Blob met behulp van de Flow Service API.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# Een [!DNL Azure Blob] basisverbinding maken met de [!DNL Flow Service]-API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL Azure Blob] (verder genoemd als &quot;[!DNL Blob]&quot;) tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een [!DNL Blob]-bronverbinding met de [!DNL Flow Service]-API te kunnen maken.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met uw [!DNL Blob]-opslag, moet u waarden opgeven voor de volgende eigenschap connection:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | Een tekenreeks die de machtigingsgegevens bevat die nodig zijn om [!DNL Blob] te verifiëren bij Experience Platform. Het patroon van de [!DNL Blob] verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Voor meer informatie over verbindingskoorden, zie dit [!DNL Blob] document op [vormend verbindingskoorden](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw [!DNL Blob]-account aan te sluiten. Het [!DNL Blob] SAS URI-patroon is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Voor meer informatie, zie dit [!DNL Blob] document op [gedeelde toegangshandtekening URIs](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Blob] is: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Blob] authentificatiegeloofsbrieven als deel van de verzoekparameters.

### Creeer een [!DNL Blob] basisverbinding gebruikend op koord-gebaseerde authentificatie van de verbinding

Als u een [!DNL Blob] basisverbinding wilt maken met behulp van verificatie op basis van een verbindingstekenreeks, dient u een verzoek van de POST in bij de [!DNL Flow Service]-API terwijl u [!DNL Blob] `connectionString` opgeeft.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met het volgende verzoek wordt een basisverbinding voor [!DNL Blob] gemaakt met verificatie op basis van een verbindingstekenreeks:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die is vereist voor toegang tot gegevens in de blob-opslag. Het patroon van de Blob-verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | De Klob-specificatie voor de opslagverbinding is: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Een [!DNL Blob] basisverbinding maken met URI voor gedeelde toegangshandtekening

Een gedeelde toegangshandtekening (SAS) URI staat veilige gedelegeerde autorisatie toe aan uw [!DNL Blob]-account. Met SAS kunt u verificatiereferenties maken met verschillende toegangsgraden, aangezien een SAS-gebaseerde verificatie u in staat stelt machtigingen, begin- en vervaldatums en bepalingen voor specifieke bronnen in te stellen.

Als u een [!DNL Blob] blob-verbinding wilt maken met de URI van een handtekening voor gedeelde toegang, dient u een POST-aanvraag in bij de [!DNL Flow Service] API en geeft u waarden op voor uw [!DNL Blob] `sasUri`.

**API-indeling**

```http
POST /connections
```

**Verzoek**

Met het volgende verzoek wordt een basisverbinding voor [!DNL Blob] gemaakt met URI voor gedeelde toegangshandtekening:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De SAS-URI die vereist is voor toegang tot gegevens in uw [!DNL Blob]-opslag. Het [!DNL Blob] SAS URI-patroon is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | De [!DNL Blob]-specificatie-id voor opslagverbinding is: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Antwoord**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Blob] verbinding gebruikend APIs gecreeerd en een unieke identiteitskaart werd verkregen als deel van het reactievermogen. Met deze verbindings-id kunt u [cloudopslag verkennen met de Flow Service API](../../explore/cloud-storage.md) of [Inst Parquet-gegevens met behulp van de Flow Service API](../../cloud-storage-parquet.md).
