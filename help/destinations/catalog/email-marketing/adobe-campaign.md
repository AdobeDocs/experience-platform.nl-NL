---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;adobe campagne;campagne
title: Adobe Campaign-verbinding
description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offline kanalen personaliseren en te leveren.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Adobe Campaign-verbinding

## Overzicht {#overview}

Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offline kanalen personaliseren en te leveren. Zie [Aan de slag met Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) voor meer informatie .

Als u publieksgegevens naar Adobe Campaign wilt verzenden, moet u eerst [verbinden de bestemming](#connect-destination) in Adobe Experience Platform, en vervolgens [een gegevensimport instellen](#import-data-into-campaign) vanaf uw opslaglocatie naar Adobe Campaign.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#allow-list}

Bij het opzetten van e-mail marketing bestemmingen met de opslag van SFTP, adviseert de Adobe dat u bepaalde IP waaiers aan uw lijst van gewenste personen toevoegt.

Zie [IP adres lijst van gewenste personen voor bestemmingen SFTP](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met uw productbeheerder om de vereiste machtigingen te verkrijgen

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

Adobe Campaign ondersteunt de volgende verbindingstypen:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

De voorkeursmethode voor het verzenden van gegevens naar Adobe Campaign is: [!DNL Amazon S3] of [!DNL Azure Blob].

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* Voor **[!UICONTROL Amazon S3]** verbindingen, moet u uw [!UICONTROL Access Key ID] en [!UICONTROL Secret Access Key].
* Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL Password].
* Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL SSH Key].
* Voor **[!UICONTROL Azure Blob]** verbindingen, moet u een verbindingstekenreeks verstrekken.
* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan geëxporteerde bestanden onder de **[!UICONTROL Key]** sectie. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.
* **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw doel.
* **[!UICONTROL Bucket Name]**: *Voor S3-verbindingen*. Ga de plaats van uw S3 emmertje in waar [!DNL Platform] zullen uw exportgegevens als CSV-bestanden indienen.
* **[!UICONTROL Folder Path]**: Geef het pad op in de opslaglocatie waar [!DNL Platform] zullen uw exportgegevens als CSV-bestanden indienen.
* **[!UICONTROL Container]**: *Voor Klob-verbindingen*. De container die het blob-pad voor uw map bevat, bevindt zich in.
* **[!UICONTROL File Format]**: Select **CSV** om CSV-bestanden naar uw opslaglocatie te exporteren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.


Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Doelkenmerken {#destination-attributes}

Wanneer het activeren van publiek aan deze bestemming, adviseert de Adobe dat u een uniek herkenningsteken van uw selecteert [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Raadpleeg voor meer informatie [best practices bij het activeren van doelgroepen naar marketingdoelen per e-mail](overview.md#best-practices).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Adobe Campaign] bestemmingen, [!DNL Platform] maakt een `.csv` in de opslaglocatie die u hebt opgegeven. Zie voor meer informatie over de bestanden [doelactivering controleren](../../ui/activate-batch-profile-destinations.md#verify) in de zelfstudie voor publieksactivering.

## Gegevensimport instellen in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Houd rekening met de [!DNL SFTP] opslaglimieten, opslaglimieten voor databases en limieten voor het actieve profiel zoals vastgelegd in uw Adobe Campaign-contract tijdens de uitvoering van deze integratie.
>* U moet uw geëxporteerde segmenten in Adobe Campaign plannen, importeren en toewijzen met [!DNL Campaign] workflows. Zie [Herhalende importbewerkingen instellen](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) in Adobe Campaign Classic documentatie en [Informatie over gegevensbeheeractiviteiten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in Adobe Campaign Standard documentatie.
>* De voorkeursmethode voor het verzenden van gegevens naar Adobe Campaign is: [!DNL Amazon S3] of [!DNL Azure Blob].

Na verbinding [!DNL Platform] aan uw [!DNL Amazon S3] of [!DNL Azure Blob] -opslag, moet u de gegevensimport van uw opslaglocatie naar Adobe Campaign instellen. Raadpleeg de volgende Adobe Campaign-documentatiepagina&#39;s voor meer informatie hierover:
* [Aan de slag met het importeren en exporteren van gegevens](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) en [Gegevens laden (bestand)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) in de documentatie van Adobe Campaign Classic.
* [Aan de slag met processen en gegevensbeheer](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) en [Bestand laden](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) in de documentatie van Adobe Campaign Standard.
