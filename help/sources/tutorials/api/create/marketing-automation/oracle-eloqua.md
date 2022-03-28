---
keywords: Experience Platform;thuis;populaire onderwerpen;oracle;eloqua;oracle eloqua
solution: Experience Platform
title: Een Eloqua-basisverbinding voor Oracles maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform met Oracle Eloqua kunt verbinden met behulp van de Flow Service API.
source-git-commit: 423f0efc3c0d9fb38cb8d1b16b885e1eddc23e72
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# Een [!DNL Oracle Eloqua] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Oracle Eloqua] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Platform:

* [Bronnen](../../../../home.md): Met Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): Platform biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met [!DNL Oracle Eloqua] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Oracle Eloqua]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| --- | --- |
| `endpoint` | Het eindpunt van uw [!DNL Oracle Eloqua]. |
| `username` | De gebruikersnaam van uw [!DNL Oracle Eloqua] account. De gebruikersnaam moet zijn opgemaakt als `siteName + \\ + username`, waarbij `siteName` is de bedrijfsnaam waarmee u zich hebt aangemeld [!DNL Oracle Eloqua] en `username` is uw gebruikersnaam. Uw gebruikersnaam voor aanmelding kan bijvoorbeeld: `adobe\\emily`. |
| `password` | Het wachtwoord dat overeenkomt met uw [!DNL Oracle Eloqua] gebruikersnaam. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De waarde van de verbindingsspecificatie-id van het dialoogvenster [!DNL Oracle Eloqua] bron is vast als: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Voor meer informatie over verificatiereferenties voor [!DNL Oracle Eloqua], zie de [[!DNL Oracle Eloqua] handleiding voor verificatie](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Oracle Eloqua] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.endpoint` | Het eindpunt van uw [!DNL Oracle Eloqua] server. |
| `auth.params.username` | De samengevoegde referentie die de sitenaam en gebruikersnaam bevat die overeenkomen met uw [!DNL Oracle Eloqua] account. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met uw [!DNL Oracle Eloqua] account. |
| `connectionSpec.id` | De waarde van de verbindingsspecificatie-id van het dialoogvenster [!DNL Oracle Eloqua] bron is vast als: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Oracle Eloqua] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van een marketingautomatiseringsbron met behulp van de [!DNL Flow Service] API](../../explore/marketing-automation.md)
* [Maak een gegevensstroom om marketingautomatiseringsgegevens naar het Platform te brengen met de opdracht [!DNL Flow Service] API](../../collect/marketing-automation.md)


