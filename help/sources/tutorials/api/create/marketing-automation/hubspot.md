---
keywords: Experience Platform;thuis;populaire onderwerpen;hubspot;Hubspot
solution: Experience Platform
title: Creeer een Verbinding van de Basis HubSpot Gebruikend de Dienst API van de Stroom
topic-legacy: overview
type: Tutorial
description: Leer hoe te om Adobe Experience Platform met HubSpot te verbinden gebruikend de Dienst API van de Stroom.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 143f3b4a113c6f36cb1bb0c3624c8503f158a16d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Een [!DNL HubSpot] basisverbinding maken met de [!DNL Flow Service]-API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie begeleidt u door de stappen om een basisverbinding voor [!DNL HubSpot] tot stand te brengen gebruikend [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md):  [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de  [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een verbinding met [!DNL HubSpot] met de [!DNL Flow Service]-API tot stand te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Flow Service] wilt laten verbinden met [!DNL HubSpot], moet u de volgende verbindingseigenschappen opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `clientId` | De client-id die is gekoppeld aan uw [!DNL HubSpot]-toepassing. |
| `clientSecret` | Het clientgeheim dat is gekoppeld aan uw [!DNL HubSpot]-toepassing. |
| `accessToken` | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `refreshToken` | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL HubSpot] is: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Voor meer informatie over begonnen worden, verwijs naar dit [document HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [Aan de slag met Platform APIs](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding tot stand te brengen, doe een verzoek van de POST aan het `/connections` eindpunt terwijl het verstrekken van uw [!DNL HubSpot] authentificatiegeloofsbrieven als deel van de verzoekparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Het volgende verzoek leidt tot een basisverbinding voor [!DNL HubSpot]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.clientId` | De client-id die is gekoppeld aan uw [!DNL HubSpot]-toepassing. |
| `auth.params.clientSecret` | Het clientgeheim dat is gekoppeld aan uw [!DNL HubSpot]-toepassing. |
| `auth.params.accessToken` | Het toegangstoken werd verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `auth.params.refreshToken` | Het vernieuwingstoken dat wordt verkregen toen aanvankelijk het voor authentiek verklaren van uw integratie OAuth. |
| `connectionSpec.id` | De [!DNL HubSpot] ID van de verbindingsspecificatie: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Antwoord**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Door deze zelfstudie te volgen hebt u een [!DNL HubSpot]-verbinding gemaakt met de API [!DNL Flow Service] en hebt u de unieke id-waarde van de verbinding verkregen. U kunt deze verbindingsID in de volgende zelfstudie gebruiken aangezien u leert hoe te om [de systemen van de marketing automatisering te onderzoeken gebruikend de Dienst API van de Stroom](../../explore/marketing-automation.md).
