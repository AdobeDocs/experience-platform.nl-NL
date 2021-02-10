---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;oracle eloqua;oracle
title: Oracle Eloqua-verbinding
description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en het genereren van verkoopleads te beheren.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# [!DNL Oracle Eloqua] verbinding

[[!DNL Oracle Eloqua]](https://www.oracle.com/marketingcloud/products/marketing-automation/) is een softwareplatform als service (SaaS) voor marketingautomatisering dat wordt aangeboden door  [!DNL Oracle] die bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en productie van verkooplood te beheren.

Als u segmentgegevens naar [!DNL Oracle Eloqua] wilt verzenden, moet u eerst [het doel](#connect-destination) in Adobe Experience Platform verbinden en vervolgens [een gegevensimport](#import-data-into-eloqua) instellen vanaf uw opslaglocatie naar [!DNL Oracle Eloqua].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Verbinden met doel {#connect-destination}

Selecteer **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]**, selecteer [!DNL Oracle Eloqua] en selecteer **[!UICONTROL Doel verbinden]**.

[Verbinden met Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Selecteer **[!UICONTROL Bestaande account]** in de stap **[!UICONTROL Verificatie]** als u eerder een verbinding met de bestemming voor cloudopslag had ingesteld, en selecteer een van uw bestaande verbindingen. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. Voor [!DNL Oracle Eloqua], kunt u tussen **[!UICONTROL SFTP met Wachtwoord]** en **[!UICONTROL SFTP met SSH Sleutel]** selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Verbinding maken met doel]**.

Voor **[!UICONTROL SFTP met Wachtwoord]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **[!UICONTROL SFTP met SSH Key]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

![De wizard Eloqua instellen](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

Vul in de stap **[!UICONTROL Setup]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
- **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
- **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
- **[!UICONTROL Pad naar]** map: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV- of tabgescheiden bestanden indient.
- **[!UICONTROL Bestandsindeling]**:  **** CSVor  **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

![Basisinformatie over Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Klik op **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld. Uw bestemming wordt nu gecreeerd en u kunt segmenten [activeren ](../../ui/activate-destinations.md) aan de bestemming.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan [!DNL Oracle Eloqua] bestemming, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteer welke schemavelden als doelkenmerken in uw geëxporteerde bestanden moeten worden gebruikt](./overview.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Oracle Eloqua] bestemmingen, leidt het Platform tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Nadat u het Platform hebt aangesloten op uw Amazon S3- of SFTP-opslagruimte, moet u de gegevensimport vanaf uw opslaglocatie instellen op [!DNL Oracle Eloqua]. Zie [Contactpersonen of accounts importeren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center] voor meer informatie over het uitvoeren van deze taak.