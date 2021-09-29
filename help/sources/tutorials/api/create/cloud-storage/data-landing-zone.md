---
keywords: Experience Platform;thuis;populaire onderwerpen;
solution: Experience Platform
title: Gegevenslandingszone verbinden met Adobe Experience Platform met behulp van de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met Data Landing Zone met behulp van de Flow Service API.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 1%

---

# [!DNL Data Landing Zone] verbinden met Adobe Experience Platform met behulp van de Flow Service API

[!DNL Data Landing Zone] is een op cloud gebaseerde gegevensopslagfaciliteit voor tijdelijke opslag van bestanden die bij Adobe Experience Platform wordt geleverd. [!DNL Data Landing Zone] wordt alleen gebruikt voor het in- en uitstappen van gegevens in en uit het Platform. Gegevens worden na zeven dagen automatisch verwijderd uit [!DNL Data Landing Zone].

In deze zelfstudie worden de stappen beschreven voor het maken van een [!DNL Data Landing Zone]-bronverbinding met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Deze zelfstudie bevat ook instructies voor het ophalen van uw [!DNL Data Landing Zone] en het weergeven en vernieuwen van uw referenties.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties bevatten aanvullende informatie die u moet weten om een [!DNL Data Landing Zone]-bronverbinding met de [!DNL Flow Service]-API te kunnen maken.

Deze zelfstudie vereist ook dat u de gids [Aan de slag met Platform APIs](../../../../../landing/api-guide.md) leest om te leren hoe te aan Platform APIs voor authentiek te verklaren en de voorbeeldvraag te interpreteren die in de documentatie wordt verstrekt.

## Een bruikbare landingszone ophalen

De eerste stap bij het gebruiken van APIs om tot [!DNL Data Landing Zone] toegang te hebben is een verzoek van de GET aan het `/landingzone` eindpunt van [!DNL Connectors] API terwijl het verstrekken van `type=user_drop_zone` als deel van uw verzoekkopbal.

**API-indeling**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Kopteksten | Beschrijving |
| --- | --- |
| `user_drop_zone` | Met het type `user_drop_zone` kan de API een landingszonecontainer onderscheiden van de andere typen containers die voor u beschikbaar zijn. |

**Verzoek**

Met het volgende verzoek wordt een bestaande landingszone opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Antwoord**

De volgende reactie retourneert informatie over een landingszone, inclusief de corresponderende `containerName` en `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `containerName` | De naam van de landingszone die u hebt opgehaald. |
| `containerTTL` | De time-to-live-instelling die wordt toegepast op uw gegevens in de landingszone. Alle gegevens binnen een bepaalde landingszone worden na zeven dagen verwijderd. |

## [!DNL Data Landing Zone] referenties ophalen

Om geloofsbrieven voor een [!DNL Data Landing Zone] terug te winnen, doe een verzoek van de GET aan het `/credentials` eindpunt van [!DNL Connectors] API.

**API-indeling**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**Verzoek**

In het volgende aanvraagvoorbeeld worden de gegevens voor een bestaande landingszone opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwoord**

De volgende reactie retourneert de referentie-informatie voor uw landingszone, inclusief uw huidige `SASToken` en `SASUri`, evenals de `storageAccountName` die correspondeert met uw landingszonecontainer.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `containerName` | De naam van uw landingszone. |
| `SASToken` | Het token voor gedeelde toegangshandtekeningen voor uw landingszone. Deze tekenreeks bevat alle informatie die nodig is om een aanvraag te autoriseren. |
| `SASUri` | De URI van de gedeelde toegangshandtekening voor uw landingszone. Deze tekenreeks is een combinatie van de URI naar de landingszone waarvoor u geauthenticeerd wordt en de bijbehorende SAS-token, |


## Referenties [!DNL Data Landing Zone] bijwerken

U kunt uw `SASToken` bijwerken door een verzoek van de POST aan het `/credentials` eindpunt van [!DNL Connectors] API te doen.

**API-indeling**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Kopteksten | Beschrijving |
| --- | --- |
| `user_drop_zone` | Met het type `user_drop_zone` kan de API een landingszonecontainer onderscheiden van de andere typen containers die voor u beschikbaar zijn. |
| `refresh` | Met de handeling `refresh` kunt u de gegevens van uw landingszone opnieuw instellen en automatisch een nieuwe `SASToken` genereren. |

**Verzoek**

Met het volgende verzoek worden de gegevens van uw landingszone bijgewerkt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Antwoord**

De volgende reactie keert bijgewerkte waarden voor uw `SASToken` en `SASUri` terug.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Bestandsstructuur en inhoud van landingszones verkennen

U kunt de bestandsstructuur en inhoud van uw landingszone verkennen door een GET-aanvraag in te dienen bij het `connectionSpecs`-eindpunt van de [!DNL Flow Service]-API.

**API-indeling**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Landing Zone]. Deze vaste ID is: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert een array met bestanden en mappen die in de gevraagde map zijn gevonden. Neem nota van het `path` bezit van het dossier u wenst te uploaden, aangezien u het in de volgende stap moet verstrekken om zijn structuur te inspecteren.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## Bestandsstructuur en inhoud van landingszone voorvertonen

Om de structuur van een dossier in uw landende streek te inspecteren, voer een verzoek van de GET uit terwijl het verstrekken van de weg van het dossier en type als vraagparameter.

**API-indeling**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Landing Zone]. Deze vaste ID is: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Het type object waartoe u toegang wilt hebben. | `file` |
| `{OBJECT}` | Het pad en de naam van het object waartoe u toegang wilt hebben. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Het type bestand. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Een Booleaanse waarde die definieert of de voorvertoning van het bestand wordt ondersteund. | </ul><li>`true`</li><li>`false`</li></ul> |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord geeft de structuur van het gevraagde dossier met inbegrip van lijstnamen en gegevenstypes terug.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

## Een bronverbinding maken

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en bron identiteitskaart nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie IMS.

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan het `/sourceConnections` eindpunt van [!DNL Flow Service] API.


**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van uw [!DNL Data Landing Zone] bronverbinding. |
| `data.format` | De indeling van de gegevens die u naar het Platform wilt verzenden. |
| `params.path` | Het pad naar het bestand dat u naar het Platform wilt brengen. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Landing Zone]. Deze vaste ID is: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Antwoord**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u uw [!DNL Data Landing Zone] geloofsbrieven teruggewonnen, zijn dossierstructuur onderzocht om het dossier te vinden u aan Platform wenst over te brengen, en creeerde een bronverbinding beginnen uw gegevens aan Platform te brengen. U kunt nu verdergaan naar de volgende zelfstudie, waar u leert hoe u [een gegevensstroom kunt maken om gegevens voor cloudopslag naar het Platform te brengen met behulp van de  [!DNL Flow Service] API](../../collect/cloud-storage.md).
