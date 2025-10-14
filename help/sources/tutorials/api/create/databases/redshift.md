---
title: Connect AWS Opnieuw overschakelen naar Experience Platform met behulp van de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met AWS Redshift met behulp van de Flow Service API.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Verbinding maken met Experience Platform via de [!DNL Flow Service] API[!DNL AWS Redshift]

>[!IMPORTANT]
>
>De [!DNL AWS Redshift] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze gids om te leren hoe u uw [!DNL AWS Redshift] bronrekening met Adobe Experience Platform kunt verbinden gebruikend [[!DNL Flow Service]  API &#x200B;](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [&#x200B; Sandboxen &#x200B;](../../../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md).

## Verbind [!DNL AWS Redshift] met Experience Platform op Azure {#azure}

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL AWS Redshift] -bron kunt verbinden met Experience Platform on Azure.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL AWS Redshift] als u de volgende verbindingseigenschappen opgeeft:

| Credentials | Beschrijving |
| `server` | De servernaam van de [!DNL AWS Redshift] -instantie. |
| `port` | De TCP-poort die een [!DNL AWS Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| `username` | De gebruikersnaam die aan uw [!DNL AWS Redshift] -account is gekoppeld. |
| `password` | Het wachtwoord dat overeenkomt met de gebruikersaccount. |
| `database` | De [!DNL AWS Redshift] -database waaruit gegevens moeten worden opgehaald. |
| `connectionSpec.id` | De verbindingsspecificatie keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL AWS Redshift] is `3416976c-a9ca-4bba-901a-1f08f66978ff` . |

Voor meer informatie over begonnen worden, verwijs naar dit [[!DNL AWS Redshift]  document &#x200B;](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html).

### Creeer een basisverbinding voor [!DNL AWS Redshift] op Experience Platform op Azure [ #azure-base ]

>[!NOTE]
>
>De standaard coderingsstandaard voor [!DNL Redshift] is Unicode. Dit kan niet worden gewijzigd.

Een basisverbinding behoudt informatie tussen uw bron en Experience Platform, met inbegrip van de verificatiereferenties van uw bron, de huidige status van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST-aanvraag naar het `/connections` -eindpunt en geeft u de [!DNL AWS Redshift] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```https
POST /connections
```

**Verzoek**

+++Selecteren om voorbeeld weer te geven

Met de volgende aanvraag wordt een basisverbinding voor [!DNL AWS Redshift] gemaakt:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
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
| --- | --- |
| `auth.params.server` | De servernaam van de instantie [!DNL AWS Redshift] . |
| `auth.params.port` | De TCP-poort die een [!DNL AWS Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL AWS Redshift] -account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met de gebruikersaccount. |
| `auth.params.database` | De [!DNL AWS Redshift] -database waaruit gegevens moeten worden opgehaald. |
| `connectionSpec.id` | De [!DNL AWS Redshift] connection specification ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Reactie**

+++Selecteren om voorbeeld weer te geven

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw gegevens te kunnen bekijken in de volgende zelfstudie.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## Verbinding maken [!DNL AWS Redshift] met Experience Platform op AWS Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Deze sectie is op implementaties van Experience Platform van toepassing die op de Diensten van het Web van AWS (AWS) lopen. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../../../landing/multi-cloud.md).

Lees de onderstaande stappen voor informatie over hoe u uw [!DNL AWS Redshift] -bron kunt verbinden met Experience Platform op AWS.

### Een basisverbinding maken voor [!DNL AWS Redshift] op Experience Platform op AWS {#aws-base}

**API formaat**

```http
POST /connections
```

**Verzoek**

Met de volgende aanvraag wordt een basisverbinding voor [!DNL AWS Redshift] gemaakt:

+++Selecteren om voorbeeld weer te geven

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auth.params.server` | De servernaam van de instantie [!DNL AWS Redshift] . |
| `auth.params.port` | De TCP-poort die een [!DNL AWS Redshift] -server gebruikt om te luisteren naar clientverbindingen. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL AWS Redshift] -account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat overeenkomt met de gebruikersaccount. |
| `auth.params.database` | De [!DNL AWS Redshift] -database waaruit gegevens moeten worden opgehaald. |
| `auth.params.schema` | De naam van het schema dat aan uw [!DNL AWS Redshift] database is gekoppeld. U moet ervoor zorgen dat de gebruiker u gegevensbestandtoegang tot wilt geven, ook toegang tot dit schema heeft. |
| `connectionSpec.id` | De [!DNL AWS Redshift] connection specification ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**Reactie**

Een succesvolle reactie keert details van de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw opslag te verkennen in de volgende zelfstudie.

+++Selecteren om voorbeeld weer te geven

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL AWS Redshift] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om gegevensbestandgegevens aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/database-nosql.md)
