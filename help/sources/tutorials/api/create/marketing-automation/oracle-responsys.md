---
keywords: Experience Platform;thuis;populaire onderwerpen;oracle;
title: (Bèta) creeer een Verbinding van de Basis van het Oracle Responsys gebruikend de Dienst API van de Stroom
description: Leer hoe te om Adobe Experience Platform met Oracle te verbinden Resys gebruikend de Dienst API van de Stroom.
source-git-commit: aa4573325f2859c258e66d4b6df411118a5d1942
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# (Beta) Maak een [!DNL Oracle Responsys] basisverbinding met de [!DNL Flow Service] API

>[!NOTE]
>
>De [!DNL Oracle Responsys] De bron is in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Oracle Responsys] met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Platform:

* [Bronnen](../../../../home.md): Met Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): Platform biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om verbinding te kunnen maken met [!DNL Oracle Responsys] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om te verbinden met [!DNL Oracle Responsys]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| --- | --- |
| `endpoint` | De URL van het REST-verificatiepunt van uw [!DNL Oracle Responsys] -instantie. |
| `clientId` | De client-id van uw [!DNL Oracle Responsys] -instantie. |
| `clientSecret` | Het clientgeheim van uw [!DNL Oracle Responsys] -instantie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De waarde van de verbindingsspecificatie-id van het dialoogvenster [!DNL Oracle Responsys] bron is vast als: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Voor meer informatie over verificatiereferenties voor [!DNL Oracle Responsys], zie de [[!DNL Oracle Responsys] handleiding voor verificatie](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Oracle Responsys] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL Oracle Responsys]:

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
| `auth.params.endpoint` | De URL van het REST-verificatiepunt van uw [!DNL Oracle Responsys] server. |
| `auth.params.clientId` | De client-id van uw [!DNL Oracle Responsys] -instantie. |
| `auth.params.clientSecret` | Het clientgeheim van uw [!DNL Oracle Responsys] -instantie. |
| `connectionSpec.id` | De waarde van de verbindingsspecificatie-id van het dialoogvenster [!DNL Oracle Responsys] bron is vast als: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Antwoord**

Een succesvolle reactie retourneert details van de zojuist gemaakte basisverbinding, inclusief de unieke id (`id`). Deze id is vereist in de volgende stap om een bronverbinding te maken.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Oracle Responsys] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om marketingautomatiseringsgegevens naar het Platform te brengen met de opdracht [!DNL Flow Service] API](../../collect/marketing-automation.md)
