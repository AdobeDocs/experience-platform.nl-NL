---
keywords: Experience Platform;thuis;populaire onderwerpen;
solution: Experience Platform
title: Gegevenslandingszone verbinden met Adobe Experience Platform met behulp van de Flow Service API
topic-legacy: overview
type: Tutorial
description: Leer hoe u Adobe Experience Platform verbindt met Data Landing Zone met behulp van de Flow Service API.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 5829b50a81741cc4883dfa8f4d7d7891b791caf5
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 1%

---

# Verbinden [!DNL Data Landing Zone] naar Adobe Experience Platform met behulp van de Flow Service API

[!DNL Data Landing Zone] is een op cloud gebaseerde gegevensopslagfaciliteit voor tijdelijke opslag van bestanden die bij Adobe Experience Platform wordt geleverd. Gegevens worden automatisch verwijderd uit de [!DNL Data Landing Zone] na zeven dagen.

Deze zelfstudie begeleidt u door de stappen voor het maken van een [!DNL Data Landing Zone] bronverbinding met de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Deze zelfstudie bevat ook instructies voor het ophalen van uw [!DNL Data Landing Zone], en uw referenties bekijken en vernieuwen.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Experience Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

In de volgende secties vindt u aanvullende informatie die u nodig hebt om een [!DNL Data Landing Zone] bronverbinding met de [!DNL Flow Service] API.

Voor deze zelfstudie moet u ook de handleiding lezen [aan de slag met Platform-API&#39;s](../../../../../landing/api-guide.md) leren hoe te om aan Platform APIs voor authentiek te verklaren en de voorbeeldvraag te interpreteren die in de documentatie wordt verstrekt.

## Een bruikbare landingszone ophalen

De eerste stap bij het gebruik van API&#39;s voor toegang [!DNL Data Landing Zone] moet een verzoek van de GET indienen bij de `/landingzone` van het [!DNL Connectors] API tijdens `type=user_drop_zone` als deel van uw verzoekkopbal.

**API-indeling**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Kopteksten | Beschrijving |
| --- | --- |
| `user_drop_zone` | De `user_drop_zone` Met type kan de API een landingszone-container onderscheiden van de andere typen containers die voor u beschikbaar zijn. |

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

De volgende reactie geeft informatie over een landingszone, inclusief de bijbehorende `containerName` en `containerTTL`.

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

## Ophalen [!DNL Data Landing Zone] geloofsbrieven

Om geloofsbrieven voor een terug te winnen [!DNL Data Landing Zone]een verzoek tot GET aan de `/credentials` van het [!DNL Connectors] API.

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

De volgende reactie retourneert de referentie-informatie voor uw landingszone, inclusief uw huidige `SASToken` en `SASUri`en de `storageAccountName` die overeenkomt met uw landingszonecontainer.

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


## Bijwerken [!DNL Data Landing Zone] geloofsbrieven

U kunt uw `SASToken` door een POST aan de `/credentials` van het [!DNL Connectors] API.

**API-indeling**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Kopteksten | Beschrijving |
| --- | --- |
| `user_drop_zone` | De `user_drop_zone` Met type kan de API een landingszone-container onderscheiden van de andere typen containers die voor u beschikbaar zijn. |
| `refresh` | De `refresh` actie staat u toe om uw landingszonegeloofsbrieven terug te stellen en automatisch een nieuwe te produceren `SASToken`. |

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

In het volgende antwoord worden bijgewerkte waarden voor uw `SASToken` en `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Bestandsstructuur en inhoud van landingszones verkennen

U kunt de bestandsstructuur en inhoud van de landingszone verkennen door een GET-verzoek in te dienen bij de `connectionSpecs` van het [!DNL Flow Service] API.

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

Een succesvol antwoord retourneert een array met bestanden en mappen die in de gevraagde map zijn gevonden. De `path` eigenschap van het bestand dat u wilt uploaden, omdat u dit in de volgende stap moet opgeven om de structuur te controleren.

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
| `{PREVIEW}` | Een Booleaanse waarde die aangeeft of de voorvertoning van het bestand wordt ondersteund. | </ul><li>`true`</li><li>`false`</li></ul> |

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

Een succesvol antwoord geeft de structuur van het gevraagde bestand, inclusief bestandsnamen en gegevenstypen.

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

### Gebruiken `determineProperties` om automatisch informatie over de bestandseigenschappen van een [!DNL Data Landing Zone]

U kunt de `determineProperties` parameter om eigenschapinformatie van de bestandsinhoud van uw [!DNL Data Landing Zone] wanneer het maken van een vraag van de GET om de inhoud en de structuur van uw bron te onderzoeken.

#### `determineProperties` Gebruikt gevallen

In de volgende tabel worden verschillende scenario&#39;s beschreven die u kunt tegenkomen bij het gebruik van de `determineProperties` de parameter van de vraag of manueel het verstrekken van informatie over uw dossier.

| `determineProperties` | `queryParams` | Antwoord |
| --- | --- | --- |
| Waar | N.v.t. | Indien `determineProperties` wordt verstrekt als vraagparameter, dan komt de dossiereigenschappen opsporing voor en de reactie keert een nieuw terug `properties` sleutel die informatie over dossiertype, compressietype, en kolomscheidingsteken omvat. |
| N.v.t. | Waar | Als de waarden voor bestandstype, compressietype en kolomscheidingsteken handmatig worden opgegeven als onderdeel van `queryParams`, dan worden zij gebruikt om het schema te produceren en de zelfde eigenschappen zijn teruggekeerd als deel van de reactie. |
| Waar | Waar | Als beide opties gelijktijdig worden uitgevoerd, wordt een fout geretourneerd. |
| N.v.t. | N.v.t. | Als geen van beide opties wordt opgegeven, wordt een fout geretourneerd omdat er geen manier is om eigenschappen voor de reactie op te halen. |

**API-indeling**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `determineProperties` | Met deze queryparameter kan de [!DNL Flow Service] API om informatie over de eigenschappen van uw dossier, met inbegrip van informatie over dossiertype, compressietype, en kolomscheidingsteken te ontdekken. | `true` |

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord retourneert de structuur van het bestand waarop de vraag betrekking heeft, inclusief bestandsnamen en gegevenstypen, en ook een `properties` sleutel, met informatie over `fileType`, `compressionType`, en `columnDelimiter`.

+++klik op mij

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| Eigenschap | Beschrijving |
| --- | --- |
| `properties.fileType` | Het corresponderende bestandstype van het bestand waarnaar wordt gevraagd. De ondersteunde bestandstypen zijn: `delimited`, `json`, en `parquet`. |
| `properties.compressionType` | Het corresponderende compressietype dat wordt gebruikt voor het bestand waarnaar wordt gevraagd. De ondersteunde compressietypen zijn: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Het corresponderende kolomscheidingsteken dat wordt gebruikt voor het bestand waarnaar wordt gevraagd. Elke waarde van één teken is een toegestaan kolomscheidingsteken. De standaardwaarde is een komma `(,)`. |


## Een bronverbinding maken

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en bron identiteitskaart nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie IMS.

Om een bronverbinding tot stand te brengen, doe een verzoek van de POST aan `/sourceConnections` van het [!DNL Flow Service] API.


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

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u uw [!DNL Data Landing Zone] referenties, verkende zijn dossierstructuur om het dossier te vinden u aan het Platform wenst over te brengen, en creeerde een bronverbinding beginnen uw gegevens aan Platform te brengen. U kunt nu verdergaan met de volgende zelfstudie, waarin u leert hoe u [een gegevensstroom maken om gegevens voor cloudopslag naar het Platform te brengen met de [!DNL Flow Service] API](../../collect/cloud-storage.md).
