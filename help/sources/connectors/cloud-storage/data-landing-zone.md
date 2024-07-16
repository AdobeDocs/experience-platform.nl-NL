---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Data Landing Zone Source
description: Leer hoe u Data Landing Zone kunt verbinden met Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: cb37eda87b8fcc0d0284db7a0bab8d48eab5aae6
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>Deze pagina is specifiek voor de [!DNL Data Landing Zone] *bron* schakelaar in Experience Platform. Voor informatie bij het verbinden met de [!DNL Data Landing Zone] *bestemmings* schakelaar, verwijs naar de [[!DNL Data Landing Zone]  pagina van de bestemmingsdocumentatie ](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht en waarmee u toegang hebt tot een veilige, op de cloud gebaseerde opslagfaciliteit voor bestanden om bestanden over te brengen naar het platform. U hebt toegang tot één [!DNL Data Landing Zone] container per sandbox en het totale gegevensvolume voor alle containers is beperkt tot de totale gegevens die worden geleverd bij uw Platform Products and Services-licentie. Alle klanten van Platform en de bijbehorende toepassingen, zoals [!DNL Customer Journey Analytics] , [!DNL Journey Orchestration] , [!DNL Intelligent Services] en [!DNL Adobe Real-Time Customer Data Platform] , beschikken over één [!DNL Data Landing Zone] container per sandbox. U kunt bestanden lezen en schrijven naar uw container via [!DNL Azure Storage Explorer] of de opdrachtregelinterface.

[!DNL Data Landing Zone] biedt ondersteuning voor verificatie op basis van SAS en de bijbehorende gegevens zijn in rust en onderweg beveiligd met standaard [!DNL Azure Blob] -opslagbeveiligingsmechanismen. Met verificatie op basis van SAS hebt u via een openbare internetverbinding veilig toegang tot uw [!DNL Data Landing Zone] -container. Er zijn geen netwerkwijzigingen vereist voor toegang tot uw [!DNL Data Landing Zone] -container. Dit betekent dat u geen lijsten van gewenste personen of instellingen voor meerdere regio&#39;s voor uw netwerk hoeft te configureren. Het platform past een strikte vervaltijd van zeven dagen toe op alle bestanden die naar een [!DNL Data Landing Zone] -container zijn geüpload. Alle bestanden worden na zeven dagen verwijderd.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden bij het benoemen van bestanden of mappen voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (zoals `0x00` tot en met `0x1F` , `\u0081` enzovoort), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## De inhoud van uw gegevenslandingszone beheren{#manage-the-contents-of-your-data-landing-zone}

U kunt [[!DNL Azure Storage Explorer] gebruiken ](https://azure.microsoft.com/en-us/features/storage-explorer/) om de inhoud van uw [!DNL Data Landing Zone] container te beheren.

Selecteer in de gebruikersinterface van [!DNL Azure Storage Explorer] het verbindingspictogram in de linkernavigatie. Het **Uitgezochte venster van het Middel** verschijnt, die u van opties voorzien om met te verbinden. Selecteer **[!DNL Blob container]** om verbinding te maken met [!DNL Data Landing Zone] .

![ selecteren-middel ](../../images/tutorials/create/dlz/select-resource.png)

Daarna, selecteer **Gedeelde toegangshandtekening URL (SAS)** als uw verbindingsmethode, en selecteer dan **daarna**.

![ selecteren-verbinding-methode ](../../images/tutorials/create/dlz/select-connection-method.png)

Na het selecteren van uw verbindingsmethode, moet u a **vertoningsnaam** en **[!DNL Blob]container SAS URL** daarna verstrekken die met uw [!DNL Data Landing Zone] container beantwoordt.

>[!TIP]
>
>U kunt uw [!DNL Data Landing Zone] -referenties ophalen uit de broncatalogus in de interface van het platform.

Verstrek uw [!DNL Data Landing Zone] SAS URL en selecteer dan **daarna**

![ enter-connection-info ](../../images/tutorials/create/dlz/enter-connection-info.png)

Het **Summiere** venster verschijnt, die u van een overzicht van uw montages, met inbegrip van informatie over uw [!DNL Blob] eindpunt en toestemmingen voorzien. Wanneer klaar, uitgezochte **verbindt**.

![ samenvatting ](../../images/tutorials/create/dlz/summary.png)

Een geslaagde verbinding werkt de gebruikersinterface van [!DNL Azure Storage Explorer] bij met uw [!DNL Data Landing Zone] -container.

![ dlz-gebruiker-container ](../../images/tutorials/create/dlz/dlz-user-container.png)

Als de [!DNL Data Landing Zone] -container is aangesloten op [!DNL Azure Storage Explorer] , kunt u nu bestanden uploaden naar de [!DNL Data Landing Zone] -container. Om te uploaden, **te selecteren uploadt** en dan **selecteert uploadt Dossiers**.

![ upload ](../../images/tutorials/create/dlz/upload.png)

Wanneer u het bestand hebt geselecteerd dat u wilt uploaden, moet u vervolgens het [!DNL Blob] type identificeren dat u het wilt uploaden als en de gewenste doelmap. Wanneer gebeëindigd, uitgezochte **uploadt**.

| [!DNL Blob] typen | Beschrijving |
| --- | --- |
| Blok [!DNL Blob] | Blok [!DNL Blobs] is geoptimaliseerd voor het efficiënt uploaden van grote hoeveelheden gegevens. Blok [!DNL Blobs] is de standaardoptie voor [!DNL Data Landing Zone] . |
| Toevoegen [!DNL Blob] | Toevoegen [!DNL Blobs] is geoptimaliseerd voor het toevoegen van gegevens aan het einde van het bestand. |

![ upload-dossiers ](../../images/tutorials/create/dlz/upload-files.png)

## Bestanden uploaden naar de [!DNL Data Landing Zone] via de opdrachtregelinterface

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

In het volgende voorbeeld wordt de [!DNL Microsoft's] Python v12 SDK gebruikt om een bestand te uploaden naar een [!DNL Data Landing Zone] :

>[!TIP]
>
>In het onderstaande voorbeeld wordt de volledige SAS URI gebruikt om verbinding te maken met een [!DNL Azure Blob] -container, maar u kunt andere methoden en bewerkingen gebruiken voor verificatie. Zie dit [[!DNL Microsoft]  document op Python v12 SDK ](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) voor meer informatie.

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
>In het onderstaande voorbeeld wordt de opdracht `copy` gebruikt, maar u kunt andere opdrachten en opties gebruiken om een bestand naar uw [!DNL Data Landing Zone] te uploaden met [!DNL AzCopy] . Zie dit [[!DNL Microsoft AzCopy]  document ](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) voor meer informatie.

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Verbinden [!DNL Data Landing Zone] met [!DNL Platform]

In de onderstaande documentatie vindt u informatie over het overbrengen van gegevens van uw [!DNL Data Landing Zone] -container naar Adobe Experience Platform met behulp van API&#39;s of de gebruikersinterface.

### API&#39;s gebruiken

- [Creeer a [!DNL Data Landing Zone]  bronverbinding gebruikend de Dienst API van de Stroom](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

- [Verbind  [!DNL Data Landing Zone]  met Platform gebruikend UI](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)

>[!IMPORTANT]
>
>Privékoppelingen worden momenteel niet ondersteund wanneer verbinding wordt gemaakt met een Experience Platform via de [!DNL Data Landing Zone] . De enige gesteunde methodes voor toegang zijn de hier vermelde methodes [ ](#manage-the-contents-of-your-data-landing-zone).

