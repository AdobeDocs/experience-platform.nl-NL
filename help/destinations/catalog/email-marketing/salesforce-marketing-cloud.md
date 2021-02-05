---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;salesforce;salesforce bestemming
title: Salesforce-verbindingsbestemming Marketing Cloud
seo-description: De Marketing Cloud van Salesforce is een digitale marketing reeks die vroeger als ExactTarget wordt bekend die u toestaat om reizen voor bezoekers en klanten te bouwen en aan te passen om hun ervaring te personaliseren.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud] verbinding

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) is een digitale marketingsuite die voorheen ExactTarget werd genoemd. Met deze suite kunt u reizen maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

Als u segmentgegevens naar [!DNL Salesforce Marketing Cloud] wilt verzenden, moet u eerst [het doel](#connect-destination) in het Platform verbinden en vervolgens [een gegevensimport](#import-data-into-salesforce) instellen vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Doel {#connect-destination} verbinden

Selecteer **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]**, selecteer [!DNL Salesforce Marketing Cloud] en selecteer **[!UICONTROL Doel verbinden]**.

![Verbinding maken met Salesforce](../../assets/catalog/email-marketing/salesforce/catalog.png)

Selecteer **[!UICONTROL Bestaande account]** in de stap **[!UICONTROL Verificatie]** als u eerder een verbinding met de bestemming voor cloudopslag had ingesteld, en selecteer een van uw bestaande verbindingen. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. Voor [!DNL Salesforce Marketing Cloud], kunt u tussen **[!UICONTROL SFTP met Wachtwoord]** en **[!UICONTROL SFTP met SSH Sleutel]** selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Verbinding maken met doel]**.

Voor **[!UICONTROL SFTP met Wachtwoord]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.

Voor **[!UICONTROL SFTP met SSH Key]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

![Salesforce-informatie invullen](../../assets/catalog/email-marketing/salesforce/account-info.png)

Vul in de stap **[!UICONTROL Setup]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
- **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
- **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
- **[!UICONTROL Pad naar]** map: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV- of tabgescheiden bestanden indient.
- **[!UICONTROL Bestandsindeling]**:  **** CSVor  **[!UICONTROL TAB_DELIMITED]**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

![Basisinformatie over Salesforce](../../assets/catalog/email-marketing/salesforce/basic-information.png)

Klik op **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld. Uw doel is nu verbonden en u kunt segmenten [activeren](../../ui/activate-destinations.md) aan de bestemming.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan [!DNL Salesforce Marketing Cloud] bestemming, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteer welke schemavelden als doelkenmerken in uw geëxporteerde bestanden moeten worden gebruikt](./overview.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Salesforce Marketing Cloud] bestemmingen, leidt het Platform tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Nadat u het Platform hebt aangesloten op uw [!DNL Amazon S3]- of SFTP-opslagruimte, moet u de gegevensimport instellen vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud]. Om te leren hoe te om dit te verwezenlijken, zie [Invoerend Abonnees in Marketing Cloud van een Dossier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in [!DNL Salesforce Help Center].