---
title: Data Landing Zone Source
description: Leer hoe u Data Landing Zone kunt verbinden met Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Deze pagina is specifiek voor de [!DNL Data Landing Zone] *bron* schakelaar in Experience Platform. Voor informatie bij het verbinden met de [!DNL Data Landing Zone] *bestemmings* schakelaar, verwijs naar de [[!DNL Data Landing Zone]  pagina van de bestemmingsdocumentatie &#x200B;](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht en waarmee u toegang hebt tot een veilige, op de cloud gebaseerde opslagfaciliteit voor bestanden om bestanden naar Experience Platform te brengen. U hebt toegang tot één [!DNL Data Landing Zone] container per sandbox en het totale gegevensvolume voor alle containers is beperkt tot de totale gegevens die worden geleverd bij uw Experience Platform-licentie voor producten en services. Alle klanten van Experience Platform beschikken over één [!DNL Data Landing Zone] -container per sandbox. U kunt bestanden lezen en schrijven naar uw container via [!DNL Azure Storage Explorer] of de opdrachtregelinterface.

[!DNL Data Landing Zone] biedt ondersteuning voor verificatie op basis van SAS en de bijbehorende gegevens zijn in rust en onderweg beveiligd met standaard [!DNL Azure Blob] -opslagbeveiligingsmechanismen. Met verificatie op basis van SAS hebt u via een openbare internetverbinding veilig toegang tot uw [!DNL Data Landing Zone] -container. Er zijn geen netwerkwijzigingen vereist voor toegang tot uw [!DNL Data Landing Zone] -container. Dit betekent dat u geen lijsten van gewenste personen of instellingen voor meerdere regio&#39;s voor uw netwerk hoeft te configureren. Experience Platform past een strikte vervaltijd van zeven dagen toe op alle bestanden en mappen die naar een [!DNL Data Landing Zone] -container zijn geüpload. Alle bestanden en mappen worden na zeven dagen verwijderd.

## Stel uw [!DNL Data Landing Zone] source in voor Experience Platform on Azure {#azure}

Volg de onderstaande stappen om te leren hoe u uw [!DNL Data Landing Zone] -account voor Experience Platform on Azure kunt instellen.

>[!NOTE]
>
>Als u [!DNL Data Landing Zone] van [!DNL Azure Data Factory] wilt toegang hebben, dan moet u de verbonden dienst voor [!DNL Data Landing Zone] tot stand brengen gebruikend de [&#x200B; SAS geloofsbrieven &#x200B;](../../tutorials/ui/create/cloud-storage/data-landing-zone.md#retrieve-your-data-landing-zone-credentials) die door Experience Platform worden verstrekt. Nadat u de gekoppelde service hebt gemaakt, kunt u de [!DNL Data Landing Zone] verkennen door het containerpad te selecteren in plaats van het standaardhoofdpad.

### Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden bij het benoemen van bestanden of mappen voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (zoals `0x00` tot en met `0x1F` , `\u0081` enzovoort), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [&#x200B; RFC 2616, Sectie 2.2: BasisRegels &#x200B;](https://www.ietf.org/rfc/rfc2616.txt) en [&#x200B; RFC 3987 &#x200B;](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

### De inhoud van uw gegevenslandingszone beheren{#manage-the-contents-of-your-data-landing-zone}

U kunt [[!DNL Azure Storage Explorer] gebruiken &#x200B;](https://azure.microsoft.com/en-us/features/storage-explorer/) om de inhoud van uw [!DNL Data Landing Zone] container te beheren.

Selecteer in de gebruikersinterface van [!DNL Azure Storage Explorer] het verbindingspictogram in de linkernavigatie. Het **Uitgezochte venster van het Middel** verschijnt, die u van opties voorzien om met te verbinden. Selecteer **[!DNL Blob container]** om verbinding te maken met [!DNL Data Landing Zone] .

![&#x200B; de uitgezochte middelwerkruimte op Azure Explorer.](../../images/tutorials/create/dlz/select-resource.png)

Daarna, selecteer **Gedeelde toegangshandtekening URL (SAS)** als uw verbindingsmethode, en selecteer dan **daarna**.

![&#x200B; de uitgezochte verbindingsmethode op Azure Explorer, met gedeelde geselecteerde toegangshandtekening.](../../images/tutorials/create/dlz/select-connection-method.png)

Na het selecteren van uw verbindingsmethode, moet u a **vertoningsnaam** en **[!DNL Blob]container SAS URL** daarna verstrekken die met uw [!DNL Data Landing Zone] container beantwoordt.

>[!TIP]
>
>U kunt uw [!DNL Data Landing Zone] -referenties ophalen uit de broncatalogus in de gebruikersinterface van Experience Platform.

Verstrek uw [!DNL Data Landing Zone] SAS URL en selecteer dan **daarna**

![&#x200B; gaat de werkruimte van verbindingsinfo op Azure Explorer in waar de vertoningsnaam en SAS URL worden ingevoerd.](../../images/tutorials/create/dlz/enter-connection-info.png)

Het **Summiere** venster verschijnt, die u van een overzicht van uw montages, met inbegrip van informatie over uw [!DNL Blob] eindpunt en toestemmingen voorzien. Wanneer klaar, uitgezochte **verbindt**.

![&#x200B; de Azure summiere werkruimte van de Ontdekkingsreiziger die de montages van uw middelverbinding opnieuw overlapt.](../../images/tutorials/create/dlz/summary.png)

Een geslaagde verbinding werkt de gebruikersinterface van [!DNL Azure Storage Explorer] bij met uw [!DNL Data Landing Zone] -container.

![&#x200B; de gegevens landende de navigatiewerkruimte van de streek op Azure Explorer.](../../images/tutorials/create/dlz/dlz-user-container.png)

Als de [!DNL Data Landing Zone] -container is aangesloten op [!DNL Azure Storage Explorer] , kunt u nu bestanden uploaden naar de [!DNL Data Landing Zone] -container. Om te uploaden, **te selecteren uploadt** en dan **selecteert uploadt Dossiers**.

![&#x200B; uploadt de werkruimte van dossiers van Azure Explorer.](../../images/tutorials/create/dlz/upload.png)

Wanneer u het bestand hebt geselecteerd dat u wilt uploaden, moet u vervolgens het [!DNL Blob] type identificeren dat u het wilt uploaden als en de gewenste doelmap. Wanneer gebeëindigd, uitgezochte **uploadt**.

| [!DNL Blob] typen | Beschrijving |
| --- | --- |
| Blok [!DNL Blob] | Blok [!DNL Blobs] is geoptimaliseerd voor het efficiënt uploaden van grote hoeveelheden gegevens. Blok [!DNL Blobs] is de standaardoptie voor [!DNL Data Landing Zone] . |
| Toevoegen [!DNL Blob] | Toevoegen [!DNL Blobs] is geoptimaliseerd voor het toevoegen van gegevens aan het einde van het bestand. |

![&#x200B; uploadt het venster van dossiers van Azure Explorer waar de geselecteerde dossiers, het type van Blob, en bestemmingscategorie worden getoond.](../../images/tutorials/create/dlz/upload-files.png)

### Bestanden uploaden naar de [!DNL Data Landing Zone] via de opdrachtregelinterface

U kunt ook de opdrachtregelinterface van uw apparaat gebruiken en bestanden uploaden naar uw [!DNL Data Landing Zone] .

### Een bestand uploaden met Bash

In het volgende voorbeeld worden Bash en cURL gebruikt om een bestand te uploaden naar een [!DNL Data Landing Zone] met de [!DNL Azure Blob Storage] REST API:

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### Een bestand uploaden met Python

In het volgende voorbeeld wordt [!DNL Microsoft's] Python v12 SDK gebruikt om een bestand te uploaden naar een [!DNL Data Landing Zone] :

>[!TIP]
>
>In het onderstaande voorbeeld wordt de volledige SAS URI gebruikt om verbinding te maken met een [!DNL Azure Blob] -container, maar u kunt andere methoden en bewerkingen gebruiken voor verificatie. Zie dit [[!DNL Microsoft]  document op Python v12 SDK &#x200B;](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) voor meer informatie.

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### Een bestand uploaden met [!DNL AzCopy]

In het volgende voorbeeld wordt het hulpprogramma [!DNL Microsoft's] [!DNL AzCopy] gebruikt om een bestand te uploaden naar een [!DNL Data Landing Zone] :

>[!TIP]
>
>In het onderstaande voorbeeld wordt de opdracht `copy` gebruikt, maar u kunt andere opdrachten en opties gebruiken om een bestand naar uw [!DNL Data Landing Zone] te uploaden met [!DNL AzCopy] . Zie dit [[!DNL Microsoft AzCopy]  document &#x200B;](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) voor meer informatie.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## De [!DNL Data Landing Zone] source voor Experience Platform instellen op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/landing/multi-cloud).

Volg de onderstaande stappen om te leren hoe u uw [!DNL Data Landing Zone] -account voor Experience Platform op Amazon Web Services (AWS) kunt instellen.

### IP adres lijst van gewenste personen voor verbinding op AWS

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform op AWS aan te sluiten. Voor meer informatie, lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform op AWS &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

### AWS CLI instellen en bewerkingen uitvoeren

- Lees de gids bij [&#x200B; het installeren van of het bijwerken aan de recentste versie van AWS CLI &#x200B;](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

### AWS CLI configureren met tijdelijke referenties

Gebruik de opdracht AWS `configure` om uw CLI in te stellen met toegangstoetsen en een sessietoken.

```shell
aws configure
```

Voer bij de aanwijzing de volgende waarden in:

- AWS access key ID: `{YOUR_ACCESS_KEY_ID}`
- AWS geheime toegangstoets: `{YOUR_SECRET_ACCESS_KEY}`
- Standaardgebiedsnaam: `{YOUR_REGION}` (bijvoorbeeld `us-west-2` )
- Standaarduitvoerindeling: `json`

Stel vervolgens het sessietoken in:

```shell
aws configure set aws_session_token your-session-token
```

### Werken met bestanden op [!DNL Amazon S3]

>[!BEGINTABS]

>[!TAB  upload een dossier aan Amazon S3 ]

Template:

```shell
aws s3 cp local-file-path s3://bucketName/dlzFolder/remote-file-Name
```

Voorbeeld:

```shell
aws s3 cp example.txt s3://bucketName/dlzFolder/example.txt
```


>[!TAB  Download een dossier van Amazon S3 ]

Template:

```shell
aws s3 cp s3://bucketName/dlzFolder/remote-file local-file-path
```

Voorbeeld:

```shell
aws s3 cp s3://bucketName/dlzFolder/example.txt example.txt
```

>[!ENDTABS]

### Meld u aan bij de AWS-console met uw [!DNL Data Landing Zone] -referenties

#### Uw referenties extraheren

Eerst, moet u het volgende verkrijgen:

- `awsAccessKeyId`
- `awsSecretAccessKey`
- `awsSessionToken`

#### Een aanmeldingstoken genereren

Daarna, gebruik de gehaalde geloofsbrieven om een zitting tot stand te brengen en een sign-in teken te produceren gebruikend het eindpunt van de Federatie van AWS:

```py
import json
import requests
 
# Example DLZ response with credentials
response_json = '''{
    "credentials": {
        "awsAccessKeyId": "your-access-key",
        "awsSecretAccessKey": "your-secret-key",
        "awsSessionToken": "your-session-token"
    }
}'''
 
# Parse credentials
response_data = json.loads(response_json)
aws_access_key_id = response_data['credentials']['awsAccessKeyId']
aws_secret_access_key = response_data['credentials']['awsSecretAccessKey']
aws_session_token = response_data['credentials']['awsSessionToken']
 
# Create session dictionary
session = {
    'sessionId': aws_access_key_id,
    'sessionKey': aws_secret_access_key,
    'sessionToken': aws_session_token
}
 
# Generate the sign-in token
signin_token_url = "https://signin.aws.amazon.com/federation"
signin_token_payload = {
    "Action": "getSigninToken",
    "Session": json.dumps(session)
}
signin_token_response = requests.post(signin_token_url, data=signin_token_payload)
signin_token = signin_token_response.json()['SigninToken']
```

#### De aanmeldings-URL voor de AWS-console maken

Zodra u een aanmeldingstoken hebt, kunt u de URL maken die u in de AWS-console registreert en rechtstreeks naar het gewenste [!DNL Amazon S3] emmertje wijst.

```py
from urllib.parse import quote
 
# Define the S3 bucket and folder path you want to access
bucket_name = "your-bucket-name"
bucket_path = "your-bucket-folder"
 
# Construct the destination URL
destination_url = f"https://s3.console.aws.amazon.com/s3/buckets/{bucket_name}?prefix={bucket_path}/&tab=objects"
 
# Create the final sign-in URL
signin_url = f"https://signin.aws.amazon.com/federation?Action=login&Issuer=YourAppName&Destination={quote(destination_url)}&SigninToken={signin_token}"
 
print(f"Sign-in URL: {signin_url}")
```

#### De AWS-console openen

Navigeer ten slotte naar de gegenereerde URL om u rechtstreeks aan te melden bij de AWS-console met uw [!DNL Data Landing Zone] -referenties. Hiermee hebt u toegang tot een specifieke map in een [!DNL Amazon S3] -emmertje. De aanmeldings-URL neemt u rechtstreeks naar die map, zodat u alleen de toegestane gegevens ziet en beheert.

## Verbinden [!DNL Data Landing Zone] met Experience Platform

>[!IMPORTANT]
>
>- Als u verbinding wilt maken met de bron, hebt u de toegangsbeheermachtigingen **[!UICONTROL View Sources]** en **[!UICONTROL Manage Sources]** nodig. Voor meer informatie, lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](../../../access-control/home.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>
>- Privékoppelingen worden momenteel niet ondersteund wanneer verbinding wordt gemaakt met Experience Platform via [!DNL Data Landing Zone] . De enige gesteunde methodes voor toegang zijn de hier vermelde methodes [&#128279;](#manage-the-contents-of-your-data-landing-zone).

In de onderstaande documentatie vindt u informatie over het overbrengen van gegevens van uw [!DNL Data Landing Zone] -container naar Adobe Experience Platform met behulp van API&#39;s of de gebruikersinterface.

### API&#39;s gebruiken

- [Creeer a [!DNL Data Landing Zone]  bronverbinding gebruikend de Dienst API van de Stroom](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

- [Verbind  [!DNL Data Landing Zone]  met Experience Platform gebruikend UI](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)

