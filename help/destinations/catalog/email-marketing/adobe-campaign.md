---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren.
seo-description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---


# Adobe Campaign

## Overzicht

Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren. Zie [Informatie over Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) voor meer informatie.

Als u segmentgegevens naar Adobe Campaign wilt verzenden, moet u eerst de bestemming [](#connect-destination) verbinden in Real-time Customer Data Platform en vervolgens een gegevensimport [](#import-data-into-campaign) instellen vanaf uw opslaglocatie naar Adobe Campaign.

## Exporttype {#export-type}

**Op profiel gebaseerd** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Connect-doel {#connect-destination}

Selecteer Adobe Campaign in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** en selecteer **[!UICONTROL Verbindingsbestemming]**.

![Verbinding maken met Adobe-campagne](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Selecteer in de Connect-doelworkflow het type **[!UICONTROL Verbinding]** voor uw opslaglocatie. Voor Adobe Campaign kunt u kiezen tussen **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP met wachtwoord]** en **[!UICONTROL SFTP met SSH-sleutel]**. Vul de informatie hieronder in, afhankelijk van het verbindingstype en selecteer vervolgens **[!UICONTROL Connect]**.

![Wizard Campagne instellen](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Voor **[!UICONTROL Amazon S3]** -verbindingen moet u uw toegangstoets-id en de sleutel voor geheime toegang opgeven.
- Voor **[!UICONTROL SFTP met de verbindingen van het Wachtwoord]** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
- Voor **[!UICONTROL SFTP met SSH Zeer belangrijke]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan de geëxporteerde bestanden onder de sectie **[!UICONTROL Key]** . Merk op dat deze openbare sleutel **als Base64 gecodeerde koord moet** worden geschreven.

![Campagnegegevens invullen](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Vul in **[!UICONTROL Basisinformatie]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
- **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
- **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
- **[!UICONTROL Naam]** emmertje: *Voor S3-verbindingen*. Ga de plaats van uw S3 emmer in waar CDP in real time uw uitvoergegevens als CSV of lusje-afgebakende dossiers zal neerleggen.
- **[!UICONTROL Pad naar]** map: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
- **[!UICONTROL Bestandsindeling]**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

![Basisinformatie over campagnes](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Klik op **[!UICONTROL Maken]** nadat u de bovenstaande velden hebt ingevuld. Uw bestemming is nu verbonden en u kunt segmenten [aan de bestemming](../../ui/activate-destinations.md) activeren.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer het [activeren van segmenten](../../ui/activate-destinations.md) aan de bestemming van Adobe Campaign, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, zie [Uitgezocht welke schemagebieden als bestemmingsattributen in uw uitgevoerde dossiers](./overview.md#destination-attributes) in e-mail marketing bestemmingsdocumentatie te gebruiken.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Adobe Campaign] bestemmingen, leidt in real time CDP tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie de bestemmingen van de Marketing van de [E-mail en de opslagbestemmingen](../../ui/activate-destinations.md#esp-and-cloud-storage) van de Wolk in de zelfstudie van de segmentactivering.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Adobe_Campaign_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Adobe_Campaign_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Gegevensimport instellen in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Houd bij het uitvoeren van deze integratie rekening met de opslaglimieten van SFTP, de opslaglimieten van de database en de limieten van het actieve profiel zoals vastgelegd in uw Adobe Campaign-contract.
>- U moet uw geëxporteerde segmenten in Adobe Campaign plannen, importeren en toewijzen met behulp van [!DNL Campaign] workflows. Raadpleeg [Een terugkerende importbewerking](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) instellen in de Adobe Campaign-documentatie.



Nadat u CDP in realtime hebt verbonden met uw [!DNL Amazon S3] of SFTP-opslag, moet u de gegevensimport instellen vanaf uw opslaglocatie naar Adobe Campaign. Raadpleeg Gegevens [](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) importeren in de documentatie van Adobe Campaign voor meer informatie over hoe u dit kunt bereiken.