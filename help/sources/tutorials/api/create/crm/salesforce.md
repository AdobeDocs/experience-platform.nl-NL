---
title: Salesforce verbinden met Experience Platform met behulp van de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met een Salesforce-account met behulp van de Flow Service API.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 56307d8457ba6d0046ad80a7c97405220aa6161c
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Salesforce] API[!DNL Flow Service]

Lees deze gids om te leren hoe u uw [!DNL Salesforce] bronrekening met Adobe Experience Platform kunt verbinden gebruikend [[!DNL Flow Service]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

## Verbinding maken [!DNL Salesforce] met Experience Platform op [!DNL Azure] {#azure}

Lees de onderstaande stappen voor informatie over hoe u de [!DNL Salesforce] -bron kunt verbinden met Experience Platform op [!DNL Azure] .

### Vereiste referenties verzamelen

>[!WARNING]
>
>Basisverificatie voor de [!DNL Salesforce] -bron wordt in januari 2026 afgekeurd. U moet naar OAuth 2 Client Credential-verificatie gaan om de bron te kunnen blijven gebruiken en gegevens van uw [!DNL Salesforce] -account te kunnen invoeren naar Experience Platform.

De [!DNL Salesforce] -bron ondersteunt basisverificatie en OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u uw [!DNL Salesforce] -account wilt verbinden met [!DNL Flow Service] via basisverificatie, geeft u waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de broninstantie [!DNL Salesforce] . De notatie voor `environmentUrl` is `https://[domain].my.salesforce.com` . |
| `username` | De gebruikersnaam voor de gebruikersaccount van [!DNL Salesforce] . |
| `password` | Het wachtwoord voor de [!DNL Salesforce] -gebruikersaccount. |
| `securityToken` | Het beveiligingstoken voor de gebruikersaccount van [!DNL Salesforce] . |
| `apiVersion` | (Optioneel) De REST API-versie van de instantie [!DNL Salesforce] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt Experience Platform automatisch de meest recente beschikbare versie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

Voor meer informatie bij begonnen worden, bezoek [&#x200B; dit document van Salesforce &#x200B;](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB  OAuth 2 de Credentials van de Cliënt ]

Als u uw [!DNL Salesforce] -account wilt verbinden met [!DNL Flow Service] via OAuth 2 Client Credential, geeft u waarden op voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| `environmentUrl` | De URL van de broninstantie [!DNL Salesforce] . De notatie voor `environmentUrl` is `https://[domain].my.salesforce.com` |
| `clientId` | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce] . |
| `clientSecret` | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce] . |
| `apiVersion` | De REST API-versie van de instantie [!DNL Salesforce] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt Experience Platform automatisch de meest recente beschikbare versie. Deze waarde is verplicht voor OAuth2 Client Credential-verificatie. |
| `includeDeletedObjects` | Een booleaanse waarde die wordt gebruikt om te bepalen of zachte verwijderde records moeten worden opgenomen. Als deze optie is ingesteld op true, kunnen elektronisch verwijderde records worden opgenomen in uw [!DNL Salesforce] -query en vanuit uw account worden opgenomen in Experience Platform. Als u de configuratie niet opgeeft, wordt deze waarde standaard ingesteld op `false` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce] is: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

Voor meer informatie bij het gebruiken van OAuth voor [!DNL Salesforce], lees de [[!DNL Salesforce]  gids over de Stroom van de Vergunning OAuth &#x200B;](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

### Een basisverbinding maken voor [!DNL Salesforce] in Experience Platform op [!DNL Azure]

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basisverbinding wilt maken en uw [!DNL Salesforce] -account op [!DNL Azure] wilt verbinden met Experience Platform, dient u een POST-aanvraag in bij het `/connections` -eindpunt en geeft u de [!DNL Salesforce] verificatiereferenties op in de hoofdtekst van de aanvraag.

**API formaat**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

+++verzoek

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

+++

+++Response

Een geslaagde reactie retourneert de nieuwe basisverbinding samen met de unieke id.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB  OAuth 2 de Credentials van de Cliënt ]

+++verzoek

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
            "apiVersion": "60.0",
            "includeDeletedObjects": true
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
| `auth.params.includeDeletedObjects` | Een booleaanse waarde die wordt gebruikt om te bepalen of zachte verwijderde records moeten worden opgenomen. |
| `connectionSpec.id` | The [!DNL Salesforce] connection specification ID: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5` . |

+++


+++Response

Een geslaagde reactie retourneert de nieuwe basisverbinding samen met de unieke id.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## Verbinding maken [!DNL Salesforce] met Experience Platform op Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../../../landing/multi-cloud.md).

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL Salesforce] -bron kunt verbinden met Experience Platform op AWS.

### Vereisten

Voor informatie over hoe te opstelling uw [!DNL Salesforce] rekening om met Experience Platform op AWS te kunnen verbinden, lees het [[!DNL Salesforce]  overzicht &#x200B;](../../../../connectors/crm/salesforce.md#aws).

### Een basisverbinding maken voor [!DNL Salesforce] op Experience Platform op AWS

Als u een basisverbinding wilt maken en uw [!DNL Salesforce] -account wilt verbinden met Experience Platform op AWS, dient u een POST-aanvraag in bij het `/connections` -eindpunt en geeft u de juiste waarden voor uw referenties op.

**API formaat**

```http
POST /connections
```

**Verzoek**

+++Selecteren om verzoek weer te geven

Met de volgende aanvraag wordt een basisverbinding voor de [!DNL Salesforce] -bron in Experience Platform op AWS gemaakt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

Voor informatie over hoe te om uw [!DNL Salesforce] terug te winnen `jwtToken`, lees de gids op [&#x200B; hoe te opstelling a  [!DNL Salesforce]  bron om met Experience Platform op AWS &#x200B;](../../../../connectors/crm/salesforce.md#aws) te verbinden.

+++

**Reactie**

+++Selecteren om reactie weer te geven

Een geslaagde reactie retourneert de nieuwe basisverbinding samen met de unieke id.

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### De verbindingsstatus controleren

Om uw verbindingsstatus te verifiëren, dient u een GET-verzoek in bij het `/connections` -eindpunt en verstrekt u de id van de basisverbinding die in de aanmaakstap is gegenereerd.

**API formaat**

```http
GET /connections
```

**Verzoek**

+++Selecteren om verzoek weer te geven

Met de volgende aanvraag wordt informatie opgehaald voor de id van de basisverbinding: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` .

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

>[!BEGINTABS]

>[!TAB  initialiserend ]

+++Selecteren om reactievoorbeeld weer te geven

In het volgende antwoord wordt informatie weergegeven voor de basis-verbindings-id: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` in de status `initializing` .

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB  Toegelaten ]

+++Selecteren om reactievoorbeeld weer te geven

In het volgende antwoord wordt informatie weergegeven voor de basis-verbindings-id: `3e908d3f-c390-482b-9f44-43d3d4f2eb82` in de status `enabled` .

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Salesforce] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van CRM aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/crm.md)
