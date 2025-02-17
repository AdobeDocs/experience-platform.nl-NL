---
title: Een Microsoft Dynamics Base Connection maken met de Flow Service API
description: Leer hoe u Platform kunt verbinden met een Microsoft Dynamics-account met behulp van de Flow Service API.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: bda26fa4ecf4f54cb36ffbedf6a9aa13faf7a09d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL Microsoft Dynamics]

Lees deze gids om te leren hoe u uw [!DNL Microsoft Dynamics] bron aan Adobe Experience Platform kunt verbinden gebruikend [[!DNL Flow Service]  API ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

De volgende secties bevatten aanvullende informatie die u moet weten om Platform met een Dynamics-account te kunnen verbinden met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Dynamics] als u waarden opgeeft voor de volgende verbindingseigenschappen:

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] -instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] -gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] -account. |

>[!TAB  dienst-hoofd en zeer belangrijke authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `servicePrincipalId` | De client-id van uw [!DNL Dynamics] -account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

>[!ENDTABS]

Voor meer informatie bij het worden begonnen, verwijs naar [ dit  [!DNL Dynamics]  document ](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL Dynamics] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Dynamics] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u een [!DNL Dynamics] -basisverbinding wilt maken met behulp van basisverificatie, dient u een POST-aanvraag in bij de [!DNL Flow Service] API en geeft u waarden op voor de `serviceUri` , `username` en `password` van de verbinding.

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor een [!DNL Dynamics] -bron gemaakt met behulp van basisverificatie.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.serviceUri` | De service-URI die aan uw [!DNL Dynamics] -instantie is gekoppeld. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Dynamics] -account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Dynamics] account is gekoppeld. |
| `connectionSpec.id` | De [!DNL Dynamics] connection specification ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Reactie**

Een succesvolle reactie keert de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Selecteren om reactievoorbeeld weer te geven

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB  de dienst belangrijkste op sleutel-gebaseerde authentificatie ]

Als u een [!DNL Dynamics] -basisverbinding wilt maken met behulp van service principal key-verificatie, dient u een POST-aanvraag in bij de [!DNL Flow Service] API en geeft u waarden op voor de `serviceUri` , `servicePrincipalId` en `servicePrincipalKey` van uw verbinding.

**Verzoek**

Met het volgende verzoek wordt een basisverbinding voor een [!DNL Dynamics] -bron gemaakt met behulp van basisverificatie op basis van hoofdsleutels van de service.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.serviceUri` | De service-URI die aan uw [!DNL Dynamics] -instantie is gekoppeld. |
| `auth.params.servicePrincipalId` | De client-id van uw [!DNL Dynamics] -account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `auth.params.servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |
| `connectionSpec.id` | De [!DNL Dynamics] connection specification ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug.

+++Selecteren om reactievoorbeeld weer te geven

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## Uw gegevenstabellen verkennen

Als u de gegevenstabellen van [!DNL Dynamics] wilt verkennen, vraagt u GET het `/connections/{BASE_CONNECTION_ID}/explore` -eindpunt aan en geeft u uw basis-verbindings-id op als onderdeel van de queryparameters.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Query-parameters | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding. Gebruik deze id om de inhoud en structuur van uw bron te verkennen. |

**Verzoek**

Met de volgende aanvraag wordt de lijst met beschikbare tabellen en weergaven opgehaald voor een [!DNL Dynamics] -bron met de id van de basisverbinding: `dd668808-25da-493f-8782-f3433b976d1e` .

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een geslaagde reactie retourneert de map [!DNL Dynamics] tables and views op het hoofdniveau.

+++Selecteren om reactievoorbeeld weer te geven

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++


## De structuur van een tabel controleren

Als u de structuur van een specifieke tabel wilt inspecteren, vraagt u GET `/connections/{BASE_CONNECTION_ID}/explore` aan en geeft u het pad naar de specifieke tabel op als een queryparameter.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| Query-parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding. Gebruik deze id om de inhoud en structuur van uw bron te verkennen. |
| `{TABLE_PATH}` | Het pad naar de tabel die u wilt verkennen. |

**Verzoek**

Met de volgende aanvraag worden de structuur en inhoud van een [!DNL Dynamics] -tabel met pad `workflowdependency` opgehaald.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een geslaagde reactie retourneert de inhoud van het pad `workflowdependency` .

+++Selecteren om reactievoorbeeld weer te geven

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## De structuur van een weergave controleren

In [!DNL Dynamics] verwijst een weergave naar de kolommen die moeten worden weergegeven, de breedte van elke kolom, het standaardsysteem waarin een lijst met records wordt gesorteerd en de standaardfilters die worden toegepast om te beperken welke records in de lijst worden weergegeven.

Als u de structuur van een weergave wilt inspecteren, vraagt u GET `/connections/{BASE_CONNECTION_ID}/explore` aan en geeft u het weergavepad op in de queryparameters. Daarnaast moet u `objectType` als `view` opgeven.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| Query-parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding. Gebruik deze id om de inhoud en structuur van uw bron te verkennen. |
| `{VIEW_PATH}` | Het pad naar de weergave die u wilt inspecteren. |

**Verzoek**

Met de volgende aanvraag wordt `accountView1` opgehaald.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een geslaagde reactie retourneert de structuur van `accountView1` .

+++Selecteren om reactievoorbeeld weer te geven

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## Weergave entiteitstype voorvertonen

Als u een voorvertoning van de inhoud van een weergave wilt weergeven, vraagt u GET om `/connections/{BASE_CONNECTION_ID}/explore` en neemt u het weergavepad en `preview=true` op in de queryparameters.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| Query-parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De id van de basisverbinding. Gebruik deze id om de inhoud en structuur van uw bron te verkennen. |
| `{VIEW_PATH}` | Het pad naar de weergave die u wilt inspecteren. |


**Verzoek**

In de volgende aanvraag wordt een voorvertoning van de inhoud van `accountView1` weergegeven.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Reactie**

Een succesvol antwoord retourneert de inhoud van `accountView1` .

+++Selecteren om reactievoorbeeld weer te geven

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## Een bronverbinding maken met de ingesloten weergave

Als u een bronverbinding wilt maken en een weergave wilt insluiten, vraagt u een POST-aanvraag naar het eindpunt van `/sourceConnections` , geeft u de tabelnaam op en geeft u `entityType` as `view` op in de hoofdtekst van de aanvraag.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een [!DNL Dynamics] bronverbinding gemaakt en worden weergaven ingesloten.

+++Selecteren om aanvraagvoorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**Reactie**

Een geslaagde reactie retourneert de zojuist gegenereerde bron-verbindings-id en de bijbehorende tag.

+++Selecteren om reactievoorbeeld weer te geven

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Microsoft Dynamics] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van CRM aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/crm.md)
