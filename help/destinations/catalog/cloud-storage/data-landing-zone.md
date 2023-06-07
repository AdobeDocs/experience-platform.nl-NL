---
title: Bestemming landingszone gegevens
description: Leer hoe te met Gegevens het Landing Zone te verbinden om segmenten te activeren en datasets uit te voeren.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 8890fd137cfe6d35dcf6177b5516605e7753a75a
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 0%

---

# (Beta) Bestemming gegevenslandingszone

>[!IMPORTANT]
>
>* Deze bestemming is momenteel in Bèta en is slechts beschikbaar aan een beperkt aantal klanten. Om toegang tot [!DNL Data Landing Zone] verbinding, neem contact op met uw Adobe-vertegenwoordiger en geef uw [!DNL Organization ID].
>* Deze documentatiepagina verwijst naar de [!DNL Data Landing Zone] *doel*. Er is ook een [!DNL Data Landing Zone] *bron* in de broncatalogus. Lees voor meer informatie de [[!DNL Data Landing Zone] bron](/help/sources/connectors/cloud-storage/data-landing-zone.md) documentatie.



## Overzicht {#overview}

[!DNL Data Landing Zone] is een [!DNL Azure Blob] -opslaginterface die door Adobe Experience Platform is ingericht, zodat u toegang hebt tot een veilige, op de cloud gebaseerde opslagvoorziening voor bestanden om bestanden uit het Platform te exporteren. U hebt toegang tot [!DNL Data Landing Zone] container per sandbox, en het totale gegevensvolume over alle containers is beperkt tot de totale gegevens die worden geleverd bij uw Platform Products and Services-licentie. Alle klanten van Platform en zijn toepassingsdiensten zoals [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], en [!DNL Real-Time Customer Data Platform] zijn voorzien van één [!DNL Data Landing Zone] container per sandbox. U kunt bestanden lezen en schrijven naar uw container via [!DNL Azure Storage Explorer] of uw opdrachtregelinterface.

[!DNL Data Landing Zone] biedt ondersteuning voor verificatie op basis van SAS en de bijbehorende gegevens zijn beveiligd met standaard [!DNL Azure Blob] beveiligingsmechanismen voor de opslag in rust en in doorvoer. Met SAS-verificatie hebt u veilig toegang tot uw [!DNL Data Landing Zone] via een openbare internetverbinding. Er zijn geen netwerkwijzigingen vereist voor toegang tot uw [!DNL Data Landing Zone] container, wat betekent u geen lijsten van gewenste personen of dwars-regio montages voor uw netwerk moet vormen.

Platform dwingt strenge tijd-aan-levende (TTL) zeven dagen op alle dossiers af die aan worden geupload [!DNL Data Landing Zone] container. Alle bestanden worden na zeven dagen verwijderd.

## Verbinding maken met uw [!UICONTROL Data Landing Zone] opslag via API of UI {#connect-api-or-ui}

* Als u verbinding wilt maken met uw [!UICONTROL Data Landing Zone] opslaglocatie via de gebruikersinterface van het Platform, lees de secties [Verbinden met de bestemming](#connect) en [Segmenten naar dit doel activeren](#activate) hieronder.
* Als u verbinding wilt maken met uw [!UICONTROL Data Landing Zone] opslagplaats programmatically, lees de [Activeer segmenten aan op dossier-gebaseerde bestemmingen door de Dienst API van de Stroom te gebruiken leerprogramma](../../api/activate-segments-file-based-destinations.md).

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de toepasselijke schemavelden (bijvoorbeeld uw PPID), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Vereisten {#prerequisites}

Houd rekening met de volgende voorwaarden waaraan moet worden voldaan voordat u de opdracht [!DNL Data Landing Zone] bestemming.

### Verbind uw [!DNL Data Landing Zone] container naar [!DNL Azure Storage Explorer]

U kunt [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) om de inhoud van uw [!DNL Data Landing Zone] container. Als u wilt beginnen met [!DNL Data Landing Zone], moet u eerst uw referenties ophalen en deze invoeren in [!DNL Azure Storage Explorer]en sluit uw [!DNL Data Landing Zone] container naar [!DNL Azure Storage Explorer].

In de [!DNL Azure Storage Explorer] UI, selecteer het verbindingspictogram in de linkernavigatiebar. De **Bron selecteren** wordt weergegeven, zodat u beschikt over opties voor het maken van een verbinding. Selecteren **[!DNL Blob container]** om verbinding te maken met uw [!DNL Data Landing Zone] opslag.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Selecteer vervolgens **URL voor gedeelde toegangshandtekening (SAS)** als uw verbindingsmethode, en selecteer dan **Volgende**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Nadat u de verbindingsmethode hebt geselecteerd, moet u een **weergavenaam** en de **[!DNL Blob]SAS-URL van container** dat overeenkomt met uw [!DNL Data Landing Zone] container.

>[!BEGINSHADEBOX]

### Haal de referenties voor uw [!DNL Data Landing Zone]

U moet de Platform APIs gebruiken om uw terug te winnen [!DNL Data Landing Zone] referenties. De API-aanroep om uw referenties op te halen wordt hieronder beschreven. Voor informatie over het krijgen van de vereiste waarden voor uw kopballen, verwijs naar [Aan de slag met Adobe Experience Platform API&#39;s](/help/landing/api-guide.md) hulplijn.

**API-indeling**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

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

>[!ENDSHADEBOX]

Geef uw weergavenaam op (`containerName`) en [!DNL Data Landing Zone] SAS URL, zoals die in de hierboven beschreven API vraag is teruggekeerd, en dan selecteren **Volgende**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

De **Samenvatting** wordt weergegeven en krijgt u een overzicht van uw instellingen, inclusief informatie over uw [!DNL Blob] eindpunt en machtigingen. Indien gereed, selecteert u **Verbinden**.

![samenvatting](/help/sources/images/tutorials/create/dlz/summary.png)

Een geslaagde verbinding werkt uw [!DNL Azure Storage Explorer] UI met uw [!DNL Data Landing Zone] container.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Met uw [!DNL Data Landing Zone] container verbonden met [!DNL Azure Storage Explorer]kunt u nu bestanden van het Experience Platform naar uw [!DNL Data Landing Zone] container. Als u bestanden wilt exporteren, moet u een verbinding tot stand brengen met de [!DNL Data Landing Zone] doel in de interface van het Experience Platform, zoals beschreven in de sectie hieronder.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Zorg ervoor dat u verbinding hebt gemaakt met uw [!DNL Data Landing Zone] container naar [!DNL Azure Storage Explorer] zoals beschreven in de [voorwaarden](#prerequisites) sectie. Omdat [!DNL Data Landing Zone] is een Adobe-provisioned opslag, te hoeven u geen verdere stappen in het Experience Platform UI uit te voeren om aan de bestemming voor authentiek te verklaren.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.
* **[!UICONTROL File type]**: Selecteer de indeling die het Experience Platform moet gebruiken voor de geëxporteerde bestanden. Wanneer u de [!UICONTROL CSV] kunt u ook [configureren, opties voor bestandsindeling](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Selecteer het compressietype dat Experience Platform moet gebruiken voor de geëxporteerde bestanden.
* **[!UICONTROL Include manifest file]**: Schakel deze optie in als u wilt dat bij het exporteren een manifest-JSON-bestand wordt opgenomen dat informatie bevat over de exportlocatie, de exportgrootte en meer.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Planning

In de **[!UICONTROL Scheduling]** stap, u kunt [het exportschema instellen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor uw [!DNL Data Landing Zone] doel en u kunt ook [de naam van uw geëxporteerde bestanden configureren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Kenmerken en identiteiten toewijzen {#map}

In de **[!UICONTROL Mapping]** U kunt kiezen welke kenmerken en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie bekijkt u de [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in activeer partijbestemmingen UI zelfstudie.

## (bètaversie) Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt datasetuitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees de leerprogramma&#39;s:

* Procedure [de uitvoer datasets gebruikend het gebruikersinterface van de Platform](/help/destinations/ui/export-datasets.md).
* Procedure [de uitvoer datasets programmatically gebruikend de Dienst API van de Stroom](/help/destinations/api/export-datasets.md).

## Geëxporteerde gegevens valideren {#exported-data}

Controleer uw [!DNL Data Landing Zone] opslaan en ervoor zorgen dat de geëxporteerde bestanden de verwachte profielpopulaties bevatten.
