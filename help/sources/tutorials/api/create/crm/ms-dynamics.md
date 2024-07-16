---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Een Microsoft Dynamics Base Connection maken met de Flow Service API
type: Tutorial
description: Leer hoe u Platform kunt verbinden met een Microsoft Dynamics-account met behulp van de Flow Service API.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Een [!DNL Microsoft Dynamics] basisverbinding maken met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding voor [!DNL Microsoft Dynamics] tot stand te brengen (verder die als &quot; [!DNL Dynamics] wordt bedoeld&quot;) gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om Platform met een Dynamics-account te kunnen verbinden met de [!DNL Flow Service] API.

### Vereiste referenties verzamelen

[!DNL Flow Service] kan alleen verbinding maken met [!DNL Dynamics] als u waarden opgeeft voor de volgende verbindingseigenschappen:

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] -instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] -gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] -account. |

>[!TAB  dienst-hoofd en zeer belangrijke authentificatie ]

| Credentials | Beschrijving |
| --- | --- |
| `servicePrincipalId` | De client-id van uw [!DNL Dynamics] -account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

>[!ENDTABS]

Voor meer informatie bij het worden begonnen, verwijs naar [ dit  [!DNL Dynamics]  document ](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Platform APIs ](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL Dynamics] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Dynamics] -verificatiegegevens op als onderdeel van de aanvraagparameters.

### Een [!DNL Dynamics] basisverbinding maken

>[!TIP]
>
>Nadat u een [!DNL Dynamics] basisverbinding hebt gemaakt, kunt u het verificatietype niet wijzigen. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

De eerste stap bij het maken van een bronverbinding is het verifiëren van de [!DNL Dynamics] -bron en het genereren van een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Als u een basis-verbindings-id wilt maken, vraagt u een POST naar het `/connections` -eindpunt en geeft u de [!DNL Dynamics] -verificatiegegevens op als onderdeel van de aanvraagparameters.

**API formaat**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Als u een [!DNL Dynamics] -basisverbinding wilt maken met behulp van basisverificatie, vraagt u een POST naar de [!DNL Flow Service] API en geeft u waarden op voor de `serviceUri` , `username` en `password` van de verbinding.

+++verzoek

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.serviceUri` | De service-URI die aan uw [!DNL Dynamics] -instantie is gekoppeld. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Dynamics] -account is gekoppeld. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Dynamics] account is gekoppeld. |
| `connectionSpec.id` | De [!DNL Dynamics] connection specification ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Response

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB  de dienst belangrijkste op sleutel-gebaseerde authentificatie ]

Als u een [!DNL Dynamics] -basisverbinding wilt maken met behulp van service principal key-verificatie, vraagt u een POST naar de [!DNL Flow Service] API en geeft u waarden op voor de `serviceUri` , `servicePrincipalId` en `servicePrincipalKey` van uw verbinding.

+++verzoek

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `auth.params.serviceUri` | De service-URI die aan uw [!DNL Dynamics] -instantie is gekoppeld. |
| `auth.params.servicePrincipalId` | De client-id van uw [!DNL Dynamics] -account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `auth.params.servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |
| `connectionSpec.id` | De [!DNL Dynamics] connection specification ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Response

Een succesvolle reactie keert de pas gecreëerde verbinding, met inbegrip van zijn uniek herkenningsteken (`id`) terug. Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Microsoft Dynamics] basisverbinding gemaakt met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Onderzoek de structuur en de inhoud van uw gegevenslijsten gebruikend  [!DNL Flow Service]  API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van CRM aan Platform te brengen gebruikend  [!DNL Flow Service]  API](../../collect/crm.md)
