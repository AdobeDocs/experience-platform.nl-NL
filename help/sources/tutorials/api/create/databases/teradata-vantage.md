---
keywords: Experience Platform;home;populaire onderwerpen;Teradata Vantage
title: Een Teradata Vantage Base Connection maken met de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Teradata Vantage met behulp van de Flow Service API.
exl-id: 88707dca-3c7a-43c7-9d71-473ad9715fc6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# Een [!DNL Teradata Vantage] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Teradata Vantage] tot stand te brengen gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../../../landing/api-guide.md).

In de volgende sectie vindt u aanvullende informatie die u moet weten als u verbinding wilt maken met [!DNL Teradata Vantage] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Teradata Vantage] als u de volgende verbindingseigenschappen opgeeft:

| Credentials | Beschrijving |
| --- | --- |
| `connectionString` | Een verbindingstekenreeks is een tekenreeks die informatie bevat over een gegevensbron en over de manier waarop u hiermee verbinding kunt maken. Het patroon van de verbindingstekenreeks voor [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}` . |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Teradata Vantage] is: `2fa8af9c-2d1a-43ea-a253-f00a00c74412` |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL Teradata Vantage]  document ](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL Teradata Vantage] -verificatiegegevens op als onderdeel van de aanvraagprocedure.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Teradata Vantage] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Teradata Vantage base connection",
      "description": "Teradata Vantage base connection",
      "auth": {
          "specName": "ConnectionString,
          "params": {
              "connectionString": "DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.connectionString` | De verbindingstekenreeks die wordt gebruikt om verbinding te maken met de instantie [!DNL Teradata Vantage] . Het patroon van de verbindingstekenreeks voor [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}` . |
| `connectionSpec.id` | The [!DNL Teradata Vantage] connection specification ID: `2fa8af9c-2d1a-43ea-a253-f00a00c74412` . |

**Reactie**

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn unieke verbindings herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Aan de hand van deze zelfstudie hebt u een [!DNL Teradata Vantage] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
