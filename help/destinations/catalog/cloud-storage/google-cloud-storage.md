---
title: (bèta) Google Cloud Storage-verbinding
description: Leer hoe u verbinding maakt met Google Cloud Storage en segmenten activeert of gegevenssets exporteert.
source-git-commit: 56fd7a5ab58186367c729cb4ca8c3b4213c44900
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# (bèta) [!DNL Google Cloud Storage] verbinding

>[!IMPORTANT]
>
>Deze bestemming is momenteel in Bèta en is slechts beschikbaar aan een beperkt aantal klanten. Om toegang tot [!DNL Google Cloud Storage] verbinding, neem contact op met uw Adobe-vertegenwoordiger en geef uw [!DNL Organization ID].

## Overzicht {#overview}

Een live uitgaande verbinding maken met [!DNL Google Cloud Storage] om gegevensbestanden van Adobe Experience Platform regelmatig naar uw eigen emmers te exporteren.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de toepasselijke schemavelden, zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Vereiste instellingen voor verbinding met uw [!DNL Google Cloud Storage] account {#prerequisites}

Om Platform met te verbinden [!DNL Google Cloud Storage], moet u eerst interoperabiliteit voor uw [!DNL Google Cloud Storage] account. Voor toegang tot de interoperabiliteitsinstelling opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Settings]** van de **[!UICONTROL Cloud Storage]** in het navigatievenster.

![Google Cloud Platform-dashboard met Cloud Storage en Settings gemarkeerd.](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

De **[!UICONTROL Settings]** wordt weergegeven. Hier kunt u informatie over uw [!DNL Google] project-id en details over uw [!DNL Google Cloud Storage] account. Om tot interoperabiliteitsmontages toegang te hebben, selecteer **[!UICONTROL Interoperability]** in de bovenste koptekst.

![Het tabblad Interoperabiliteit wordt gemarkeerd op het dashboard voor het Google Cloud-Platform.](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

De **[!UICONTROL Interoperability]** De pagina bevat informatie over authentificatie, toegangstoetsen, en het standaardproject verbonden aan uw de dienstrekening. Als u een nieuwe toegangstoets-id en een geheime toegangssleutel voor uw serviceaccount wilt genereren, selecteert u **[!UICONTROL Create a Key for a Service Account]**.

![De sleutel voor een serviceaccountbesturingselement maken die is gemarkeerd op het dashboard voor Google Cloud-Platforms.](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

U kunt uw onlangs gegenereerde toegangstoets-id en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] aan Platform.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](/help/destinations/ui/connect-destination.md). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Access key ID]**: Een alfanumerieke tekenreeks van 61 tekens die wordt gebruikt voor het verifiëren van uw [!DNL Google Cloud Storage] aan Platform. Voor informatie over het verkrijgen van deze waarde leest u de [voorwaarden](#prerequisites) hierboven.
* **[!UICONTROL Secret access key]**: Een tekenreeks van 40 tekens met een basiscodering van 64 tekens die wordt gebruikt voor de verificatie van uw [!DNL Google Cloud Storage] aan Platform. Voor informatie over het verkrijgen van deze waarde leest u de [voorwaarden](#prerequisites) hierboven.
* **[!UICONTROL Encryption key]**: U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling toe te voegen aan uw geëxporteerde bestanden. Uw openbare sleutel moet worden geschreven als een [!DNL Base64-encoded] tekenreeks. Bekijk een voorbeeld van een correct geformatteerde, base64-gecodeerde sleutel in de documentatieverbinding hieronder. Het middelste deel wordt verkort om kort te zijn.

   ![Afbeelding die een voorbeeld toont van een PGP-sleutel met de juiste indeling en basis64-codering in de gebruikersinterface](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Voor meer informatie over deze waarden leest u de [HMAC-sleutels voor Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) hulplijn. Raadpleeg voor meer informatie over het genereren van uw eigen toegangstoets-id en geheime toegangstoets de [[!DNL Google Cloud Storage] bronoverzicht](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Vul de voorkeursnaam voor dit doel in.
* **[!UICONTROL Description]**: Optioneel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken.
* **[!UICONTROL Bucket name]**: Voer de naam in van de [!DNL Google Cloud Storage] emmer die door deze bestemming moet worden gebruikt.
* **[!UICONTROL Folder path]**: Voer het pad in naar de doelmap waarin de geëxporteerde bestanden worden opgeslagen.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Planning

In de **[!UICONTROL Scheduling]** stap, u kunt [het exportschema instellen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) voor uw [!DNL Google Cloud Storage] doel en u kunt ook [de naam van uw geëxporteerde bestanden configureren](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Kenmerken en identiteiten toewijzen {#map}

In de **[!UICONTROL Mapping]** U kunt kiezen welke kenmerken en identiteitsvelden u wilt exporteren voor uw profielen. U kunt ook selecteren om de kopteksten in het geëxporteerde bestand te wijzigen in een gewenste vriendelijke naam. Voor meer informatie bekijkt u de [toewijzingsstap](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) in activeer partijbestemmingen UI zelfstudie.

## (bètaversie) Gegevensbestanden exporteren {#export-datasets}

Deze bestemming steunt datasetuitvoer. Voor volledige informatie over hoe te de uitvoer van de opstellingsdataset, lees [zelfstudie over exportgegevensbestanden](/help/destinations/ui/export-datasets.md).

## Geëxporteerde gegevens valideren {#exported-data}

Controleer uw [!DNL Google Cloud Storage] emmertje en zorg ervoor dat de uitgevoerde dossiers de verwachte profielpopulaties bevatten.
