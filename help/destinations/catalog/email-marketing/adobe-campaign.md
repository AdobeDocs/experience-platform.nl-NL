---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;adobe campagne;campagne
title: Adobe Campaign-verbinding
description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---


# Adobe Campaign-verbinding

Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren. Zie [Informatie over Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) voor meer informatie.

Als u segmentgegevens naar Adobe Campaign wilt verzenden, moet u eerst [de bestemming](#connect-destination) in Adobe Experience Platform verbinden en vervolgens [een gegevensimport](#import-data-into-campaign) instellen vanaf uw opslaglocatie naar Adobe Campaign.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Doel {#connect-destination} verbinden

Selecteer in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** Adobe Campaign en selecteer vervolgens **[!UICONTROL Doel verbinden]**.

![Verbinding maken met Adobe-campagne](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Selecteer in de Connect-doelworkflow het type **[!UICONTROL Verbinding]** voor uw opslaglocatie. Voor Adobe Campaign kunt u kiezen tussen **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP met wachtwoord]**, **[!UICONTROL SFTP met SSH Key]** en **[!UICONTROL Azure Blob]**. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer dan **[!UICONTROL Connect]**.

![Wizard Campagne instellen](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Voor **[!UICONTROL Amazon S3]** verbindingen, moet u uw Zeer belangrijke identiteitskaart van de Toegang en Geheime Sleutel van de Toegang verstrekken.
- Voor **[!UICONTROL SFTP met Wachtwoord]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
- Voor **[!UICONTROL SFTP met SSH Key]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.
- Voor **[!UICONTROL Azure Blob]**-verbindingen moet u een verbindingstekenreeks opgeven.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan uw geëxporteerde bestanden onder de sectie **[!UICONTROL Key]**. Merk op dat deze openbare sleutel **must** als Base64 wordt geschreven gecodeerd koord.

![Campagnegegevens invullen](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Vul in **[!UICONTROL Basisinformatie]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
- **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
- **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
- **[!UICONTROL Naam]** emmertje:  *Voor S3-verbindingen*. Voer de locatie van uw S3-emmertje in waar Platform uw exportgegevens als CSV- of tabgescheiden bestanden indient.
- **[!UICONTROL Pad naar]** map: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV- of tabgescheiden bestanden indient.
- **[!UICONTROL Container]**:  *Voor Blob-verbindingen*. De container die het blob-pad voor uw map bevat, bevindt zich in.
- **[!UICONTROL Bestandsindeling]**:  **** CSVor  **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

![Basisinformatie over campagnes](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Klik op **[!UICONTROL Maken]** nadat u de bovenstaande velden hebt ingevuld. Uw doel is nu verbonden en u kunt segmenten [activeren](../../ui/activate-destinations.md) aan de bestemming.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan de bestemming van Adobe Campaign, adviseren wij dat u een uniek herkenningsteken van uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, zie [Selecteer welke schemagebieden als bestemmingsattributen in uw uitgevoerde dossiers ](./overview.md#destination-attributes) in e-mail marketing bestemmingsdocumentatie te gebruiken.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Adobe Campaign] bestemmingen, leidt het Platform tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Houd bij het uitvoeren van deze integratie rekening met de opslaglimieten van SFTP, de opslaglimieten van de database en de limieten van het actieve profiel zoals vastgelegd in uw Adobe Campaign-contract.
>- U moet uw geëxporteerde segmenten in Adobe Campaign plannen, importeren en toewijzen met behulp van [!DNL Campaign]-workflows. Raadpleeg [Herhalende importbewerkingen instellen](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) in Adobe Campaign-documentatie.



Nadat u het Platform hebt aangesloten op uw [!DNL Amazon S3]- of SFTP-opslagruimte, moet u de gegevensimport instellen vanaf uw opslaglocatie naar Adobe Campaign. Raadpleeg [Gegevens importeren](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) in de documentatie van Adobe Campaign voor meer informatie over het uitvoeren van dit project.