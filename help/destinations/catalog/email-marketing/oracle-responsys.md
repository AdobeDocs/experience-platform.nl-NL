---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;oracle responsys bestemming
title: Verbinding oracle Responsys
description: Responsys is een marketingtool voor e-mailberichten voor marketingcampagnes over meerdere kanalen die door Oracle worden aangeboden om interacties via e-mail, mobiele apparaten, displays en sociale media te personaliseren.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# [!DNL Oracle Responsys] verbinding

## Overzicht {#overview}

[](https://www.oracle.com/cx/marketing/campaign-management/) Reageren op een marketingtool voor e-mailberichten van bedrijven voor marketingcampagnes over meerdere kanalen die worden aangeboden door interacties  [!DNL Oracle] te personaliseren voor e-mail, mobiele apparaten, displays en sociale media.

Als u segmentgegevens naar [!DNL Oracle Responsys] wilt verzenden, moet u eerst [verbinding maken met het doel](#connect-destination) in Adobe Experience Platform en vervolgens [een gegevensimport instellen](#import-data-into-responsys) vanaf uw opslaglocatie naar [!DNL Oracle Responsys].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Doel {#connect-destination} verbinden

Selecteer **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer **[!UICONTROL Connect destination]**.[!DNL Oracle Responsys]

![Verbinden met Responssys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

Als u in de stap **[!UICONTROL Account]** eerder een verbinding met uw bestemming voor cloudopslag hebt ingesteld, selecteert u **[!UICONTROL Existing Account]** en selecteert u een van uw bestaande verbindingen. U kunt ook **[!UICONTROL New Account]** selecteren om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Connect to destination]**. Voor [!DNL Oracle Responsys], kunt u tussen **[!UICONTROL SFTP with Password]** en **[!UICONTROL SFTP with SSH Key]** selecteren.

![Connect Resys-account](../../assets/catalog/email-marketing/oracle-responsys/connection-type.png)

Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Configure]**.

- Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL Password] verstrekken.
- Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username], en [!UICONTROL SSH Key] verstrekken.

U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan uw geëxporteerde bestanden onder de sectie **[!UICONTROL Key]**. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.

![Gegevens van Responsys invullen](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

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

![Basisinformatie van Responsys](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Klik op **[!UICONTROL Create destination]** nadat u de bovenstaande velden hebt ingevuld. Uw doel is nu verbonden en u kunt segmenten [activeren](../../ui/activate-destinations.md) aan de bestemming.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan [!DNL Oracle Responsys] bestemming, adviseert Adobe dat u een uniek herkenningsteken van uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, verwijs naar [Selecteer welke schemagebieden om als bestemmingsattributen in uw uitgevoerde dossiers te gebruiken](./overview.md#destination-attributes).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Oracle Responsys] bestemmingen, leidt het Platform tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in [!DNL Oracle Responsys] {#import-data-into-responsys}

Nadat u [!DNL Platform] hebt aangesloten op uw SFTP-opslag, moet u de gegevensimport vanaf uw opslaglocatie instellen op [!DNL Oracle Responsys]. Zie [Contactpersonen of accounts importeren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in [!DNL Oracle Responsys Help Center] voor meer informatie over het uitvoeren van deze taak.