---
title: Creeer een Verbinding van de Basis van de Marketing Cloud Salesforce gebruikend de Dienst API van de Stroom
description: Leer hoe u uw Salesforce-Marketing Cloud met behulp van de Flow Service API voor Experience Platform verifieert.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 1%

---

# Een [!DNL Salesforce Marketing Cloud] basisverbinding met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de [!DNL Salesforce Marketing Cloud] bronintegratie.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Salesforce Marketing Cloud] met de [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

De volgende sectie bevat aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL Salesforce Marketing Cloud] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Salesforce Marketing Cloud]moet u de volgende eigenschappen voor de verbinding opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | De hostserver van uw toepassing. Dit is vaak uw subdomein. **Opmerking:** Wanneer u uw `host` waarde, hoeft u alleen het subdomein op te geven en niet de volledige URL. Als de host-URL bijvoorbeeld `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, hoeft u alleen maar in te voeren `acme-ab12c3d4e5fg6hijk7lmnop8qrst` als uw hostwaarde. |
| `clientId` | De client-id die aan uw [!DNL Salesforce Marketing Cloud] toepassing. |
| `clientSecret` | Het clientgeheim dat aan uw [!DNL Salesforce Marketing Cloud] toepassing. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Salesforce Marketing Cloud] is: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Raadpleeg voor meer informatie over aan de slag gaan [[!DNL Salesforce Marketing Cloud] document](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL Salesforce Marketing Cloud] verificatiegegevens als onderdeel van de aanvraaginstantie.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Salesforce Marketing Cloud]:

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
| `auth.params.clientId` | De client-id die aan uw [!DNL Salesforce Marketing Cloud] toepassing. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL Salesforce Marketing Cloud] toepassing. |
| `connectionSpec.id` | De [!DNL Salesforce Marketing Cloud] Verbindingsspecificatie-id: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Salesforce Marketing Cloud] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om marketingautomatiseringsgegevens naar het platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/marketing-automation.md)
