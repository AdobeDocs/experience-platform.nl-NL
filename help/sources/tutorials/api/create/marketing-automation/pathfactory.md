---
title: Een PathFactory Base Connection maken met de Flow Service API
description: Leer hoe u uw PathFactory-account verifieert aan de hand van de Flow Service API voor Experience Platform.
badge: Beta
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Een [!DNL PathFactory] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Lees dit document voor meer informatie over het maken van een basisverbinding voor [!DNL PathFactory] met de [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

De volgende sectie bevat aanvullende informatie die u nodig hebt om verbinding te kunnen maken met [!DNL PathFactory] met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen {#gather-credentials}

Om tot uw rekening PathFactory op het Platform toegang te hebben, moet u de volgende waarden verstrekken:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Gebruikersnaam | Uw [!DNL PathFactory] gebruikersnaam account. Dit is essentieel voor het identificeren van uw account in het systeem. |
| Wachtwoord | Het wachtwoord dat aan uw [!DNL PathFactory] account. Zorg ervoor dat dit veilig blijft om ongeoorloofde toegang te voorkomen. |
| Domein | Het domein dat aan uw [!DNL PathFactory] account. Dit verwijst doorgaans naar de unieke id in uw [!DNL PathFactory] URL. |
| Toegangstoken | Een uniek token dat wordt gebruikt voor API-verificatie om te zorgen voor veilige communicatie tussen uw systemen en [!DNL PathFactory]. |
| API-eindpunten | Specifieke API-eindpunten voor toegang tot gegevens: Bezoekers, Sessies en Paginaweergaven. Elk eindpunt komt overeen met verschillende gegevenssets die u kunt ophalen. **Opmerking:** Deze worden vooraf gedefinieerd door [!DNL PathFactory] en zijn specifiek voor de gegevens die u wilt gebruiken: <ul><li>**Eindpunt van bezoekers**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Sessieeindpunt**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Eindpunt van paginaweergaven**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Voor meer informatie over het beveiligen en gebruiken van uw geloofsbrieven, en hoe te om uw toegangstoken te verkrijgen en te verfrissen, bezoek [[!DNL PathFactory] Ondersteuningscentrum](https://support.pathfactory.com/categories/adobe/). Deze bron bevat uitgebreide handleidingen voor het beheer van uw referenties en voor een effectieve en veilige API-integratie.

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL PathFactory] verificatiegegevens als onderdeel van de aanvraaginstantie.

**API-indeling**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding gemaakt voor [!DNL PathFactory]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
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
| `auth.params.clientId` | De client-id die aan uw [!DNL PathFactory] toepassing. |
| `auth.params.clientSecret` | Het clientgeheim dat aan uw [!DNL PathFactory] toepassing. |
| `connectionSpec.id` | De [!DNL PathFactory] Verbindingsspecificatie-id: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke verbindings-id (`id`). Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL PathFactory] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om marketingautomatiseringsgegevens naar het platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/marketing-automation.md)
