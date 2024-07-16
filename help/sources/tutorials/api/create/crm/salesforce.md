---
title: Een Salesforce Base-verbinding maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met een Salesforce-account met behulp van de Flow Service API.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 7d450ba3357389a2934f187e4838e534d698dd4a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---

# Een [!DNL Salesforce] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Salesforce] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om [!DNL Platform] met de API [!DNL Flow Service] te kunnen verbinden met een [!DNL Salesforce] -account.

### Vereiste referenties verzamelen

De [!DNL Salesforce] -bron ondersteunt basisverificatie en OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u uw [!DNL Salesforce] -account wilt verbinden met [!DNL Flow Service] via basisverificatie, geeft u waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de broninstantie [!DNL Salesforce] . |
| `username` | De gebruikersnaam voor de gebruikersaccount van [!DNL Salesforce] . |
| `password` | Het wachtwoord voor de [!DNL Salesforce] -gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de gebruikersaccount van [!DNL Salesforce] . |
| `apiVersion` | (Optioneel) De REST API-versie van de instantie [!DNL Salesforce] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

Voor meer informatie bij begonnen worden, bezoek [ dit document van Salesforce ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB  OAuth 2 de Credentials van de Cliënt ]

Als u uw [!DNL Salesforce] -account wilt verbinden met [!DNL Flow Service] via OAuth 2 Client Credential, geeft u waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de broninstantie [!DNL Salesforce] . |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce] . |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce] . |
| `apiVersion` | De REST API-versie van de instantie [!DNL Salesforce] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. Deze waarde is verplicht voor OAuth2 Client Credential-verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

Voor meer informatie bij het gebruiken van OAuth voor [!DNL Salesforce], lees de [[!DNL Salesforce]  gids over de Stroom van de Vergunning OAuth ](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Salesforce] -verificatiegegevens op in de aanvraaginstantie.

**API formaat**

```http
POST /connections
```

**Verzoek**

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Salesforce] gemaakt met behulp van basisverificatie:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.environmentUrl` | De URL van de instantie [!DNL Salesforce] . |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Salesforce] -account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Salesforce] account is gekoppeld. |
| `auth.params.securityToken` | Het beveiligingstoken dat aan uw [!DNL Salesforce] -account is gekoppeld. |
| `connectionSpec.id` | The [!DNL Salesforce] connection specification ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

>[!TAB  OAuth 2 de Credentials van de Cliënt ]

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Salesforce] gemaakt met OAuth 2 Client Credential:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.environmentUrl` | De URL van de instantie [!DNL Salesforce] . |
| `auth.params.clientId` | De client-id die aan uw [!DNL Salesforce] -account is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL Salesforce] -account is gekoppeld. |
| `auth.params.apiVersion` | De REST API-versie van de instantie [!DNL Salesforce] die u gebruikt. |
| `connectionSpec.id` | The [!DNL Salesforce] connection specification ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

>[!ENDTABS]

**Reactie**

Een geslaagde reactie retourneert de nieuwe basisverbinding samen met de unieke id.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Salesforce] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van CRM aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/crm.md)
