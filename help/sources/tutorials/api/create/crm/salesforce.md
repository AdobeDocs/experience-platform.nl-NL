---
title: Een Salesforce Base-verbinding maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met een Salesforce-account met behulp van de Flow Service API.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 7d450ba3357389a2934f187e4838e534d698dd4a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---

# Een [!DNL Salesforce] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Salesforce] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken [!DNL Platform] een [!DNL Salesforce] account gebruiken [!DNL Flow Service] API.

### Vereiste referenties verzamelen

De [!DNL Salesforce] De bron steunt basisauthentificatie en de Credentials van de Cliënt OAuth2.

>[!BEGINTABS]

>[!TAB Basisverificatie]

Als u verbinding wilt maken met uw [!DNL Salesforce] account aan [!DNL Flow Service] het gebruiken van basisauthentificatie, verstrek waarden voor de volgende geloofsbrieven:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de [!DNL Salesforce] broninstantie. |
| `username` | De gebruikersnaam voor de [!DNL Salesforce] gebruikersaccount. |
| `password` | Het wachtwoord voor de [!DNL Salesforce] gebruikersaccount. |
| `securityToken` | De beveiligingstoken voor de [!DNL Salesforce] gebruikersaccount. |
| `apiVersion` | Optioneel) De REST API-versie van de [!DNL Salesforce] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Ga voor meer informatie over aan de slag gaan [dit Salesforce-document](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2 Client Credential]

Als u verbinding wilt maken met uw [!DNL Salesforce] account aan [!DNL Flow Service] Gebruik OAuth 2 Client Credential en geef waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de [!DNL Salesforce] broninstantie. |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce]. |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce]. |
| `apiVersion` | De REST API-versie van de [!DNL Salesforce] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. Deze waarde is verplicht voor OAuth2 Client Credential-verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Voor meer informatie over het gebruik van OAuth voor [!DNL Salesforce], lees de [[!DNL Salesforce] handleiding over OAuth Authorization Flows](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` en biedt u uw [!DNL Salesforce] verificatiegegevens in de aanvraaginstantie.

**API-indeling**

```http
POST /connections
```

**Verzoek**

>[!BEGINTABS]

>[!TAB Basisverificatie]

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Salesforce] basisverificatie gebruiken:

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
| `auth.params.environmentUrl` | De URL van uw [!DNL Salesforce] -instantie. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Salesforce] account. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Salesforce] account. |
| `auth.params.securityToken` | Het veiligheidstoken verbonden aan uw [!DNL Salesforce] account. |
| `connectionSpec.id` | De [!DNL Salesforce] Verbindingsspecificatie-id: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!TAB OAuth 2 Client Credential]

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Salesforce] gebruik van OAuth 2 Client Credential:

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
| `auth.params.environmentUrl` | De URL van uw [!DNL Salesforce] -instantie. |
| `auth.params.clientId` | De client-id die aan uw [!DNL Salesforce] account. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL Salesforce] account. |
| `auth.params.apiVersion` | De REST API-versie van de [!DNL Salesforce] -instantie die u gebruikt. |
| `connectionSpec.id` | De [!DNL Salesforce] Verbindingsspecificatie-id: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

>[!ENDTABS]

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding samen met de unieke id.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Salesforce] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om CRM-gegevens naar het platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/crm.md)
