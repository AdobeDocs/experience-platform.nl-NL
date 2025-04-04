---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;adobe campagne;campagne
title: Adobe Campaign-verbinding
description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offline kanalen personaliseren en te leveren.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---

# Adobe Campaign-verbinding

## Overzicht {#overview}

Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offline kanalen personaliseren en te leveren. Zie [ Begonnen met Campaign Classic ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) voor meer informatie krijgen.

Om publieksgegevens naar Adobe Campaign te verzenden, moet u eerst [ de bestemming ](#connect-destination) in Adobe Experience Platform verbinden, en dan [ opstelling een gegevensinvoer ](#import-data-into-campaign) van uw opslagplaats in Adobe Campaign.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [ werkschema van de bestemmingsactivering ](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [ partij op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#allow-list}

Bij het opzetten van e-mail marketing bestemmingen met de opslag van SFTP, adviseert Adobe dat u bepaalde IP waaiers aan uw lijst van gewenste personen toevoegt.

Verwijs naar [ IP adreslijst van gewenste personen voor bestemmingen SFTP ](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ toegangsbeheeroverzicht ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

Adobe Campaign ondersteunt de volgende verbindingstypen:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

De voorkeursmethode voor het verzenden van gegevens naar Adobe Campaign is via [!DNL Amazon S3] of [!DNL Azure Blob] .

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* Voor **[!UICONTROL Amazon S3]** -verbindingen moet u de [!UICONTROL Access Key ID] en [!UICONTROL Secret Access Key] opgeven.
* Voor **[!UICONTROL SFTP with Password]** -verbindingen moet u [!UICONTROL Domain] , [!UICONTROL Port] , [!UICONTROL Username] en [!UICONTROL Password] opgeven.
* Voor **[!UICONTROL SFTP with SSH Key]** -verbindingen moet u [!UICONTROL Domain] , [!UICONTROL Port] , [!UICONTROL Username] en [!UICONTROL SSH Key] opgeven.
* Voor **[!UICONTROL Azure Blob]** -verbindingen moet u een verbindingstekenreeks opgeven.
* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan geëxporteerde bestanden onder de sectie **[!UICONTROL Key]** . De openbare sleutel moet als een [!DNL Base64] gecodeerde tekenreeks worden geschreven.
* **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
* **[!UICONTROL Description]**: voer een beschrijving in voor uw doel.
* **[!UICONTROL Bucket Name]**: *voor S3 verbindingen*. Voer de locatie van uw S3-emmertje in waar [!DNL Experience Platform] uw exportgegevens als CSV-bestanden indient.
* **[!UICONTROL Folder Path]**: geef het pad op uw opslaglocatie op waar [!DNL Experience Platform] uw exportgegevens als CSV-bestanden indient.
* **[!UICONTROL Container]**: *voor verbindingen Blob*. De container die het blob-pad voor uw map bevat, bevindt zich in.
* **[!UICONTROL File Format]**: Selecteer **CSV** om Csv- dossiers naar uw opslagplaats uit te voeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}


Zie [ publieksgegevens aan de uitvoerbestemmingen van het partijprofiel ](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

### Doelkenmerken {#destination-attributes}

Wanneer het activeren van publiek aan deze bestemming, adviseert Adobe dat u een uniek herkenningsteken van uw [ verenigingsschema ](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, verwijs naar [ beste praktijken wanneer het activeren van publiek aan e-mail marketing bestemmingen ](overview.md#best-practices).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Adobe Campaign] -doelen maakt [!DNL Experience Platform] een `.csv` -bestand in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de dossiers, zie [ sectie van de publiekactivering ](../../ui/activate-batch-profile-destinations.md#verify) in het leerprogramma van de publiekactivering verifiëren.

## Gegevensimport instellen in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Houd bij het uitvoeren van deze integratie rekening met de opslaglimieten van [!DNL SFTP] , de opslaglimieten van de database en de limieten van het actieve profiel zoals vastgelegd in uw Adobe Campaign-contract.
>* U moet uw geëxporteerde segmenten in Adobe Campaign plannen, importeren en toewijzen met behulp van [!DNL Campaign] -workflows. Verwijs naar [ Vestiging een terugkomende invoer ](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) in de documentatie van Adobe Campaign Classic en [ Ongeveer de activiteiten van het gegevensbeheer ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in de documentatie van Adobe Campaign Standard.
>* De voorkeursmethode voor het verzenden van gegevens naar Adobe Campaign is via [!DNL Amazon S3] of [!DNL Azure Blob] .

Nadat u [!DNL Experience Platform] hebt verbonden met uw [!DNL Amazon S3] - of [!DNL Azure Blob] -opslag, moet u de gegevensimport instellen vanaf uw opslaglocatie naar Adobe Campaign. Raadpleeg de volgende Adobe Campaign-documentatiepagina&#39;s voor meer informatie hierover:
* [ krijgt begonnen met gegevensimport en de uitvoer ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) en [ het laden van Gegevens (dossier) ](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) in de documentatie van Adobe Campaign Classic.
* [ krijgt begonnen met processen en gegevensbeheer ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) en [ dossier van de Lading ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) in de documentatie van Adobe Campaign Standard.
