---
title: Een Eloqua-basisverbinding voor Oracles maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform met Oracle Eloqua kunt verbinden met behulp van de Flow Service API.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Een [!DNL Oracle Eloqua] basisverbinding maken met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De bron [!DNL Oracle Eloqua] wordt eind mei 2025 vervangen. U kunt ook de [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) -bron gebruiken.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Oracle Eloqua] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Platform:

* [ Bronnen ](../../../../home.md): Het platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): Het platform verstrekt virtuele zandbakken die één enkele [!DNL Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met [!DNL Oracle Eloqua] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Oracle Eloqua] als u waarden opgeeft voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| `endpoint` | Het eindpunt van de [!DNL Oracle Eloqua] . |
| `username` | De gebruikersnaam van uw [!DNL Oracle Eloqua] -account. De gebruikersnaam moet zijn opgemaakt als `siteName + \\ + username` , waarbij `siteName` de bedrijfsnaam is die u hebt gebruikt om u aan te melden bij [!DNL Oracle Eloqua] en `username` de gebruikersnaam is. De gebruikersnaam voor uw aanmelding kan bijvoorbeeld: `adobe\\emily` zijn. |
| `password` | Het wachtwoord voor uw [!DNL Oracle Eloqua] -gebruikersnaam. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De waarde voor de verbindingsspecificatie-id van de [!DNL Oracle Eloqua] -bron is vast als: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003` . |

Voor meer informatie over authentificatiegeloofsbrieven voor [!DNL Oracle Eloqua], zie de [[!DNL Oracle Eloqua]  gids over authentificatie ](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Oracle Eloqua] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Oracle Eloqua] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `name` | De naam van uw [!DNL Oracle Eloqua] basisverbinding. Het wordt aanbevolen een beschrijvende naam op te geven, aangezien u met deze waarde uw basisverbinding kunt opzoeken. |
| `description` | (Optioneel) Een eigenschap die u kunt opnemen voor aanvullende informatie over de basisverbinding. |
| `auth.specName` | Het verificatietype dat voor de verbinding wordt gebruikt. |
| `auth.params.endpoint` | Het eindpunt van de [!DNL Oracle Eloqua] -server. |
| `auth.params.username` | De samengevoegde referentie die de sitenaam en gebruikersnaam bevat die overeenkomen met uw [!DNL Oracle Eloqua] -account. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw [!DNL Oracle Eloqua] -account. |
| `connectionSpec.id` | De waarde voor de verbindingsspecificatie-id van de [!DNL Oracle Eloqua] -bron is vast als: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde basisverbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Oracle Eloqua] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om marketing automatiseringsgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/marketing-automation.md)
