---
title: Salesforce Service Cloud Source Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Salesforce Service Cloud met behulp van de Flow Service API.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Een [!DNL Salesforce Service Cloud] bronverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees dit leerprogramma leren hoe te om een basisverbinding voor [!DNL Salesforce Service Cloud] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Salesforce Service Cloud] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

>[!WARNING]
>
>Basisverificatie voor de [!DNL Salesforce Service Cloud] -bron wordt in januari 2026 afgekeurd. U moet naar OAuth 2 Client Credential-verificatie gaan om de bron te kunnen blijven gebruiken en gegevens van uw [!DNL Salesforce Service Cloud] -account te kunnen invoeren naar Experience Platform.

De [!DNL Salesforce Service Cloud] -bron ondersteunt basisverificatie en OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u uw [!DNL Salesforce Service Cloud] -account wilt verbinden met [!DNL Flow Service] via basisverificatie, geeft u waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de broninstantie [!DNL Salesforce Service Cloud] . |
| `username` | De gebruikersnaam voor de gebruikersaccount van [!DNL Salesforce Service Cloud] . |
| `password` | Het wachtwoord voor de [!DNL Salesforce Service Cloud] -gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de gebruikersaccount van [!DNL Salesforce Service Cloud] . |
| `apiVersion` | (Optioneel) De REST API-versie van de instantie [!DNL Salesforce Service Cloud] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt Experience Platform automatisch de meest recente beschikbare versie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce Service Cloud] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

Voor meer informatie bij begonnen worden, bezoek [ dit document van Salesforce ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB  OAuth 2 de Credentials van de Cliënt ]

Als u uw [!DNL Salesforce Service Cloud] -account wilt verbinden met [!DNL Flow Service] via OAuth 2 Client Credential, geeft u waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de broninstantie [!DNL Salesforce Service Cloud] . |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce Service Cloud] . |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce Service Cloud] . |
| `apiVersion` | De REST API-versie van de instantie [!DNL Salesforce Service Cloud] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt Experience Platform automatisch de meest recente beschikbare versie. Deze waarde is verplicht voor OAuth2 Client Credential-verificatie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce Service Cloud] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

Voor meer informatie bij het gebruiken van OAuth voor [!DNL Salesforce Service Cloud], lees de [[!DNL Salesforce Service Cloud]  gids over de Stroom van de Vergunning OAuth ](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Salesforce Service Cloud] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

**Verzoek**

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Salesforce Service Cloud] gemaakt met behulp van basisverificatie:

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
| `auth.params.environmentUrl` | De URL van de instantie [!DNL Salesforce Service Cloud] . |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Salesforce Service Cloud] -account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Salesforce Service Cloud] account is gekoppeld. |
| `auth.params.securityToken` | Het beveiligingstoken dat aan uw [!DNL Salesforce Service Cloud] -account is gekoppeld. |
| `connectionSpec.id` | De [!DNL Salesforce Service Cloud] connection specification ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB  OAuth2 Client Credential ]

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Salesforce Service Cloud] gemaakt met OAuth 2 Client Credential:

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
| `auth.params.environmentUrl` | De URL van de instantie [!DNL Salesforce Service Cloud] . |
| `auth.params.clientId` | De client-id die aan uw [!DNL Salesforce Service Cloud] -account is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL Salesforce Service Cloud] -account is gekoppeld. |
| `auth.params.apiVersion` | De REST API-versie van de instantie [!DNL Salesforce Service Cloud] die u gebruikt. |
| `connectionSpec.id` | The [!DNL Salesforce Service Cloud] connection specification ID: `cb66ab34-8619-49cb-96d1-39b37ede86ea` . |

>[!ENDTABS]

**Reactie**

Een geslaagde reactie retourneert de nieuwe basisverbinding samen met de unieke id.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Salesforce Service Cloud] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van het klantensucces aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/customer-success.md)
