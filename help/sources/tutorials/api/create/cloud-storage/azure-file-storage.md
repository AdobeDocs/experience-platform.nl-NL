---
keywords: Experience Platform;home;populaire onderwerpen;Azure;Azure File Storage;Azure-bestandsopslag
solution: Experience Platform
title: Een Azure File Storage Base Connection maken met de Flow Service API
type: Tutorial
description: Leer hoe u Azure File Storage met Adobe Experience Platform kunt verbinden met behulp van de Flow Service API.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Een [!DNL Azure File Storage] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Azure File Storage] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Azure File Storage] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Azure File Storage] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het eindpunt van de [!DNL Azure File Storag] instantie u toegang hebt tot. |
| `userId` | De gebruiker met voldoende toegang tot het [!DNL Azure File Storage] eindpunt. |
| `password` | Het wachtwoord voor uw [!DNL Azure File Storage] -instantie |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Azure File Storage] is: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` . |

Voor meer informatie over begonnen worden verwijs naar [ dit Azure document van de Opslag van het Dossier ](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Azure File Storage] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Azure File Storage] gemaakt:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | Het eindpunt van de instantie [!DNL Azure File Storage] waartoe u toegang hebt. |
| `auth.params.userId` | De gebruiker met voldoende toegang tot het [!DNL Azure File Storage] eindpunt. |
| `auth.params.password` | De toegangssleutel van [!DNL Azure File Storage]. |
| `connectionSpec.id` | The [!DNL Azure File Storage] connection specification ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Azure File Storage] -verbinding gemaakt met de [!DNL Flow Service] API en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze identiteitskaart in het volgende leerprogramma gebruiken aangezien u leert [ een opslag van de derdewolk onderzoeken gebruikend de Dienst API van de Stroom ](../../explore/cloud-storage.md).
