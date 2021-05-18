---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;adobe campagne;campagne
title: Adobe Campaign-verbinding
description: Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---

# Adobe Campaign-verbinding

## Overzicht {#overview}

Adobe Campaign is een reeks oplossingen die u helpen campagnes op al uw online en offlinekanalen te personaliseren en te leveren. Zie [Aan de slag met Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) voor meer informatie.

Als u segmentgegevens naar Adobe Campaign wilt verzenden, moet u eerst [de bestemming](#connect-destination) in Adobe Experience Platform verbinden en vervolgens [een gegevensimport](#import-data-into-campaign) instellen vanaf uw opslaglocatie naar Adobe Campaign.

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in de  **[!UICONTROL Select attributes]** stap van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## IP adres lijst van gewenste personen {#allow-list}

Bij het vestigen van e-mail marketing bestemmingen met opslag SFTP, adviseert Adobe dat u bepaalde IP waaiers aan uw lijst van gewenste personen toevoegt.

Verwijs naar [IP adreslijst van gewenste personen voor wolkenopslagbestemmingen ](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Doel {#connect-destination} verbinden

Selecteer in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** Adobe Campaign en selecteer **[!UICONTROL Configure]**.

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen [!UICONTROL Activate] en [!UICONTROL Configure] de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

![Verbinding maken met Adobe Campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Selecteer **[!UICONTROL Connection type]** voor uw opslaglocatie in de stap **[!UICONTROL Account]** van de Connect-doelworkflow. Voor Adobe Campaign kunt u kiezen tussen **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP with Password]**, **[!UICONTROL SFTP with SSH Key]** en **[!UICONTROL Azure Blob]**. De voorkeursmethode voor het verzenden van gegevens naar Adobe Campaign is [!DNL Amazon S3] of [!DNL Azure Blob]. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, dan uitgezocht **[!UICONTROL Connect]**.


![Wizard Campagne instellen](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Voor **[!UICONTROL Amazon S3]** verbindingen, moet u [!UICONTROL Access Key ID] en [!UICONTROL Secret Access Key] verstrekken.
- Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL Password] verstrekken.
- Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL SSH Key] verstrekken.
- Voor **[!UICONTROL Azure Blob]** verbindingen, moet u een verbindingskoord verstrekken.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan uw geëxporteerde bestanden onder de sectie **[!UICONTROL Key]**. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

![Campagnegegevens invullen](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Vul in **[!UICONTROL Account authentication]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
- **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
- **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming.
- **[!UICONTROL Bucket Name]**:  *Voor S3-verbindingen*. Ga de plaats van uw S3 emmer in waar [!DNL Platform] uw uitvoergegevens als CSV of lusje-afgebakende dossiers zal deponeren.
- **[!UICONTROL Folder Path]**: Geef het pad op uw opslaglocatie op waar uw exportgegevens als CSV- of tabgescheiden bestanden  [!DNL Platform] worden opgeslagen.
- **[!UICONTROL Container]**:  *Voor Blob-verbindingen*. De container die het blob-pad voor uw map bevat, bevindt zich in.
- **[!UICONTROL File Format]**:  **** CSVor  **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
- **[!UICONTROL Marketing actions]**: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie de pagina [Beleid voor gegevensgebruik overzicht](../../../data-governance/policies/overview.md) voor meer informatie over marketingacties.

![Basisinformatie over campagnes](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Selecteer **[!UICONTROL Create destination]** nadat u de bovenstaande velden hebt ingevuld. Uw doel is nu verbonden en u kunt segmenten [activeren](../../ui/activate-destinations.md) aan de bestemming.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan de bestemming van Adobe Campaign, Adobe adviseert dat u een uniek herkenningsteken van uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, verwijs naar [Selecteer welke schemagebieden om als bestemmingsattributen in uw uitgevoerde dossiers te gebruiken](./overview.md#destination-attributes).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Adobe Campaign] bestemmingen, [!DNL Platform] leidt tot een lusje-afgebakend `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Houd bij het uitvoeren van deze integratie rekening met de [!DNL SFTP]-opslaglimieten, opslaglimieten voor databases en limieten voor actieve profielen zoals vastgelegd in uw Adobe Campaign-contract.
>- U moet uw geëxporteerde segmenten in Adobe Campaign plannen, importeren en toewijzen met behulp van [!DNL Campaign]-workflows. Raadpleeg [Een terugkerende import instellen](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) in Adobe Campaign Classic-documentatie en [Informatie over gegevensbeheeractiviteiten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in Adobe Campaign Standard-documentatie.
>- De voorkeursmethode voor het verzenden van gegevens naar Adobe Campaign is [!DNL Amazon S3] of [!DNL Azure Blob].



Nadat u [!DNL Platform] hebt aangesloten op uw [!DNL Amazon S3]- of [!DNL Azure Blob]-opslagruimte, moet u de gegevensimport instellen vanaf uw opslaglocatie naar Adobe Campaign. Raadpleeg de volgende Adobe Campaign-documentatiepagina&#39;s voor meer informatie hierover:
- [Ga aan de slag met het importeren en ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) exporteren van gegevens en het laden van  [gegevens (bestand)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) in de Adobe Campaign Classic-documentatie.
- [Ga aan de slag met processen en ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) gegevensbeheer en  [het dossier van de ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) Lading in de documentatie van Adobe Campaign Standard.
