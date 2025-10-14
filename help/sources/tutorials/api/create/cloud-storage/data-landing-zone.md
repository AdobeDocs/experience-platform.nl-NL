---
title: Gegevenslandingszone verbinden met Adobe Experience Platform met behulp van de Flow Service API
description: Leer hoe u Adobe Experience Platform verbindt met Data Landing Zone met behulp van de Flow Service API.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 1%

---

# Verbind [!DNL Data Landing Zone] met Adobe Experience Platform gebruikend de Dienst API van de Stroom

>[!IMPORTANT]
>
>Deze pagina is specifiek voor de [!DNL Data Landing Zone] *bron* schakelaar in Experience Platform. Voor informatie bij het verbinden met de [!DNL Data Landing Zone] *bestemmings* schakelaar, verwijs naar de [[!DNL Data Landing Zone]  pagina van de bestemmingsdocumentatie &#x200B;](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] is een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden die naar Adobe Experience Platform kunnen worden overgebracht. Gegevens worden automatisch na zeven dagen uit de [!DNL Data Landing Zone] verwijderd.

Dit leerprogramma begeleidt u door de stappen op hoe te om a [!DNL Data Landing Zone] bronverbinding tot stand te brengen gebruikend [[!DNL Flow Service]  API &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/). Deze zelfstudie bevat ook instructies voor het ophalen van [!DNL Data Landing Zone] en het weergeven en vernieuwen van uw referenties.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Dit leerprogramma vereist u ook om de gids te lezen over [&#x200B; begonnen wordt met Experience Platform APIs &#x200B;](../../../../../landing/api-guide.md) om te leren hoe te aan Experience Platform APIs voor authentiek te verklaren en de voorbeeldvraag te interpreteren die in de documentatie wordt verstrekt.

De volgende secties bevatten aanvullende informatie die u moet weten om een [!DNL Data Landing Zone] -bronverbinding met de [!DNL Flow Service] API te kunnen maken.

## Een bruikbare landingszone ophalen

>[!IMPORTANT]
>
>U moet de toegangsbeheermachtiging van **[!UICONTROL Manage Sources]** hebben om de [!DNL Data Landing Zone] API&#39;s te kunnen gebruiken en `type=user_drop_zone` op te halen. Voor meer informatie, lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](../../../../../access-control/home.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

De eerste stap bij het gebruik van API&#39;s voor toegang tot [!DNL Data Landing Zone] is het indienen van een GET-aanvraag voor het `/landingzone` eindpunt van de [!DNL Connectors] API terwijl `type=user_drop_zone` wordt opgegeven als onderdeel van de aanvraagheader.

**API formaat**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| Kopteksten | Beschrijving |
| --- | --- |
| `user_drop_zone` | Met het type `user_drop_zone` kan de API een landingszone-container onderscheiden van de andere typen containers die voor u beschikbaar zijn. |

**Verzoek**

Met het volgende verzoek wordt een bestaande landingszone opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Reactie**

Afhankelijk van uw leverancier retourneert een succesvol verzoek het volgende:

>[!BEGINTABS]

>[!TAB  Reactie op Azure ]

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `containerName` | De naam van de landingszone die u hebt opgehaald. |
| `containerTTL` | De vervaltijd (in dagen) die op uw gegevens binnen de landingszone wordt toegepast. Alle gegevens binnen een bepaalde landingszone worden na zeven dagen verwijderd. |


>[!TAB  Reactie op AWS ]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## [!DNL Data Landing Zone] gebruikersgegevens ophalen

Als u referenties voor een [!DNL Data Landing Zone] wilt ophalen, vraagt u GET het `/credentials` -eindpunt van de [!DNL Connectors] API aan.

**API formaat**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**Verzoek**

In het volgende aanvraagvoorbeeld worden de gegevens voor een bestaande landingszone opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Reactie**

Afhankelijk van uw leverancier retourneert een succesvol verzoek het volgende:

>[!BEGINTABS]

>[!TAB  Reactie op Azure ]

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `containerName` | De naam van de [!DNL Data Landing Zone] . |
| `SASToken` | Het token voor gedeelde toegangshandtekeningen voor uw [!DNL Data Landing Zone] . Deze tekenreeks bevat alle informatie die nodig is om een aanvraag te autoriseren. |
| `storageAccountName` | De naam van uw opslagaccount. |
| `SASUri` | De URI voor de gedeelde toegangshandtekening voor uw [!DNL Data Landing Zone] . Deze tekenreeks is een combinatie van de URI naar de [!DNL Data Landing Zone] waarnaar u wordt geverifieerd en de bijbehorende SAS-token. |
| `expiryDate` | De datum waarop uw SAS-token verloopt. U moet uw token vernieuwen vóór de vervaldatum om deze te kunnen blijven gebruiken in uw toepassing voor het uploaden van gegevens naar de [!DNL Data Landing Zone] . Als u uw token niet handmatig vernieuwt vóór de opgegeven vervaldatum, wordt deze automatisch vernieuwd en wordt er een nieuw token weergegeven wanneer de aanroep van de GET-gebruikersgegevens wordt uitgevoerd. |

>[!TAB  Reactie op AWS ]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `credentials.clientId` | De client-id van uw [!DNL Data Landing Zone] in AWS. |
| `credentials.awsAccessKeyId` | De toegangs belangrijkste identiteitskaart van uw [!DNL Data Landing Zone] in AWS. |
| `credentials.awsSecretAccessKey` | De geheime toegangssleutel van uw [!DNL Data Landing Zone] in AWS. |
| `credentials.awsSessionToken` | Uw AWS-sessietoken. |
| `dlzPath.bucketName` | De naam van je AWS emmertje. |
| `dlzPath.dlzFolder` | De map [!DNL Data Landing Zone] die u opent. |
| `dlzProvider` | De [!DNL Data Landing Zone] -provider die u gebruikt. Voor Amazon is dit [!DNL Amazon S3] . |
| `expiryTime` | De vervaltijd in unieke tijd. |

>[!ENDTABS]

### De vereiste velden ophalen met behulp van API&#39;s

Nadat u uw token hebt gegenereerd, kunt u de vereiste velden programmatisch ophalen aan de hand van de onderstaande aanvraagvoorbeelden:

>[!BEGINTABS]

>[!TAB  Python ]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB  Java ]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## [!DNL Data Landing Zone] gebruikersgegevens bijwerken

U kunt uw `SASToken` bijwerken door een POST-aanvraag in te dienen bij het `/credentials` eindpunt van de [!DNL Connectors] API.

**API formaat**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Kopteksten | Beschrijving |
| --- | --- |
| `user_drop_zone` | Met het type `user_drop_zone` kan de API een landingszone-container onderscheiden van de andere typen containers die voor u beschikbaar zijn. |
| `refresh` | Met de handeling `refresh` kunt u de gegevens van de landingszone opnieuw instellen en automatisch een nieuwe `SASToken` genereren. |

**Verzoek**

Met het volgende verzoek worden de gegevens van uw landingszone bijgewerkt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Reactie**

In het volgende antwoord worden bijgewerkte waarden voor de `SASToken` en `SASUri` geretourneerd.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## Bestandsstructuur en inhoud van landingszones verkennen

U kunt de bestandsstructuur en inhoud van de landingszone verkennen door een GET-aanvraag in te dienen bij het eindpunt `connectionSpecs` van de [!DNL Flow Service] API.

**API formaat**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parameter | Beschrijving |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Landing Zone] . Deze vaste id is: `26f526f2-58f4-4712-961d-e41bf1ccc0e8` . |

**Verzoek**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord retourneert een array met bestanden en mappen die in de gevraagde map zijn gevonden. Let op de eigenschap `path` van het bestand dat u wilt uploaden, aangezien u dit in de volgende stap moet opgeven om de structuur te controleren.

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

Om de structuur van een dossier in uw landingsstreek te inspecteren, voer een verzoek van GET terwijl het verstrekken van de weg van het dossier en type als vraagparameter uit.

**API formaat**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Landing Zone] . Deze vaste id is: `26f526f2-58f4-4712-961d-e41bf1ccc0e8` . |
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

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

### Gebruik `determineProperties` om automatisch informatie over de bestandseigenschappen van een [!DNL Data Landing Zone] te detecteren

Met de parameter `determineProperties` kunt u eigenschapinformatie van de bestandsinhoud van uw [!DNL Data Landing Zone] automatisch detecteren wanneer u een GET-aanroep maakt om de inhoud en structuur van uw bron te verkennen.

#### `determineProperties` gebruikt hoofdletters/kleine letters

In de volgende tabel worden verschillende scenario&#39;s beschreven die u kunt tegenkomen wanneer u de query-parameter `determineProperties` gebruikt of handmatig informatie over het bestand opgeeft.

| `determineProperties` | `queryParams` | Antwoord |
| --- | --- | --- |
| Waar | N.v.t. | Als `determineProperties` wordt verstrekt als vraagparameter, dan komt de dossiereigenschappen opsporing voor en de reactie keert een nieuwe `properties` sleutel terug die informatie over dossiertype, compressietype, en kolomscheidingsteken omvat. |
| N.v.t. | Waar | Als de waarden voor bestandstype, compressietype en kolomscheidingsteken handmatig worden opgegeven als onderdeel van `queryParams` , worden deze gebruikt om het schema te genereren en worden dezelfde eigenschappen geretourneerd als onderdeel van het antwoord. |
| Waar | Waar | Als beide opties gelijktijdig worden uitgevoerd, wordt een fout geretourneerd. |
| N.v.t. | N.v.t. | Als geen van beide opties wordt opgegeven, wordt een fout geretourneerd omdat er geen manier is om eigenschappen voor de reactie op te halen. |

**API formaat**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parameter | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `determineProperties` | Met deze queryparameter kan de [!DNL Flow Service] -API informatie detecteren over de eigenschappen van het bestand, zoals informatie over het bestandstype, het compressietype en het kolomscheidingsteken. | `true` |

**Verzoek**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord retourneert de structuur van het bestand waarop de vraag betrekking heeft, inclusief bestandsnamen en gegevenstypen, en ook een `properties` -sleutel met informatie over `fileType` , `compressionType` en `columnDelimiter` .

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
| `properties.fileType` | Het corresponderende bestandstype van het bestand waarnaar wordt gevraagd. De ondersteunde bestandstypen zijn: `delimited` , `json` en `parquet` . |
| `properties.compressionType` | Het corresponderende compressietype dat wordt gebruikt voor het bestand waarnaar wordt gevraagd. De ondersteunde compressietypen zijn: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Het corresponderende kolomscheidingsteken dat wordt gebruikt voor het bestand waarnaar wordt gevraagd. Elke waarde van één teken is een toegestaan kolomscheidingsteken. De standaardwaarde is een komma `(,)` . |


## Een bronverbinding maken

Een bronverbinding maakt en beheert de verbinding met de externe bron vanwaar gegevens worden ingevoerd. Een bronverbinding bestaat uit informatie zoals gegevensbron, gegevensformaat, en bron identiteitskaart nodig om een gegevensstroom tot stand te brengen. Een bronverbindingsinstantie is specifiek voor een huurder en organisatie.

Als u een bronverbinding wilt maken, vraagt u een POST-aanvraag naar het `/sourceConnections` -eindpunt van de [!DNL Flow Service] API.


**API formaat**

```http
POST /sourceConnections
```

**Verzoek**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `data.format` | De indeling van de gegevens die u naar Experience Platform wilt verzenden. |
| `params.path` | Het pad naar het bestand dat u naar Experience Platform wilt brengen. |
| `connectionSpec.id` | De verbindingsspecificatie-id die overeenkomt met [!DNL Data Landing Zone] . Deze vaste id is: `26f526f2-58f4-4712-961d-e41bf1ccc0e8` . |

**Reactie**

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug. Deze id is vereist in de volgende zelfstudie om een gegevensstroom te maken.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Volgende stappen

Aan de hand van deze zelfstudie hebt u uw [!DNL Data Landing Zone] -gegevens opgehaald, de bestandsstructuur onderzocht om het bestand te zoeken dat u naar Experience Platform wilt verzenden, en een bronverbinding gemaakt om uw gegevens naar Experience Platform te verzenden. U kunt nu aan het volgende leerprogramma te werk gaan, waar u zult leren hoe te [&#x200B; een dataflow creëren om de gegevens van de wolkenopslag aan Experience Platform te brengen gebruikend  [!DNL Flow Service]  API &#x200B;](../../collect/cloud-storage.md).
