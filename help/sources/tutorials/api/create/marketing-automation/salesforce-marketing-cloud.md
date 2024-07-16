---
title: Creeer een Verbinding van de Basis van de Marketing Cloud Salesforce gebruikend de Dienst API van de Stroom
description: Leer hoe u uw Salesforce-Marketing Cloud met behulp van de Flow Service API voor Experience Platform verifieert.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 30f1e8a0424ee0f81d8e98fb24886ad1480b270c
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Een [!DNL Salesforce Marketing Cloud] basisverbinding maken met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de bronintegratie van [!DNL Salesforce Marketing Cloud] .

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Salesforce Marketing Cloud] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

In de volgende sectie vindt u aanvullende informatie die u moet weten als u verbinding wilt maken met [!DNL Salesforce Marketing Cloud] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Salesforce Marketing Cloud] als u de volgende verbindingseigenschappen opgeeft:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De hostserver van uw toepassing. Dit is vaak uw subdomein. **Nota:** wanneer het ingaan van uw `host` waarde, moet u `{subdomain}.rest.marketingcloudapis.com` specificeren. Als de host-URL bijvoorbeeld `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` is, moet u `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` als waarde voor de host invoeren. |
| `clientId` | De client-id die aan uw [!DNL Salesforce Marketing Cloud] -toepassing is gekoppeld. |
| `clientSecret` | Het clientgeheim dat aan de toepassing [!DNL Salesforce Marketing Cloud] is gekoppeld. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce Marketing Cloud] is: `ea1c2a08-b722-11eb-8529-0242ac130003` . |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL Salesforce Marketing Cloud]  document ](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Salesforce Marketing Cloud] -verificatiegegevens op als onderdeel van de aanvraaginstantie.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Salesforce Marketing Cloud] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.clientId` | De client-id die aan uw [!DNL Salesforce Marketing Cloud] -toepassing is gekoppeld. |
| `auth.params.clientSecret` | Het clientgeheim dat aan de toepassing [!DNL Salesforce Marketing Cloud] is gekoppeld. |
| `connectionSpec.id` | The [!DNL Salesforce Marketing Cloud] connection specification ID: `ea1c2a08-b722-11eb-8529-0242ac130003` . |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Salesforce Marketing Cloud] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om marketing automatiseringsgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/marketing-automation.md)
