---
title: Adobe-campagne
seo-title: Adobe-campagne
description: De Campagne van Adobe is een reeks oplossingen die u helpen campagnes over al uw online en off-line kanalen personaliseren en leveren.
seo-description: De Campagne van Adobe is een reeks oplossingen die u helpen campagnes over al uw online en off-line kanalen personaliseren en leveren.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Adobe-campagne

## Overzicht

De Campagne van Adobe is een reeks oplossingen die u helpen campagnes over al uw online en off-line kanalen personaliseren en leveren. Zie [Informatie over Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) voor meer informatie.

Als u segmentgegevens wilt verzenden naar Adobe Campaign, moet u eerst een [verbinding maken met het doel](#connect-destination) in het Adobe Real-time Customer Data Platform en vervolgens een gegevensimport [](#import-data-into-campaign) instellen vanaf uw opslaglocatie naar de Adobe-campagne.

## Connect-doel {#connect-destination}

1. Selecteer in **[!UICONTROL Connections > Destinations]** Adobe Campaign en selecteer vervolgens **[!UICONTROL Connect destination]**.

   ![Verbinding maken met Adobe-campagne](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Selecteer in de Connect-doelworkflow de locatie **[!UICONTROL Connection type]** voor uw opslaglocatie. Voor Adobe-campagne kunt u kiezen tussen **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]** en **[!UICONTROL SFTP with SSH Key]**. Vul de informatie hieronder in, afhankelijk van het verbindingstype en selecteer vervolgens **[!UICONTROL Connect]**.

   ![Wizard Campagne instellen](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Voor **[!UICONTROL Amazon S3]** verbindingen, moet u uw Zeer belangrijke identiteitskaart van de Toegang en Geheime Sleutel van de Toegang verstrekken.
Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel SSH verstrekken.

   ![Campagnegegevens invullen](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Vul in **[!UICONTROL Basic Information]**, zoals hieronder wordt getoond, de relevante informatie voor uw bestemming in:
   * **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
   * **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming.
   * **[!UICONTROL Bucket Name]**: *Voor S3-verbindingen*. Ga de plaats van uw S3 emmer in waar CDP in real time uw uitvoergegevens als CSV of lusje-afgebakende dossiers zal neerleggen.
   * **[!UICONTROL Folder Path]**: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **[!UICONTROL File Format]**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
   ![Basisinformatie over campagnes](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Klik **[!UICONTROL Create]** nadat u de bovenstaande velden hebt ingevuld. Uw bestemming is nu verbonden en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken {#destination-attributes}

Wanneer u segmenten [](/help/rtcdp/destinations/activate-destinations.md) activeert naar de bestemming van de Campagne van Adobe, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.


## Gegevensimport instellen in Adobe-campagne {#import-data-into-campaign}

Nadat u CDP in realtime hebt verbonden met uw Amazon S3- of SFTP-opslag, moet u de gegevensimport instellen vanaf uw opslaglocatie naar de Adobe-campagne. Zie Gegevens [importeren in de documentatie bij de Help van Adobe Campagne voor meer informatie over het uitvoeren van dit](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) proces.