---
keywords: Experience Platform;home;populaire onderwerpen;[!DNL Azure Table Storage];[!DNL Azure Table Storage];Azure lijstopslag
solution: Experience Platform
title: Een Azure Table Storage Base Connection maken met de Flow Service API
type: Tutorial
description: Leer hoe u Azure Table Storage met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
exl-id: 8ebd5d77-ed1f-47e1-8212-efb6c5e84ec1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Een [!DNL Azure Table Storage] basisverbinding maken met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Azure Table Storage] -connector bevindt zich in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Azure Table Storage] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Azure Table Storage] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Azure Table Storage] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met een instantie [!DNL Azure Table Storage] . Het patroon van de verbindingstekenreeks voor [!DNL Azure Table Storage] is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Azure Table Storage] is `ecde33f2-c56f-46cc-bdea-ad151c16cd69` . |

Voor meer informatie over het verkrijgen van een verbindingskoord, verwijs naar [ dit  [!DNL Azure Table Storage]  document ](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Azure Table Storage] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Azure Table Storage] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met een instantie [!DNL Azure Table Storage] . Het patroon van de verbindingstekenreeks voor [!DNL Azure Table Storage] is: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}` . |
| `connectionSpec.id` | The [!DNL Azure Table Storage] connection specification ID: `ecde33f2-c56f-46cc-bdea-ad151c16cd69` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Azure Table Storage] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
