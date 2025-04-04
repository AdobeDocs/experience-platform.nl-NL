---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;e-mailbestemming voor responsys
title: Oracle Responsys-verbinding
description: Responsys is een marketingtool voor e-mailberichten voor marketingcampagnes over meerdere kanalen die door Oracle worden aangeboden om interacties via e-mail, mobiele apparaten, displays en sociale media aan te passen.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# [!DNL Oracle Responsys] verbinding

## Overzicht {#overview}

[ Responsys ](https://www.oracle.com/cx/marketing/campaign-management/) is een ondernemings e-mail marketing hulpmiddel voor dwars-kanaal marketing campagnes die door [!DNL Oracle] worden aangeboden om interactie over e-mail, mobiel, vertoning, en sociaal te personaliseren.

Om publieksgegevens naar [!DNL Oracle Responsys] te verzenden, moet u eerst [ met de bestemming ](#connect-destination) in Adobe Experience Platform verbinden, en dan [ opstelling een gegevensinvoer ](#import-data-into-responsys) van uw opslagplaats in [!DNL Oracle Responsys].

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
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment, samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm van de uitgezochte profielkenmerken van het [ werkschema van de bestemmingsactivering ](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Lees meer over [ partij op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#allow-list}

Bij het instellen van e-mailmarketingdoelen met SFTP-opslag raadt Adobe u aan bepaalde IP-bereiken toe te voegen aan uw lijst van gewenste personen.

Verwijs naar [ IP adres lijst van gewenste personen voor bestemmingen SFTP ](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

Dit doel ondersteunt de volgende verbindingstypen:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Verbindingsparameters {#parameters}

Terwijl [ vestiging ](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

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

Voor [!DNL Oracle Responsys] -doelen maakt Experience Platform een `.csv` -bestand in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de dossiers, zie [ de activering van het publiek ](../../ui/activate-batch-profile-destinations.md#verify) in het leerprogramma van de publiekactivering verifiëren.

## Gegevensimport instellen in [!DNL Oracle Responsys] {#import-data-into-responsys}

Nadat u [!DNL Experience Platform] hebt verbonden met uw [!DNL SFTP] -opslag, moet u de gegevens die u wilt importeren vanaf uw opslaglocatie naar [!DNL Oracle Responsys] instellen. Leren hoe te om dit te verwezenlijken, zie [ Importerend contacten of rekeningen ](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in [!DNL Oracle Responsys Help Center].
