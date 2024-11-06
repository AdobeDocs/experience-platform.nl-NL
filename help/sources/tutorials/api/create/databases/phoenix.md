---
title: Een Phoenix Base-verbinding maken met de Flow Service API
description: Leer hoe u een Phoenix-database met de Flow Service API met Adobe Experience Platform kunt verbinden.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Een [!DNL Phoenix] basisverbinding maken met de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De bron [!DNL Phoenix] wordt eind mei 2025 vervangen. U kunt de [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) gebruiken in plaats van de [!DNL Phoenix] -bron.

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Deze zelfstudie bevat stappen voor het maken van een basisverbinding en het aansluiten van uw [!DNL Phoenix] -account op Adobe Experience Platform met behulp van de [!DNL Flow Service] API.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Experience Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u moet weten voordat u verbinding kunt maken met [!DNL Phoenix] via de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

U moet de volgende verificatiereferenties opgeven om uw [!DNL Phoenix] -account aan te sluiten op het Experience Platform.

| Credentials | Beschrijving |
| ---------- | ----------- |
| `host` | Het IP-adres of de hostnaam van de [!DNL Phoenix] -server. |
| `username` | De gebruikersnaam die u gebruikt om toegang te krijgen tot [!DNL Phoenix] Server. |
| `password` | Het wachtwoord voor de gebruiker. |
| `port` | De TCP-poort die de [!DNL Phoenix] -server gebruikt om te luisteren naar clientverbindingen. Als u verbinding maakt met [!DNL Azure HDInsights] , geeft u de poort op als 443. Als deze parameter niet wordt opgegeven, wordt de standaardwaarde 8765 gebruikt. |
| `httpPath` | De gedeeltelijke URL die overeenkomt met de [!DNL Phoenix] -server. Geef /hbasephoenix0 op als u [!DNL Azure] HDInsights-cluster gebruikt. |
| `enableSsl` | Een booleaanse waarde. Geeft aan of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Phoenix] is: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Voor meer informatie over begonnen worden verwijs naar [ dit document Phoenix ](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basisverbinding wilt maken, vraagt u een POST naar het `/connections` -eindpunt terwijl u de [!DNL Phoenix] -verificatiegegevens opgeeft in de aanvraaginstantie.

**API formaat**

```https
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL Phoenix] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --------- | ----------- |
| `auth.params.host` | De host van de [!DNL Phoenix] -server. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Phoenix] -verbinding is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Phoenix] verbinding is gekoppeld. |
| `auth.params.port` | De TCP-poort voor uw [!DNL Phoenix] -verbinding. |
| `auth.params.httpPath` | Het gedeeltelijke http-pad voor uw [!DNL Phoenix] -verbinding. |
| `auth.params.enableSsl` | De booleaanse waarde die opgeeft of de verbindingen met de server via SSL zijn gecodeerd. |
| `connectionSpec.id` | The [!DNL Phoenix] connection specification ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43` . |

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Phoenix] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
