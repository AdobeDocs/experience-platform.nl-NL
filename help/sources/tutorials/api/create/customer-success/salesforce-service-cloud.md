---
title: Een Cloud Source Connection van de Salesforce-service maken met behulp van de Flow Service API
description: Leer hoe u Adobe Experience Platform met de Flow Service API kunt verbinden met Salesforce Service Cloud.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Een [!DNL Salesforce Service Cloud] bronverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees deze zelfstudie om te leren hoe u een basisverbinding maakt voor [!DNL Salesforce Service Cloud] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Salesforce Service Cloud] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

De [!DNL Salesforce Service Cloud] De bron steunt basisauthentificatie en de Credentials van de Cliënt OAuth2.

>[!BEGINTABS]

>[!TAB Basisverificatie]

Als u verbinding wilt maken met uw [!DNL Salesforce Service Cloud] account aan [!DNL Flow Service] het gebruiken van basisauthentificatie, verstrek waarden voor de volgende geloofsbrieven:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de [!DNL Salesforce Service Cloud] broninstantie. |
| `username` | De gebruikersnaam voor de [!DNL Salesforce Service Cloud] gebruikersaccount. |
| `password` | Het wachtwoord voor de [!DNL Salesforce Service Cloud] gebruikersaccount. |
| `securityToken` | De beveiligingstoken voor de [!DNL Salesforce Service Cloud] gebruikersaccount. |
| `apiVersion` | (Optioneel) De REST API-versie van de [!DNL Salesforce Service Cloud] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce Service Cloud] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Ga voor meer informatie over aan de slag gaan [dit Salesforce-document](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2 Client Credential]

Als u verbinding wilt maken met uw [!DNL Salesforce Service Cloud] account aan [!DNL Flow Service] Gebruik OAuth 2 Client Credential en geef waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de [!DNL Salesforce Service Cloud] broninstantie. |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce Service Cloud]. |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce Service Cloud]. |
| `apiVersion` | De REST API-versie van de [!DNL Salesforce Service Cloud] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. Deze waarde is verplicht voor OAuth2 Client Credential-verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce Service Cloud] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Voor meer informatie over het gebruik van OAuth voor [!DNL Salesforce Service Cloud], lees de [[!DNL Salesforce Service Cloud] handleiding over OAuth Authorization Flows](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL Salesforce Service Cloud] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```http
POST /connections
```

**Verzoek**

>[!BEGINTABS]

>[!TAB Basisverificatie]

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Salesforce Service Cloud] basisverificatie gebruiken:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschrijving |
| ---| --- |
| `auth.params.environmentUrl` | De URL van uw [!DNL Salesforce Service Cloud] -instantie. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Salesforce Service Cloud] account. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Salesforce Service Cloud] account. |
| `auth.params.securityToken` | Het veiligheidstoken verbonden aan uw [!DNL Salesforce Service Cloud] account. |
| `connectionSpec.id` | De [!DNL Salesforce Service Cloud] Verbindingsspecificatie-id: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB OAuth2 Client Credential]

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Salesforce Service Cloud] gebruik van OAuth 2 Client Credential:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
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
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.environmentUrl` | De URL van uw [!DNL Salesforce Service Cloud] -instantie. |
| `auth.params.clientId` | De client-id die aan uw [!DNL Salesforce Service Cloud] account. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL Salesforce Service Cloud] account. |
| `auth.params.apiVersion` | De REST API-versie van de [!DNL Salesforce Service Cloud] -instantie die u gebruikt. |
| `connectionSpec.id` | De [!DNL Salesforce Service Cloud] Verbindingsspecificatie-id: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**Antwoord**

Een geslaagde reactie retourneert de nieuwe basisverbinding samen met de unieke id.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Salesforce Service Cloud] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een dataflow om gegevens van het klantsucces naar Platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/customer-success.md)
