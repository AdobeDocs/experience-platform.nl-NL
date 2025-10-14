---
title: Een Google Cloud Storage Base Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform kunt verbinden met een Google Cloud Storage-account met behulp van de Flow Service API.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Een [!DNL Google Cloud Storage] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Google Cloud Storage] tot stand te brengen gebruikend [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met een Google Cloud Storage-account met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met uw [!DNL Google Cloud Storage] -account als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `accessKeyId` | Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform. |
| `secretAccessKey` | Een tekenreeks van 40 tekens met een basiscodering van 64 tekens die wordt gebruikt om uw [!DNL Google Cloud Storage] -account te verifiëren bij Experience Platform. |
| `bucketName` | De naam van uw [!DNL Google Cloud Storage] emmertje. U moet een emmernaam specificeren als u toegang tot een specifieke subomslag in uw wolkenopslag wilt verlenen. |
| `folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. |

Voor meer informatie over deze waarden, zie de [&#x200B; de sleutels van HMAC van de Opslag van de Wolk van Google HMAC &#x200B;](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) gids. Voor stappen op hoe te om uw eigen toegangs zeer belangrijke identiteitskaart en geheime toegangssleutel te produceren, verwijs naar het [[!DNL Google Cloud Storage]  overzicht &#x200B;](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Google Cloud Storage] -verificatiegegevens op als onderdeel van de aanvraagparameters.

>[!TIP]
>
>Tijdens deze stap kunt u ook de submappen aangeven waartoe uw account toegang heeft door de naam van de emmertje en het pad naar de submap te definiëren.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Google Cloud Storage] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
          }
      },
      "connectionSpec": {
          "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.accessKeyId` | De toegangs sleutel-id die aan uw [!DNL Google Cloud Storage] account is gekoppeld. |
| `auth.params.secretAccessKey` | De geheime toegangstoets die aan uw [!DNL Google Cloud Storage] account is gekoppeld. |
| `auth.params.bucketName` | De naam van uw [!DNL Google Cloud Storage] emmertje. U moet een emmernaam specificeren als u toegang tot specifieke subfolder in uw wolkenopslag wilt verlenen. |
| `auth.params.folderPath` | Het pad naar de map waartoe u toegang wilt verlenen. |
| `connectionSpec.id` | De [!DNL Google Cloud Storage] connection specification ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist voor het verkennen van uw gegevens voor cloudopslag in de volgende zelfstudie.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u een [!DNL Google Cloud Storage] -verbinding gemaakt met behulp van API&#39;s en is een unieke id verkregen als onderdeel van de hoofdtekst van de reactie. U kunt deze verbindingsidentiteitskaart gebruiken om [&#x200B; wolkenopslag te onderzoeken gebruikend de Dienst API van de Stroom &#x200B;](../../explore/cloud-storage.md).
