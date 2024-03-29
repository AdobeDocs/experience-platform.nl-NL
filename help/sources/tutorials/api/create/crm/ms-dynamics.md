---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Een Microsoft Dynamics Base Connection maken met de Flow Service API
type: Tutorial
description: Leer hoe u Platform kunt verbinden met een Microsoft Dynamics-account met behulp van de Flow Service API.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# Een [!DNL Microsoft Dynamics] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Microsoft Dynamics] (hierna &quot;[!DNL Dynamics]&quot;) gebruiken [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de platformservices.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één platforminstantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om Platform met een rekening van de Dynamiek met succes te verbinden gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] verbinding maken met [!DNL Dynamics]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

>[!BEGINTABS]

>[!TAB Basisverificatie]

| Credentials | Beschrijving |
| --- | --- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] -instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] account. |

>[!TAB Service-principal en sleutelverificatie]

| Credentials | Beschrijving |
| --- | --- |
| `servicePrincipalId` | De client-id van uw [!DNL Dynamics] account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |

>[!ENDTABS]

Raadpleeg voor meer informatie over aan de slag gaan [dit [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Platform-API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Platform APIs met succes te maken, zie de gids op [aan de slag met platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

>[!TIP]
>
>Nadat u een verificatietype hebt gemaakt, kunt u dit type van een [!DNL Dynamics] basisverbinding. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL Dynamics] verificatiereferenties als onderdeel van de aanvraagparameters.

### Een [!DNL Dynamics] basisverbinding

>[!TIP]
>
>Nadat u een verificatietype hebt gemaakt, kunt u dit type van een [!DNL Dynamics] basisverbinding. Als u het verificatietype wilt wijzigen, moet u een nieuwe basisverbinding maken.

De eerste stap bij het maken van een bronverbinding is het verifiëren van uw [!DNL Dynamics] bron en genereer een basis-verbindings-id. Met een basis-verbindings-id kunt u bestanden verkennen en door de bestanden navigeren vanuit de bron en specifieke items identificeren die u wilt invoeren, zoals informatie over de gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` als u uw [!DNL Dynamics] verificatiereferenties als onderdeel van de aanvraagparameters.

**API-indeling**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Basisverificatie]

Een [!DNL Dynamics] basisverbinding die basisauthentificatie gebruikt, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van waarden voor uw verbinding `serviceUri`, `username`, en `password`.

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
| `auth.params.serviceUri` | De service-URI die aan uw [!DNL Dynamics] -instantie. |
| `auth.params.username` | De gebruikersnaam die aan uw [!DNL Dynamics] account. |
| `auth.params.password` | Het wachtwoord dat aan uw [!DNL Dynamics] account. |
| `connectionSpec.id` | De [!DNL Dynamics] Verbindingsspecificatie-id: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Response

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke id (`id`). Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB De belangrijkste op sleutel-gebaseerde authentificatie van de dienst]

Een [!DNL Dynamics] basisverbinding die de dienst belangrijkste op sleutel-gebaseerde authentificatie gebruikt, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van waarden voor uw verbinding `serviceUri`, `servicePrincipalId`, en `servicePrincipalKey`.

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
| `auth.params.serviceUri` | De service-URI die aan uw [!DNL Dynamics] -instantie. |
| `auth.params.servicePrincipalId` | De client-id van uw [!DNL Dynamics] account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `auth.params.servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |
| `connectionSpec.id` | De [!DNL Dynamics] Verbindingsspecificatie-id: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Response

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke id (`id`). Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Microsoft Dynamics] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Maak een gegevensstroom om CRM-gegevens naar het platform te brengen met behulp van de [!DNL Flow Service] API](../../collect/crm.md)
