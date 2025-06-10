---
title: Een Azure Event Hubs Source Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met een Azure Event Hubs-account met behulp van de Flow Service API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 0%

---

# Een [!DNL Azure Event Hubs] bronverbinding maken met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze zelfstudie om te leren hoe te om [!DNL Azure Event Hubs] (verder als &quot;[!DNL Event Hubs]&quot;worden doorverwezen) met Experience Platform te verbinden, gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

- [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
- [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u [!DNL Event Hubs] met de API van [!DNL Flow Service] kunt verbinden met Experience Platform.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met uw [!DNL Event Hubs] -account als u waarden opgeeft voor de volgende verbindingseigenschappen:

>[!BEGINTABS]

>[!TAB  Standaard authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De primaire sleutel van de naamruimte [!DNL Event Hubs] . De `sasPolicy` die `sasKey` aansluit bij `manage` , moet rechten hebben geconfigureerd om de [!DNL Event Hubs] -lijst te vullen. |
| `namespace` | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De [!DNL Event Hubs] -id van de verbindingsspecificatie is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` . |

>[!TAB  SAS authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `sasKey` | De primaire sleutel van de naamruimte [!DNL Event Hubs] . De `sasPolicy` die `sasKey` aansluit bij `manage` , moet rechten hebben geconfigureerd om de [!DNL Event Hubs] -lijst te vullen. |
| `namespace` | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |
| `eventHubName` | Vul de naam [!DNL Azure Event Hub] in. Lees de [ documentatie van Microsoft ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) voor meer informatie over [!DNL Event Hub] namen. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De [!DNL Event Hubs] -id van de verbindingsspecificatie is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` . |

Voor meer informatie over de authentificatie van gedeelde toegangshandtekeningen (SAS) voor [!DNL Event Hubs], lees de [[!DNL Azure]  gids bij het gebruiken van SAS ](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB  Hub van de Gebeurtenis Azure Actieve Auth van de Folder ]

| Credentials | Beschrijving |
| --- | --- |
| `tenantId` | De huurder-id waarvan u toestemming wilt vragen. Uw huurder identiteitskaart kan als GUID of als vriendschappelijke naam worden geformatteerd. **Nota**: De huurder identiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in de [!DNL Microsoft Azure] interface. |
| `clientId` | De toepassings-id die aan uw app is toegewezen. U kunt deze id ophalen via de portal [!DNL Microsoft Entra ID] waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| `clientSecretValue` | Het clientgeheim dat naast de client-id wordt gebruikt om uw app te verifiëren. U kunt uw clientgeheim ophalen via de [!DNL Microsoft Entra ID] -portal waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| `namespace` | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |

Voor meer informatie over [!DNL Azure Active Directory], lees de [ Azure gids bij het gebruiken van identiteitskaart van Microsoft Entra ](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB  Hub Scoped Azure Actieve Auth van de Folder van de Gebeurtenis ]

| Credentials | Beschrijving |
| --- | --- |
| `tenantId` | De huurder-id waarvan u toestemming wilt vragen. Uw huurder identiteitskaart kan als GUID of als vriendschappelijke naam worden geformatteerd. **Nota**: De huurder identiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in de [!DNL Microsoft Azure] interface. |
| `clientId` | De toepassings-id die aan uw app is toegewezen. U kunt deze id ophalen via de portal [!DNL Microsoft Entra ID] waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| `clientSecretValue` | Het clientgeheim dat naast de client-id wordt gebruikt om uw app te verifiëren. U kunt uw clientgeheim ophalen via de [!DNL Microsoft Entra ID] -portal waar u uw [!DNL Azure Active Directory] hebt geregistreerd. |
| `namespace` | De naamruimte van de [!DNL Event Hub] die u opent. Een naamruimte [!DNL Event Hub] biedt een unieke container voor het bereik, waarin u een of meer naamruimten kunt maken [!DNL Event Hubs] . |
| `eventHubName` | Vul de naam [!DNL Azure Event Hub] in. Lees de [ documentatie van Microsoft ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) voor meer informatie over [!DNL Event Hub] namen. |

>[!ENDTABS]

Voor meer informatie over deze waarden, verwijs naar [ dit document van de Hubs van deze Gebeurtenis ](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL Event Hubs] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

De eerste stap bij het maken van een bronverbinding is het verifiëren van de [!DNL Event Hubs] -bron en het genereren van een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Event Hubs] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Standaard authentificatie ]

Als u een account wilt maken met standaardverificatie, vraagt u een POST-aanvraag naar het eindpunt van `/connections` en geeft u de waarden voor de `sasKeyName` , `sasKey` en `namespace` .

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}"
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `auth.params.sasKey` | De gegenereerde handtekening voor gedeelde toegang. |
| `auth.params.namespace` | De naamruimte van de [!DNL Event Hubs] die u opent. |
| `connectionSpec.id` | De [!DNL Event Hubs] connection specification ID is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze verbinding-id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB  SAS authentificatie ]

Als u een account wilt maken met behulp van SAS-verificatie, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u waarden op voor uw `sasKeyName` , `sasKey` , `namespace` en `eventHubName` .

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.sasKeyName` | De naam van de machtigingsregel, ook wel de SAS-sleutelnaam genoemd. |
| `auth.params.sasKey` | De gegenereerde handtekening voor gedeelde toegang. |
| `auth.params.namespace` | De naamruimte van de [!DNL Event Hubs] die u opent. |
| `params.eventHubName` | De naam voor de [!DNL Event Hubs] -bron. |
| `connectionSpec.id` | De [!DNL Event Hubs] connection specification ID is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze verbinding-id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB  Hub van de Gebeurtenis Azure Actieve Auth van de Folder ]

Als u een account wilt maken met Azure Active Directory Auth, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u waarden op voor de `tenantId` , `clientId` , `clientSecretValue` en `namespace` .

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.tenantId` | De huurder-id van uw toepassing. **Nota**: De huurder identiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in de [!DNL Microsoft Azure] interface. |
| `auth.params.clientId` | De client-id van uw organisatie. |
| `auth.params.clientSecretValue` | De geheime waarde van de cliënt van uw organisatie. |
| `auth.params.namespace` | De naamruimte van de [!DNL Event Hubs] die u opent. |
| `connectionSpec.id` | De [!DNL Event Hubs] connection specification ID is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze verbinding-id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB  Hub Scoped Azure Actieve Auth van de Folder van de Gebeurtenis ]

Als u een account wilt maken met Azure Active Directory Auth, vraagt u een POST-aanvraag naar het eindpunt van `/connections` en geeft u waarden op voor uw `tenantId` , `clientId` , `clientSecretValue` , `namespace` en `eventHubName` .

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.tenantId` | De huurder-id van uw toepassing. **Nota**: De huurder identiteitskaart wordt bedoeld als &quot;identiteitskaart van de Folder&quot;in de [!DNL Microsoft Azure] interface. |
| `auth.params.clientId` | De client-id van uw organisatie. |
| `auth.params.clientSecretValue` | De geheime waarde van de cliënt van uw organisatie. |
| `auth.params.namespace` | De naamruimte van de [!DNL Event Hubs] die u opent. |
| `auth.params.eventHubName` | De naam voor de [!DNL Event Hubs] -bron. |
| `connectionSpec.id` | De [!DNL Event Hubs] connection specification ID is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++Response

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze verbinding-id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## Een bronverbinding maken

>[!TIP]
>
>Een consumentengroep van [!DNL Event Hubs] kan slechts voor één enkele stroom in een bepaald tijd worden gebruikt.

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en een identiteitskaart van de bronverbinding nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie.

Als u een bronverbinding wilt maken, vraagt u een POST-aanvraag naar het `/sourceConnections` -eindpunt van de [!DNL Flow Service] API.

**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Azure Event Hubs source connection",
      "description": "A source connection for Azure Event Hubs",
      "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "eventHubName": "{EVENT_HUB_NAME}",
          "dataType": "raw",
          "reset": "latest",
          "consumerGroup": "{CONSUMER_GROUP}"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de bronverbinding. Zorg ervoor dat de naam van uw bronverbinding beschrijvend is aangezien u dit kunt gebruiken om informatie over uw bronverbinding op te zoeken. |
| `description` | Een optionele waarde die u kunt opgeven voor meer informatie over uw bronverbinding. |
| `baseConnectionId` | De verbindings-id van de [!DNL Event Hubs] -bron die in de vorige stap is gegenereerd. |
| `connectionSpec.id` | The fixed connection specification ID for [!DNL Event Hubs]. Deze id is: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` . |
| `data.format` | De indeling van de [!DNL Event Hubs] -gegevens die u wilt invoeren. Momenteel is de enige ondersteunde gegevensindeling `json` . |
| `params.eventHubName` | De naam voor de [!DNL Event Hubs] -bron. |
| `params.dataType` | Deze parameter bepaalt het type van de gegevens die worden opgenomen. Tot de ondersteunde gegevenstypen behoren: `raw` en `xdm` . |
| `params.reset` | Deze parameter bepaalt hoe de gegevens worden gelezen. Gebruik `latest` om te beginnen met het lezen van de meest recente gegevens en gebruik `earliest` om te beginnen met het lezen van de eerste beschikbare gegevens in de stream. Deze parameter is optioneel en wordt standaard ingesteld op `earliest` als deze niet wordt opgegeven. |
| `params.consumerGroup` | Het publicatie- of abonnementsmechanisme dat voor [!DNL Event Hubs] moet worden gebruikt. Deze parameter is optioneel en wordt standaard ingesteld op `$Default` als deze niet wordt opgegeven. Verwijs naar deze [[!DNL Event Hubs]  gids op gebeurtenisconsumenten ](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) voor meer informatie. **Nota**: Een [!DNL Event Hubs] consumentengroep kan slechts voor één enkele stroom in een bepaalde tijd worden gebruikt. |

>[!NOTE]
>
>Nadat u een streaming gegevensstroom hebt gemaakt of bijgewerkt, moet u de gegevensinvoer kort na vijf minuten pauzeren om te voorkomen dat gegevens verloren gaan of dat gegevens verloren gaan.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Event Hubs] -bronverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze bron verbindingsidentiteitskaart in het volgende leerprogramma gebruiken om [ een het stromen dataflow tot stand te brengen gebruikend  [!DNL Flow Service]  API ](../../collect/streaming.md).
