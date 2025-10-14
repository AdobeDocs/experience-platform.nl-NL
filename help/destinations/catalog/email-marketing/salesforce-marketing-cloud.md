---
title: Salesforce Marketing Cloud-verbinding
description: Salesforce Marketing Cloud is een digitale marketingsuite die voorheen ExactTarget werd genoemd. Met deze suite kunt u reizen maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# [!DNL (Files) Salesforce Marketing Cloud] verbinding

## Overzicht {#overview}

[[!DNL Salesforce Marketing Cloud] &#x200B;](https://www.salesforce.com/products/marketing-cloud/email-marketing/) is een digitale marketing reeks die vroeger als ExactTarget wordt bekend die u toestaat om reizen voor bezoekers en klanten te bouwen en aan te passen om hun ervaring te personaliseren.

Om publieksgegevens naar [!DNL Salesforce Marketing Cloud] te verzenden, moet u eerst [&#x200B; met de bestemming &#x200B;](#connect-destination) in Experience Platform verbinden, en dan [&#x200B; opstelling een gegevensinvoer &#x200B;](#import-data-into-salesforce) van uw opslagplaats in [!DNL Salesforce Marketing Cloud].

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

Bij het opzetten van e-mail marketing bestemmingen met de opslag van SFTP, adviseert Adobe dat u bepaalde IP waaiers aan uw lijst van gewenste personen toevoegt.

Verwijs naar [&#x200B; IP adreslijst van gewenste personen voor bestemmingen SFTP &#x200B;](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven.

Dit doel ondersteunt de volgende verbindingstypen:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Verbindingsparameters {#parameters}

Terwijl [&#x200B; vestiging &#x200B;](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* Voor **[!UICONTROL SFTP with Password]** -verbindingen moet u het volgende opgeven:
   * **[!UICONTROL Domain]**: het IP-adres of de domeinnaam van uw SFTP-account;
   * **[!UICONTROL Port]**: de poort die wordt gebruikt door de opslaglocatie van uw SFTP;
   * **[!UICONTROL Username]**: De gebruikersnaam die u wilt aanmelden bij uw SFTP-opslaglocatie;
   * **[!UICONTROL Password]**: Het wachtwoord om u aan te melden bij uw SFTP-opslaglocatie.
* Voor **[!UICONTROL SFTP with SSH Key]** -verbindingen moet u het volgende opgeven:
   * **[!UICONTROL Domain]**: het IP-adres of de domeinnaam van uw SFTP-account;
   * **[!UICONTROL Port]**: de poort die wordt gebruikt door de opslaglocatie van uw SFTP;
   * **[!UICONTROL Username]**: De gebruikersnaam die u wilt aanmelden bij uw SFTP-opslaglocatie;
   * **[!UICONTROL SSH Key]**: De persoonlijke SSH-sleutel die wordt gebruikt om u aan te melden bij uw SFTP-opslaglocatie. De persoonlijke sleutel moet zijn opgemaakt als een Base64-gecodeerde tekenreeks en mag niet met een wachtwoord zijn beveiligd.

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

Voor [!DNL Salesforce Marketing Cloud] -doelen maakt Experience Platform een `.csv` -bestand in de opslaglocatie die u hebt opgegeven. Voor meer informatie over de dossiers, zie [&#x200B; de activering van het publiek &#x200B;](../../ui/activate-batch-profile-destinations.md#verify) in het leerprogramma van de publiekactivering verifiëren.

## Gegevensimport instellen in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Nadat u [!DNL Experience Platform] hebt verbonden met uw [!DNL SFTP] -opslag, moet u de gegevens die u wilt importeren vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud] instellen. Leren hoe te om dit te verwezenlijken, zie [&#x200B; het Invoeren Abonnees in Marketing Cloud van een Dossier &#x200B;](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) in [!DNL Salesforce Help Center].
