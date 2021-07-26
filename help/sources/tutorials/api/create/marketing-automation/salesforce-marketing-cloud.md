---
keywords: Experience Platform;home;populaire onderwerpen;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Creeer een Verbinding van de Basis van de Marketing Cloud Salesforce gebruikend de Dienst API van de Stroom
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform met de Flow Service API kunt verbinden met Salesforce-Marketing Cloud.
source-git-commit: 56458ed6e74a76e2787ab3b9f1409b11556bdee2
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Een [!DNL Salesforce Marketing Cloud] basisverbinding maken met de [!DNL Flow Service]-API

>[!NOTE]
>
>De bron [!DNL Salesforce Marketing Cloud] is in bèta. Zie [Bronnen overzicht](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bèta-geëtiketteerde bronnen.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL Salesforce Marketing Cloud] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van  [!DNL Platform] services.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

De volgende sectie bevat aanvullende informatie die u moet weten om een verbinding met [!DNL Salesforce Marketing Cloud] met de API [!DNL Flow Service] tot stand te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL Salesforce Marketing Cloud], moet u de volgende verbindingseigenschappen opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De hostserver van uw toepassing. Dit is vaak uw subdomein. |
| `clientId` | De client-id die is gekoppeld aan uw [!DNL Salesforce Marketing Cloud]-toepassing. |
| `clientSecret` | Het clientgeheim dat is gekoppeld aan uw [!DNL Salesforce Marketing Cloud]-toepassing. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce Marketing Cloud] is: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

Raadpleeg dit [[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm) voor meer informatie over aan de slag gaan.

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL Salesforce Marketing Cloud] authentificatiegeloofsbrieven als deel van het verzoeklichaam.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.clientId` | De client-id die is gekoppeld aan uw [!DNL Salesforce Marketing Cloud]-toepassing. |
| `auth.params.clientSecret` | Het clientgeheim dat is gekoppeld aan uw [!DNL Salesforce Marketing Cloud]-toepassing. |
| `connectionSpec.id` | De [!DNL Salesforce Marketing Cloud] ID van de verbindingsspecificatie: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

**Antwoord**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Door deze zelfstudie te volgen hebt u een [!DNL Salesforce Marketing Cloud]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsID in de volgende zelfstudie gebruiken aangezien u leert hoe te om [de systemen van de marketing automatisering te onderzoeken gebruikend de Dienst API van de Stroom](../../explore/marketing-automation.md).
