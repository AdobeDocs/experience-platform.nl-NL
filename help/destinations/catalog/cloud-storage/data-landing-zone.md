---
title: Bestemming landingszone gegevens
description: Leer hoe u verbinding maakt met Data Landing Zone om het publiek te activeren en gegevenssets te exporteren.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: cb37eda87b8fcc0d0284db7a0bab8d48eab5aae6
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# Bestemming landingszone gegevens

>[!IMPORTANT]
>
>Deze documentatiepagina verwijst naar de [!DNL Data Landing Zone] *doel*. Er is ook een [!DNL Data Landing Zone] *bron* in de broncatalogus. Lees voor meer informatie de [[!DNL Data Landing Zone] bron](/help/sources/connectors/cloud-storage/data-landing-zone.md) documentatie.


## Overzicht {#overview}

[!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht, zodat u toegang hebt tot een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden die u kunt exporteren vanuit Platform. U hebt toegang tot [!DNL Data Landing Zone] container per sandbox, en het totale gegevensvolume over alle containers is beperkt tot de totale gegevens die worden geleverd bij uw licentie voor platformproducten en -services. Alle klanten van Platform en zijn toepassingen zoals [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], en [!DNL Real-Time Customer Data Platform] zijn voorzien van één [!DNL Data Landing Zone] container per sandbox. U kunt bestanden lezen en schrijven naar uw container via [!DNL Azure Storage Explorer] of uw opdrachtregelinterface.

[!DNL Data Landing Zone] biedt ondersteuning voor verificatie op basis van SAS en de bijbehorende gegevens zijn beveiligd met standaard [!DNL Azure Blob] beveiligingsmechanismen voor de opslag in rust en in doorvoer. Met SAS-verificatie hebt u veilig toegang tot uw [!DNL Data Landing Zone] via een openbare internetverbinding. Er zijn geen netwerkwijzigingen vereist voor toegang tot uw [!DNL Data Landing Zone] container, wat betekent u geen lijsten van gewenste personen of dwars-regio montages voor uw netwerk moet vormen.

Het platform dwingt strikte tijd-aan-levende (TTL) zeven dagen op alle dossiers af die aan worden geupload [!DNL Data Landing Zone] container. Alle bestanden worden na zeven dagen verwijderd.

## Verbinding maken met uw [!UICONTROL Data Landing Zone] opslag via API of UI {#connect-api-or-ui}

* Als u verbinding wilt maken met uw [!UICONTROL Data Landing Zone] opslaglocatie via de gebruikersinterface van het platform, lees de secties [Verbinden met de bestemming](#connect) en [Soorten publiek naar dit doel activeren](#activate) hieronder.
* Als u verbinding wilt maken met uw [!UICONTROL Data Landing Zone] opslagplaats programmatically, lees de [Activeer publiek aan op dossier-gebaseerde bestemmingen door de Zelfstudie van de Dienst van de Stroom te gebruiken API](../../api/activate-segments-file-based-destinations.md).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de toepasselijke schemavelden (bijvoorbeeld uw PPID), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt dataset de uitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Procedure [de uitvoer datasets gebruikend het gebruikersinterface van het Platform](/help/destinations/ui/export-datasets.md).
* Procedure [de uitvoer datasets programmatically gebruikend de Dienst API van de Stroom](/help/destinations/api/export-datasets.md).

## Bestandsindeling van de geëxporteerde gegevens {#file-format}

Bij exporteren *publieksgegevens*, Platform maakt een `.csv`, `parquet`, of `.json` in de opslaglocatie die u hebt opgegeven. Zie voor meer informatie over de bestanden de [ondersteunde bestandsindelingen voor export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) in de zelfstudie voor publieksactivering.

Bij exporteren *gegevenssets*, Platform maakt een `.parquet` of `.json` in de opslaglocatie die u hebt opgegeven. Zie voor meer informatie over de bestanden de [succesvolle uitvoer van gegevenssets controleren](../../ui/export-datasets.md#verify) in de zelfstudie over exportgegevensbestanden.

## Vereisten {#prerequisites}

Houd rekening met de volgende voorwaarden waaraan moet worden voldaan voordat u de opdracht [!DNL Data Landing Zone] bestemming.

### Verbind uw [!DNL Data Landing Zone] container naar [!DNL Azure Storage Explorer]

U kunt [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) om de inhoud van uw [!DNL Data Landing Zone] container. Als u wilt beginnen met [!DNL Data Landing Zone], moet u eerst uw referenties ophalen en deze invoeren in [!DNL Azure Storage Explorer]en sluit uw [!DNL Data Landing Zone] container naar [!DNL Azure Storage Explorer].

In de [!DNL Azure Storage Explorer] UI, selecteer het verbindingspictogram in de linkernavigatiebar. De **Bron selecteren** wordt weergegeven, zodat u beschikt over opties voor het maken van een verbinding. Selecteren **[!DNL Blob container]** om verbinding te maken met uw [!DNL Data Landing Zone] opslag.

![Selecteer bron die is gemarkeerd in de Azure UI.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Selecteer vervolgens **URL voor gedeelde toegangshandtekening (SAS)** als uw verbindingsmethode, en selecteer dan **Volgende**.

![Selecteer verbindingsmethode die in de Azure UI wordt gemarkeerd.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Nadat u de verbindingsmethode hebt geselecteerd, moet u een **weergavenaam** en de **[!DNL Blob]SAS-URL van container** dat overeenkomt met uw [!DNL Data Landing Zone] container.

>[!BEGINSHADEBOX]

### Haal de referenties voor uw [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

U moet de platform-API&#39;s gebruiken om uw [!DNL Data Landing Zone] referenties. De API-aanroep om uw referenties op te halen wordt hieronder beschreven. Voor informatie over het krijgen van de vereiste waarden voor uw kopballen, verwijs naar [Aan de slag met Adobe Experience Platform API&#39;s](/help/landing/api-guide.md) hulplijn.

**API-indeling**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Query-parameters | Beschrijving |
| --- | --- |
| `dlz_destination` | De `dlz_destination` type staat API toe om een container van de landingszonebestemming van de andere types van containers te onderscheiden die voor u beschikbaar zijn. |

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

**Antwoord**

De volgende reactie retourneert de referentie-informatie voor uw landingszone, inclusief uw huidige `SASToken` en `SASUri`en de `storageAccountName` die overeenkomt met uw landingszonecontainer.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `containerName` | De naam van uw landingszone. |
| `SASToken` | Het token voor gedeelde toegangshandtekeningen voor uw landingszone. Deze tekenreeks bevat alle informatie die nodig is om een aanvraag te autoriseren. |
| `SASUri` | De URI van de gedeelde toegangshandtekening voor uw landingszone. Deze tekenreeks is een combinatie van de URI naar de landingszone waarvoor u geauthenticeerd wordt en de bijbehorende SAS-token, |

{style="table-layout:auto"}

### Bijwerken [!DNL Data Landing Zone] geloofsbrieven {#update-dlz-credentials}

U kunt uw gegevens desgewenst ook vernieuwen. U kunt uw `SASToken` door een POST aan de `/credentials` het eindpunt van de [!DNL Connectors] API.

**API-indeling**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Query-parameters | Beschrijving |
| --- | --- |
| `dlz_destination` | De `dlz_destination` type staat API toe om een container van de landingszonebestemming van de andere types van containers te onderscheiden die voor u beschikbaar zijn. |
| `refresh` | De `refresh` actie staat u toe om uw landingszonegeloofsbrieven terug te stellen en automatisch een nieuwe te produceren `SASToken`. |

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

>[!ENDSHADEBOX]

Geef uw weergavenaam op (`containerName`) en [!DNL Data Landing Zone] SAS URL, zoals die in de hierboven beschreven API vraag is teruggekeerd, en dan selecteren **Volgende**.

![Voer verbindingsgegevens in die zijn gemarkeerd in de Azure UI.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

De **Samenvatting** wordt weergegeven en krijgt u een overzicht van uw instellingen, inclusief informatie over uw [!DNL Blob] eindpunt en toestemmingen. Indien klaar, selecteert u **Verbinden**.

![Overzicht van instellingen die worden weergegeven in de Azure UI.](/help/sources/images/tutorials/create/dlz/summary.png)

Een geslaagde verbinding werkt uw [!DNL Azure Storage Explorer] UI met uw [!DNL Data Landing Zone] container.

![Overzicht van de DLZ gebruikerscontainer die in Azure UI wordt benadrukt.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Met uw [!DNL Data Landing Zone] container verbonden met [!DNL Azure Storage Explorer]kunt u nu bestanden van het Experience Platform naar uw [!DNL Data Landing Zone] container. Als u bestanden wilt exporteren, moet u een verbinding tot stand brengen met de [!DNL Data Landing Zone] doel in de interface van het Experience Platform, zoals beschreven in de sectie hieronder.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Zorg ervoor dat u verbinding hebt gemaakt met uw [!DNL Data Landing Zone] container naar [!DNL Azure Storage Explorer] zoals beschreven in de [voorwaarden](#prerequisites) sectie. Omdat [!DNL Data Landing Zone] is een Adobe-provisioned opslag, te hoeven u geen verdere stappen in het Experience Platform UI uit te voeren om aan de bestemming voor authentiek te verklaren.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL File type]**: Selecteer het Experience Platform voor de indeling die u voor de geëxporteerde bestanden wilt gebruiken. Wanneer u de [!UICONTROL CSV] kunt u [configureren, opties voor bestandsindeling](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer. Het manifest wordt genoemd gebruikend het formaat `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Een [voorbeeldmanifestbestand](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Het manifestbestand bevat de volgende velden:
   * `flowRunId`: De [dataflow run](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) waarmee het geëxporteerde bestand is gegenereerd.
   * `scheduledTime`: De tijd in UTC toen het bestand werd geëxporteerd.
   * `exportResults.sinkPath`: Het pad in de opslaglocatie waar het geëxporteerde bestand is opgeslagen.
   * `exportResults.name`: De naam van het geëxporteerde bestand.
   * `size`: De grootte van het geëxporteerde bestand, in bytes.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Planning

In de **[!UICONTROL Scheduling]** stap, u kunt [het exportschema instellen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor uw [!DNL Data Landing Zone] doel en u kunt ook [de naam van uw geëxporteerde bestanden configureren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Kenmerken en identiteiten toewijzen {#map}

In de **[!UICONTROL Mapping]** U kunt kiezen welke kenmerken en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie bekijkt u de [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in activeer partijbestemmingen UI zelfstudie.

## Geëxporteerde gegevens valideren {#exported-data}

Controleer uw [!DNL Data Landing Zone] opslaan en ervoor zorgen dat de geëxporteerde bestanden de verwachte profielpopulaties bevatten.
