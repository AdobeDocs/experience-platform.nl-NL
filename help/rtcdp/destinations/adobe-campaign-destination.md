---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren.
seo-description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Adobe Campaign

## Overzicht

Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren. Zie [Informatie over Adobe Campaign Classic](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) voor meer informatie.

Als u segmentgegevens naar Adobe Campaign wilt verzenden, moet u eerst de bestemming [](#connect-destination) verbinden in het Platform voor realtime klantgegevens van Adobe en vervolgens een gegevensimport [](#import-data-into-campaign) instellen vanaf uw opslaglocatie naar Adobe Campaign.

## Connect-doel {#connect-destination}

1. Selecteer Adobe Campaign in **[!UICONTROL Verbindingen > Doelen]** en selecteer **[!UICONTROL Verbindingsbestemming]**.

   ![Verbinding maken met Adobe-campagne](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Selecteer in de Connect-doelworkflow het type **[!UICONTROL Verbinding]** voor uw opslaglocatie. Voor Adobe Campaign kunt u kiezen tussen **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP met wachtwoord]** en **[!UICONTROL SFTP met SSH-sleutel]**. Vul de informatie hieronder in, afhankelijk van het verbindingstype en selecteer vervolgens **[!UICONTROL Connect]**.

   ![Wizard Campagne instellen](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   Voor **[!UICONTROL Amazon S3]** -verbindingen moet u uw toegangstoets-id en de sleutel voor geheime toegang opgeven.
Voor **[!UICONTROL SFTP met de verbindingen van het Wachtwoord]** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **[!UICONTROL SFTP met SSH Zeer belangrijke]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

   ![Campagnegegevens invullen](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. Vul in **[!UICONTROL Basisinformatie]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
   * **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
   * **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
   * **[!UICONTROL Naam]** emmertje: *Voor S3-verbindingen*. Ga de plaats van uw S3 emmer in waar CDP in real time uw uitvoergegevens als CSV of lusje-afgebakende dossiers zal neerleggen.
   * **[!UICONTROL Pad naar]** map: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **[!UICONTROL Bestandsindeling]**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

   ![Basisinformatie over campagnes](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. Klik op **[!UICONTROL Maken]** nadat u de bovenstaande velden hebt ingevuld. Uw bestemming is nu verbonden en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken {#destination-attributes}

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de bestemming van Adobe Campaign, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.


## Gegevensimport instellen in Adobe Campaign {#import-data-into-campaign}

Nadat u CDP in realtime hebt verbonden met uw [!DNL Amazon S3] of SFTP-opslag, moet u de gegevensimport instellen vanaf uw opslaglocatie naar Adobe Campaign. Zie Gegevens [](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) importeren in de Help-documentatie van Adobe Campaign voor meer informatie over hoe u dit kunt bereiken.