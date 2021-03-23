---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;oracle eloqua;oracle
title: Oracle Eloqua-verbinding
description: Oracle Eloqua is een softwareplatform als service (SaaS) voor marketingautomatisering dat door Oracle wordt aangeboden en dat bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en het genereren van verkooplood te beheren.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# [!DNL Oracle Eloqua] verbinding

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) is een softwareplatform als service (SaaS) voor marketingautomatisering dat wordt aangeboden door  [!DNL Oracle] die bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en productie van verkooplood te beheren.

Als u segmentgegevens naar [!DNL Oracle Eloqua] wilt verzenden, moet u eerst [het doel](#connect-destination) in Adobe Experience Platform verbinden en vervolgens [een gegevensimport](#import-data-into-eloqua) instellen vanaf uw opslaglocatie naar [!DNL Oracle Eloqua].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Verbinden met doel {#connect-destination}

Selecteer **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer **[!UICONTROL Configure]**.[!DNL Oracle Eloqua]

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen [!UICONTROL Activate] en [!UICONTROL Configure] de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.

![Verbinden met Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Als u in de stap **[!UICONTROL Account]** eerder een verbinding met uw bestemming voor cloudopslag hebt ingesteld, selecteert u **[!UICONTROL Existing Account]** en selecteert u een van uw bestaande verbindingen. U kunt ook **[!UICONTROL New Account]** selecteren om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Connect to destination]**. Voor [!DNL Oracle Eloqua], kunt u tussen **[!UICONTROL SFTP with Password]** en **[!UICONTROL SFTP with SSH Key]** selecteren.

![Connect Eloqua-account](../../assets/catalog/email-marketing/oracle-eloqua/connection-type.png)

Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Connect to destination]**.

- Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL Password] verstrekken.
- Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL SSH Key] verstrekken.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan uw geëxporteerde bestanden onder de sectie **[!UICONTROL Key]**. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

![Eloqua-verbinding met doel](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

Vul in de stap **[!UICONTROL Authentication]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
- **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
- **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming.
- **[!UICONTROL Folder Path]**: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV- of tabgescheiden bestanden indient.
- **[!UICONTROL File Format]**:  **** CSVor  **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
- **[!UICONTROL Marketing actions]**: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Voor meer informatie over marketing acties, zie [Overzicht van het beleid van het gebruik van Gegevens](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Basisinformatie over Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Klik op **[!UICONTROL Create destination]** nadat u de bovenstaande velden hebt ingevuld. Uw bestemming wordt nu gecreeerd en u kunt segmenten [activeren ](../../ui/activate-destinations.md) aan de bestemming.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan [!DNL Oracle Eloqua] bestemming, adviseert Adobe dat u een uniek herkenningsteken van uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, verwijs naar [Selecteer welke schemagebieden om als bestemmingsattributen in uw uitgevoerde dossiers te gebruiken](./overview.md#destination-attributes).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Oracle Eloqua] bestemmingen, leidt het Platform tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Nadat u [!DNL Platform] hebt aangesloten op uw SFTP-opslag, moet u de gegevensimport vanaf uw opslaglocatie instellen op [!DNL Oracle Eloqua]. Zie [Contactpersonen of accounts importeren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center] voor meer informatie over het uitvoeren van deze taak.