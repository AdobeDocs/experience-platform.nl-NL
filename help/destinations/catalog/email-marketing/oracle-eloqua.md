---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;oracle eloqua;oracle
title: (Bestanden) Oracle Eloqua-verbinding
description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en het genereren van verkoopleads te beheren.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# [!DNL (Files) Oracle Eloqua] verbinding

[[!DNL Oracle Eloqua] &#x200B;](https://www.oracle.com/cx/marketing/automation/) is software als de dienstplatform (van SaaS) voor marketing automatisering die door [!DNL Oracle] wordt aangeboden die B2B marketers en organisaties probeert te helpen marketing campagnes en verkooplood produceren.

Om publieksgegevens naar [!DNL Oracle Eloqua] te verzenden, moet u eerst [&#x200B; de bestemming &#x200B;](#connect-destination) in Adobe Experience Platform verbinden, en dan [&#x200B; opstelling een gegevensinvoer &#x200B;](#import-data-into-eloqua) van uw opslagplaats in [!DNL Oracle Eloqua].

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [&#x200B; werkschema van de bestemmingsactivering &#x200B;](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [&#x200B; partij op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#allow-list}

Bij het instellen van e-mailmarketingdoelen met SFTP-opslag raadt Adobe u aan bepaalde IP-bereiken toe te voegen aan uw lijst van gewenste personen.

Verwijs naar [&#x200B; IP adres lijst van gewenste personen voor bestemmingen SFTP &#x200B;](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; toegangsbeheeroverzicht &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

Dit doel ondersteunt de volgende verbindingstypen:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Verbindingsparameters {#parameters}

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* Voor **[!UICONTROL SFTP with Password]** -verbindingen moet u het volgende opgeven:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* Voor **[!UICONTROL SFTP with SSH Key]** -verbindingen moet u het volgende opgeven:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]

* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan geëxporteerde bestanden onder de sectie **[!UICONTROL Key]** . De openbare sleutel moet als een [!DNL Base64] gecodeerde tekenreeks worden geschreven.
* **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
* **[!UICONTROL Description]**: voer een beschrijving in voor uw doel.
* **[!UICONTROL Folder Path]**: geef het pad op uw opslaglocatie op waar Experience Platform uw exportgegevens als CSV-bestanden indient.
* **[!UICONTROL File Format]**: Selecteer **CSV** om Csv- dossiers naar uw opslagplaats uit te voeren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Zie [&#x200B; publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](../../ui/activate-batch-profile-destinations.md) voor instructies op het activeren van publiek aan deze bestemming activeren.

### Doelkenmerken {#destination-attributes}

Wanneer het activeren van publiek aan deze bestemming, adviseert Adobe dat u een uniek herkenningsteken van uw [&#x200B; verenigingsschema &#x200B;](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, verwijs naar [&#x200B; beste praktijken wanneer het activeren van publiek aan e-mail marketing bestemmingen &#x200B;](overview.md#best-practices).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Oracle Eloqua] -doelen maakt Experience Platform een `.csv` -bestand in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de dossiers, zie [&#x200B; de activering van het publiek &#x200B;](../../ui/activate-batch-profile-destinations.md#verify) in het leerprogramma van de publiekactivering verifiëren.

## Gegevensimport instellen in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Nadat u [!DNL Experience Platform] hebt verbonden met uw [!DNL SFTP] -opslag, moet u de gegevens die u wilt importeren vanaf uw opslaglocatie naar [!DNL Oracle Eloqua] instellen. Leren hoe te om dit te verwezenlijken, zie [&#x200B; Importerend contacten of rekeningen &#x200B;](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center].
