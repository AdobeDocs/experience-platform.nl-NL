---
title: Een Amazon Redshift Base-verbinding maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Amazon Redshift met behulp van de Flow Service API.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Een [!DNL Amazon Redshift] basisverbinding maken met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De [!DNL Amazon Redshift] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Amazon Redshift] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Amazon Redshift] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Amazon Redshift] als u de volgende verbindingseigenschappen opgeeft:

| **Referentie** | **Beschrijving** |
| -------------- | --------------- |
| `server` | De server die aan uw [!DNL Amazon Redshift] account is gekoppeld. |
| `port` | De TCP-poort die een [!DNL Amazon Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| `username` | De gebruikersnaam die aan uw [!DNL Amazon Redshift] -account is gekoppeld. |
| `password` | Het wachtwoord dat aan uw [!DNL Amazon Redshift] account is gekoppeld. |
| `database` | De [!DNL Amazon Redshift] -database die u opent. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Amazon Redshift] is `3416976c-a9ca-4bba-901a-1f08f66978ff` . |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL Amazon Redshift]  document ](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!NOTE]
>
>De standaard coderingsstandaard voor [!DNL Redshift] is Unicode. Dit kan niet worden gewijzigd.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Amazon Redshift] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Amazon Redshift] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| ------------- | --------------- |
| `auth.params.server` | Uw [!DNL Amazon Redshift] -server. |
| `auth.params.port` | De TCP-poort die de [!DNL Amazon Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| `auth.params.database` | De database die aan uw [!DNL Amazon Redshift] -account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Amazon Redshift] account is gekoppeld. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Amazon Redshift] -account is gekoppeld. |
| `connectionSpec.id` | De [!DNL Amazon Redshift] connection specification ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Amazon Redshift] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
