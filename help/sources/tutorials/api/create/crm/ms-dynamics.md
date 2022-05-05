---
keywords: Experience Platform;home;populaire onderwerpen;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Een Microsoft Dynamics Base Connection maken met de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Platform met behulp van de Flow Service API kunt verbinden met een Microsoft Dynamics-account.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Een [!DNL Microsoft Dynamics] basisverbinding met de [!DNL Flow Service] API

Een basisverbinding vertegenwoordigt de geverifieerde verbinding tussen een bron en Adobe Experience Platform.

Dit leerprogramma begeleidt u door de stappen om een basisverbinding tot stand te brengen voor [!DNL Microsoft Dynamics] (hierna &quot;[!DNL Dynamics]&quot;) het gebruik van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om Platform met een rekening van de Dynamiek met succes te verbinden gebruikend [!DNL Flow Service] API.

### Vereiste referenties verzamelen

Om [!DNL Flow Service] om verbinding te maken met [!DNL Dynamics]moet u waarden opgeven voor de volgende eigenschappen van de verbinding:

| Credentials | Beschrijving |
| ---------- | ----------- |
| `serviceUri` | De service-URL van uw [!DNL Dynamics] -instantie. |
| `username` | De gebruikersnaam voor uw [!DNL Dynamics] gebruikersaccount. |
| `password` | Het wachtwoord voor uw [!DNL Dynamics] account. |
| `servicePrincipalId` | De client-id van uw [!DNL Dynamics] account. Deze ID wordt vereist wanneer het gebruiken van de dienst hoofd en op sleutel-gebaseerde authentificatie. |
| `servicePrincipalKey` | De geheime sleutel van de dienst belangrijkste geheim. Deze referentie wordt vereist wanneer het gebruiken van de dienst belangrijkste en op sleutel-gebaseerde authentificatie. |
| `connectionSpec.id` | De verbindingsspecificatie keert de eigenschappen van de bronschakelaar, met inbegrip van authentificatiespecificaties met betrekking tot het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Dynamics] is: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Ga voor meer informatie over aan de slag gaan [dit [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md).

## Een basisverbinding maken

Een basisverbinding behoudt informatie tussen uw bron en Platform, met inbegrip van de de authentificatiegeloofsbrieven van uw bron, de huidige staat van de verbinding, en uw unieke identiteitskaart van de basisverbinding. Met de ID van de basisverbinding kunt u bestanden verkennen en door bestanden navigeren vanuit uw bron en kunt u de specifieke items identificeren die u wilt opnemen, inclusief informatie over hun gegevenstypen en indelingen.

Om een identiteitskaart van de basisverbinding te creëren, doe een verzoek van de POST aan `/connections` eindpunt terwijl het verstrekken van uw [!DNL Dynamics] verificatiereferenties als onderdeel van de aanvraagparameters.

### Een [!DNL Dynamics] basisverbinding met basisverificatie

Als u een [!DNL Dynamics] basisverbinding die basisauthentificatie gebruikt, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van waarden voor uw verbinding `serviceUri`, `username`, en `password`.

**API-indeling**

```http
POST /connections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke id (`id`). Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Een [!DNL Dynamics] basisverbinding die de dienst belangrijkste op sleutel-gebaseerde authentificatie gebruikt

Als u een [!DNL Dynamics] basisverbinding die de dienst belangrijkste op sleutel-gebaseerde authentificatie gebruikt, doe een verzoek van de POST aan [!DNL Flow Service] API terwijl het verstrekken van waarden voor uw verbinding `serviceUri`, `servicePrincipalId`, en `servicePrincipalKey`.

**API-indeling**

```http
POST /connections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Antwoord**

Met een geslaagde reactie wordt de nieuwe verbinding geretourneerd, inclusief de unieke id (`id`). Deze id is vereist om uw CRM-systeem in de volgende stap te verkennen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een [!DNL Microsoft Dynamics] basisverbinding met de [!DNL Flow Service] API. U kunt deze basis verbindings-id in de volgende zelfstudies gebruiken:

* [Ontdek de structuur en inhoud van uw gegevenslijsten gebruikend [!DNL Flow Service] API](../../explore/tabular.md)
* [Creeer een dataflow om de gegevens van CRM aan Platform te brengen gebruikend [!DNL Flow Service] API](../../collect/crm.md)
