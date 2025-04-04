---
keywords: Experience Platform;home;populaire onderwerpen;orakel;
title: (Beta) Maak een Oracle Resys Base Connection met behulp van de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Oracle Responsys met behulp van de Flow Service API.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# (Beta) Maak een [!DNL Oracle Responsys] basisverbinding met de [!DNL Flow Service] API

>[!NOTE]
>
>De bron [!DNL Oracle Responsys] is in bèta. Zie het [ Bronoverzicht ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Oracle Responsys] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met [!DNL Oracle Responsys] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Oracle Responsys] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| `endpoint` | De URL van het REST-verificatiepunt van uw [!DNL Oracle Responsys] -instantie. |
| `clientId` | De client-id van uw [!DNL Oracle Responsys] -instantie. |
| `clientSecret` | Het clientgeheim van de instantie [!DNL Oracle Responsys] . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De waarde voor de verbindingsspecificatie-id van de [!DNL Oracle Responsys] -bron is vast als: `ff4274f2-c9a9-11eb-b8bc-0242ac130003` . |

Voor meer informatie over authentificatiegeloofsbrieven voor [!DNL Oracle Responsys], zie de [[!DNL Oracle Responsys]  gids over authentificatie ](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Oracle Responsys] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Oracle Responsys] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De naam van uw [!DNL Oracle Responsys] basisverbinding. Het wordt aanbevolen een beschrijvende naam op te geven, aangezien u met deze waarde uw basisverbinding kunt opzoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor aanvullende informatie over de basisverbinding. |
| `auth.specName` | Het verificatietype dat voor de verbinding wordt gebruikt. |
| `auth.params.endpoint` | Het REST-verificatiepunt URL van uw [!DNL Oracle Responsys] -server. |
| `auth.params.clientId` | De client-id van uw [!DNL Oracle Responsys] -instantie. |
| `auth.params.clientSecret` | Het clientgeheim van de instantie [!DNL Oracle Responsys] . |
| `connectionSpec.id` | De waarde voor de verbindingsspecificatie-id van de [!DNL Oracle Responsys] -bron is vast als: `ff4274f2-c9a9-11eb-b8bc-0242ac130003` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Oracle Responsys] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om marketing automatiseringsgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/marketing-automation.md)
