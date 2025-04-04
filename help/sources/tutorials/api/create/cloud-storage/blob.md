---
title: Een Azure Blob Base Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Azure Blob met behulp van de Flow Service API.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Een [!DNL Azure Blob] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma verstrekt stappen om een basisverbinding voor [!DNL Azure Blob] tot stand te brengen (verder die als &quot; [!DNL Blob] wordt bedoeld&quot;) gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een [!DNL Blob] -bronverbinding met de [!DNL Flow Service] API te kunnen maken.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met uw [!DNL Blob] -opslag als u waarden opgeeft voor de volgende eigenschap connection:

>[!BEGINTABS]

>[!TAB  het koordauthentificatie van de Verbinding ]

| Credentials | Beschrijving |
| --- | --- |
| `connectionString` | Een tekenreeks die de machtigingsgegevens bevat die nodig zijn voor verificatie van [!DNL Blob] naar Experience Platform. Het patroon van de [!DNL Blob] verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}` . Voor meer informatie over verbindingskoorden, zie dit [!DNL Blob] document op [ vormend verbindingskoorden ](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Blob] is: `d771e9c1-4f26-40dc-8617-ce58c4b53702` . |

>[!TAB  de authentificatie van SAS URI ]

| Credentials | Beschrijving |
| --- | --- |
| `sasUri` | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw [!DNL Blob] -account te verbinden. Het [!DNL Blob] patroon van SAS URI is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` voor meer informatie, zie dit [!DNL Blob] document op [ gedeelde toegangshandtekening URIs ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | De naam van de container die u toegang tot wilt aanwijzen. Wanneer u een nieuw account maakt met de [!DNL Blob] -bron, kunt u een containernaam opgeven om gebruikerstoegang tot de submap van uw keuze op te geven. |
| `folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Blob] is: `d771e9c1-4f26-40dc-8617-ce58c4b53702` . |

>[!ENDTABS]

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL Blob] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

De [!DNL Blob] -bron ondersteunt verificatie met zowel een verbindingstekenreeks als een gedeelde toegangshandtekening (SAS). Een gedeelde toegangshandtekening (SAS) URI maakt beveiligde gedelegeerde autorisatie voor uw [!DNL Blob] -account mogelijk. Met SAS kunt u verificatiereferenties maken met verschillende toegangsgraden, aangezien een SAS-gebaseerde verificatie u in staat stelt machtigingen, begin- en vervaldatums en bepalingen voor specifieke bronnen in te stellen.

Tijdens deze stap kunt u ook de submappen aangeven waartoe uw account toegang heeft door de naam van de container en het pad naar de submap te definiëren.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Blob] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

>[!BEGINTABS]

>[!TAB  Koord van de Verbinding ]

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Blob] gemaakt met verificatie op basis van een verbindingstekenreeks:

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
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

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die is vereist voor toegang tot gegevens in de blob-opslag. Het patroon van de Blob-verbindingstekenreeks is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}` . |
| `connectionSpec.id` | De Klob-specificatie voor de verbinding is: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB  de Authentificatie van SAS URI ]

Als u een [!DNL Blob] -verbinding wilt maken met de URI van een handtekening voor gedeelde toegang, dient u een POST-aanvraag in bij de [!DNL Flow Service] API en geeft u waarden op voor uw [!DNL Blob] `sasUri` -handtekening.

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
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

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De SAS-URI die vereist is voor toegang tot gegevens in uw [!DNL Blob] -opslag. Het [!DNL Blob] SAS URI-patroon is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` . |
| `connectionSpec.id` | De specificatie-id voor de [!DNL Blob] opslagverbinding is: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Blob] -verbinding gemaakt met behulp van API&#39;s en is een unieke id verkregen als onderdeel van de hoofdtekst van de reactie. U kunt deze verbindingsidentiteitskaart gebruiken om [ wolkenopslag te onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
