---
title: Bestemming landingszone gegevens
description: Leer hoe u verbinding maakt met Data Landing Zone om het publiek te activeren en gegevenssets te exporteren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 4eef1804d6974fd54f5e74e0efe62257190f408b
workflow-type: tm+mt
source-wordcount: '1976'
ht-degree: 0%

---

# Bestemming landingszone gegevens

>[!IMPORTANT]
>
>Deze documentatiepagina verwijst naar [!DNL Data Landing Zone] *bestemming*. Er is ook a [!DNL Data Landing Zone] *bron* in de broncatalogus. Voor meer informatie, lees de [[!DNL Data Landing Zone]  bron ](/help/sources/connectors/cloud-storage/data-landing-zone.md) documentatie.


## Overzicht {#overview}

[!DNL Data Landing Zone] is een interface voor cloudopslag die door Adobe Experience Platform is ingericht en waarmee u toegang hebt tot een veilige opslagvoorziening voor bestanden in de cloud waarmee u bestanden vanuit Experience Platform kunt exporteren. U hebt toegang tot één [!DNL Data Landing Zone] container per sandbox en het totale gegevensvolume voor alle containers is beperkt tot de totale gegevens die worden geleverd bij uw Experience Platform-licentie voor producten en services. Alle klanten van Experience Platform en de bijbehorende toepassingen, zoals [!DNL Customer Journey Analytics] , [!DNL Journey Orchestration] , [!DNL Intelligent Services] en [!DNL Real-Time Customer Data Platform] , beschikken over één [!DNL Data Landing Zone] container per sandbox.

Experience Platform past een strikte, 7-dagen durende (TTL) toe op alle bestanden die naar een [!DNL Data Landing Zone] -container zijn geüpload. Alle bestanden worden na zeven dagen verwijderd.

De [!DNL Data Landing Zone] doelconnector is beschikbaar voor klanten die de Azure- of Amazon Web Service-cloudondersteuning gebruiken. Het authentificatiemechanisme is verschillend gebaseerd op de wolk waarin de bestemming provisioned is, zijn al het andere over de bestemming en zijn gebruiksgevallen het zelfde. Lees meer over de twee verschillende authentificatiemechanismen in de secties [ voor authentiek verklaren aan de Gegevens Landing Zone die in Azure Blob ](#authenticate-dlz-azure) wordt voorzien en [ voor authentiek verklaart aan de AWS-provisioned Gegeven Landing Zone ](#authenticate-dlz-aws).

![ Diagram die tonen hoe de implementatie van de bestemmings van de Gebied van Gegevens verschillend is gebaseerd op de wolkensteun.](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png " Gegevens Landing Zone bestemmingsimplementatie door wolkensteun "){zoomable="yes"}

## Verbinding maken met uw [!UICONTROL Data Landing Zone] -opslag via API of UI {#connect-api-or-ui}

* Om met uw [!UICONTROL Data Landing Zone] opslagplaats te verbinden gebruikend het gebruikersinterface van Experience Platform, lees de secties [ verbinden met de bestemming ](#connect) en [ actief publiek aan deze bestemming ](#activate) hieronder.
* Om met uw [!UICONTROL Data Landing Zone] opslagplaats programmatically te verbinden, lees [ actief publiek aan op dossier-gebaseerde bestemmingen door de dienst API van de Stroom te gebruiken leerprogramma ](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de toepasselijke schemagebieden (bijvoorbeeld uw PPID), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [ werkschema van de bestemmingsactivering ](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [ partij op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt dataset de uitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Hoe te [ datasets uitvoeren gebruikend het gebruikersinterface van Experience Platform ](/help/destinations/ui/export-datasets.md).
* Hoe te [ datasets programmatically uitvoeren gebruikend de Dienst API van de Stroom ](/help/destinations/api/export-datasets.md).

## Bestandsindeling van de geëxporteerde gegevens {#file-format}

Wanneer het uitvoeren van *publieksgegevens*, leidt Experience Platform tot een `.csv`, `parquet`, of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [ gesteunde dossierformaten voor de uitvoer ](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) sectie in het leerprogramma van de publiekactivering.

Wanneer het uitvoeren van *datasets*, leidt Experience Platform tot een `.parquet` of `.json` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [ succesvolle datasetuitvoer ](../../ui/export-datasets.md#verify) sectie in het de uitvoerdatasetleerprogramma verifiëren.

## Verifieer aan de Gebied van Gegevens die in Azure Blob wordt verstrekt {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die worden uitgevoerd op Microsoft Azure. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

U kunt bestanden lezen en schrijven naar uw container via [!DNL Azure Storage Explorer] of de opdrachtregelinterface.

[!DNL Data Landing Zone] biedt ondersteuning voor verificatie op basis van SAS en de bijbehorende gegevens zijn in rust en onderweg beveiligd met standaard [!DNL Azure Blob] -opslagbeveiligingsmechanismen. SAS staat voor [ gedeelde toegangshandtekening ](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

Als u uw gegevens via een openbare internetverbinding wilt beveiligen, gebruikt u SAS-verificatie voor een veilige toegang tot uw [!DNL Data Landing Zone] -container. Er zijn geen netwerkwijzigingen vereist voor toegang tot uw [!DNL Data Landing Zone] -container. Dit betekent dat u geen lijsten van gewenste personen of instellingen voor meerdere regio&#39;s voor uw netwerk hoeft te configureren.

### Sluit de [!DNL Data Landing Zone] -container aan op [!DNL Azure Storage Explorer]

U kunt [[!DNL Azure Storage Explorer] gebruiken ](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) om de inhoud van uw [!DNL Data Landing Zone] container te beheren. Als u [!DNL Data Landing Zone] wilt gaan gebruiken, moet u eerst uw referenties ophalen, deze invoeren in [!DNL Azure Storage Explorer] en de [!DNL Data Landing Zone] -container verbinden met [!DNL Azure Storage Explorer] .

Selecteer in de gebruikersinterface van [!DNL Azure Storage Explorer] het verbindingspictogram op de linkernavigatiebalk. Het **Uitgezochte venster van het Middel** verschijnt, die u van opties voorzien om met te verbinden. Selecteer **[!DNL Blob container]** om verbinding te maken met uw [!DNL Data Landing Zone] -opslag.

![ Uitgezochte middel dat in Azure UI wordt benadrukt.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Daarna, selecteer **Gedeelde toegangshandtekening URL (SAS)** als uw verbindingsmethode, en selecteer dan **daarna**.

![ Uitgezochte verbindingsmethode die in Azure UI wordt benadrukt.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Na het selecteren van uw verbindingsmethode, moet u a **vertoningsnaam** en **[!DNL Blob]container SAS URL** verstrekken die met uw [!DNL Data Landing Zone] container beantwoordt.

>[!BEGINSHADEBOX]

### De referenties voor uw [!DNL Data Landing Zone] ophalen {#retrieve-dlz-credentials}

U moet de Experience Platform API&#39;s gebruiken om uw [!DNL Data Landing Zone] -gegevens op te halen. De API-aanroep om uw referenties op te halen wordt hieronder beschreven. Voor informatie over het krijgen van de vereiste waarden voor uw kopballen, verwijs [ Begonnen het worden met Adobe Experience Platform APIs ](/help/landing/api-guide.md) gids.

**API formaat**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Query-parameters | Beschrijving |
| --- | --- |
| `dlz_destination` | Met het type `dlz_destination` kan de API een doelcontainer van de landingszone onderscheiden van de andere typen containers die voor u beschikbaar zijn. |

{style="table-layout:auto"}

**Verzoek**

In het volgende aanvraagvoorbeeld worden de gegevens voor een bestaande landingszone opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Reactie**

De volgende reactie retourneert de referentie-informatie voor de landingszone, inclusief de huidige `SASToken` en `SASUri` , en de `storageAccountName` die overeenkomen met de container van de landingszone.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `containerName` | De naam van uw landingszone. |
| `SASToken` | Het token voor gedeelde toegangshandtekeningen voor uw landingszone. Deze tekenreeks bevat alle informatie die nodig is om een aanvraag te autoriseren. |
| `SASUri` | De URI van de gedeelde toegangshandtekening voor uw landingszone. Deze tekenreeks is een combinatie van de URI naar de landingszone waarvoor u geauthenticeerd wordt en de bijbehorende SAS-token, |

{style="table-layout:auto"}

### [!DNL Data Landing Zone] gebruikersgegevens bijwerken {#update-dlz-credentials}

U kunt uw gegevens desgewenst ook vernieuwen. U kunt uw `SASToken` bijwerken door een POST-aanvraag in te dienen bij het `/credentials` eindpunt van de [!DNL Connectors] API.

**API formaat**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Query-parameters | Beschrijving |
| --- | --- |
| `dlz_destination` | Met het type `dlz_destination` kan de API een doelcontainer van de landingszone onderscheiden van de andere typen containers die voor u beschikbaar zijn. |
| `refresh` | Met de handeling `refresh` kunt u de gegevens van de landingszone opnieuw instellen en automatisch een nieuwe `SASToken` genereren. |

{style="table-layout:auto"}

**Verzoek**

Met het volgende verzoek worden de gegevens van uw landingszone bijgewerkt.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
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
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Verstrek uw vertoningsnaam (`containerName`) en [!DNL Data Landing Zone] SAS URL, zoals die in de hierboven beschreven API vraag is teruggekeerd, en selecteer dan **Volgende**.

![ ga verbindingsinfo in die in Azure UI wordt benadrukt.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Het **Summiere** venster verschijnt, die u van een overzicht van uw montages, met inbegrip van informatie over uw [!DNL Blob] eindpunt en toestemmingen voorzien. Wanneer klaar, uitgezochte **verbindt**.

![ Samenvatting van montages die in Azure UI worden getoond.](/help/sources/images/tutorials/create/dlz/summary.png)

Een geslaagde verbinding werkt de gebruikersinterface van [!DNL Azure Storage Explorer] bij met uw [!DNL Data Landing Zone] -container.

![ Samenvatting van de DLZ gebruikerscontainer die in Azure UI wordt benadrukt.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Als de [!DNL Data Landing Zone] -container is aangesloten op [!DNL Azure Storage Explorer] , kunt u nu bestanden van Experience Platform naar uw [!DNL Data Landing Zone] -container exporteren. Als u bestanden wilt exporteren, moet u een verbinding tot stand brengen met de [!DNL Data Landing Zone] -bestemming in de gebruikersinterface van Experience Platform, zoals hieronder wordt beschreven.

## Verifiëren voor de AWS-provisioned Data Landing Zone {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Voer de onderstaande bewerkingen uit om referenties naar uw [!DNL Data Landing Zone] -instantie te verkrijgen die is ingericht op AWS. Gebruik vervolgens een keuzerondje om verbinding te maken met de instantie [!DNL Data Landing Zone] .

>[!BEGINSHADEBOX]

### De referenties voor uw [!DNL Data Landing Zone] ophalen {#retrieve-dlz-credentials-aws}

U moet de Experience Platform API&#39;s gebruiken om uw [!DNL Data Landing Zone] -gegevens op te halen. De API-aanroep om uw referenties op te halen wordt hieronder beschreven. Voor informatie over het krijgen van de vereiste waarden voor uw kopballen, verwijs [ Begonnen het worden met Adobe Experience Platform APIs ](/help/landing/api-guide.md) gids.

**API formaat**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| Query-parameters | Beschrijving |
| --- | --- |
| `dlz_destination` | Voeg de `dlz_destination` vraagparameter toe om te specificeren dat u het [!DNL Data Landing Zone] *bestemmings* type van containergeloofsbrieven wilt worden teruggewonnen. Om geloofsbrieven voor een Gegevens te verbinden en terug te winnen die Zone ** aanvoeren, bekijk de [ documentatie van bronnen ](/help/sources/connectors/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

**Verzoek**

In het volgende aanvraagvoorbeeld worden de gegevens voor een bestaande landingszone opgehaald.

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**Reactie**

De volgende reactie retourneert de referentie-informatie voor de landingszone, inclusief de huidige `awsAccessKeyId` , `awsSecretAccessKey` en andere informatie.

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `credentials` | Dit object bevat de tags `awsAccessKeyId` , `awsSecretAccessKey` en `awsSessionToken` die Experience Platform gebruikt om bestanden te exporteren naar de ingericht locatie voor de landingszone van gegevens. |
| `dlzPath` | Dit object bevat het pad op de AWS-locatie met Adobe-provisioning waar geëxporteerde bestanden worden gedeponeerd. |
| `dlzProvider` | Geeft aan dat dit een Amazon S3-provisioned Data Landing Zone is. |
| `expiryTime` | Geeft aan wanneer de referenties in het `credentials` -object verlopen. Voer de aanvraag opnieuw uit om de voorwaarden te vernieuwen. |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) worden beschreven. Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Zorg ervoor dat u uw [!DNL Data Landing Zone] container aan [!DNL Azure Storage Explorer] zoals die in de [ wordt beschreven eerste vereisten ](#prerequisites) sectie hebt verbonden. Omdat [!DNL Data Landing Zone] is een opslagruimte met Adobe-provisioning, hoeft u geen verdere stappen in de Experience Platform-interface uit te voeren om verificatie naar de bestemming uit te voeren.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Bekijk een voorbeeld van een correct opgemaakte coderingssleutel in de onderstaande afbeelding.
  ![ Beeld dat een voorbeeld van een correct geformatteerde sleutel PGP in UI toont.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)
* **[!UICONTROL Name]**: vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Folder path]**: voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL File type]**: selecteer de indeling die Experience Platform moet gebruiken voor de geëxporteerde bestanden. Wanneer het selecteren van de [!UICONTROL CSV] optie, kunt u ook [ de dossier het formatteren opties ](../../ui/batch-destinations-file-formatting-options.md) vormen.
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Bekijk a [ steekproef manifestdossier ](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [ dataflow looppas ](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die het uitgevoerde dossier produceerde.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in uw opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [ publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

### Planning

In de **[!UICONTROL Scheduling]** stap, kunt u [ opstelling het uitvoerprogramma ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor uw [!DNL Data Landing Zone] bestemming en u kunt ook [ de naam van uw uitgevoerde dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) vormen.

### Kenmerken en identiteiten toewijzen {#map}

In de stap **[!UICONTROL Mapping]** kunt u selecteren welke kenmerk- en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie, bekijk de [ toewijzingsstap ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in de activerende partijbestemmingen UI leerprogramma.

## Geëxporteerde gegevens valideren {#exported-data}

Om te controleren of gegevens zijn geëxporteerd, controleert u de [!DNL Data Landing Zone] -opslag en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.
