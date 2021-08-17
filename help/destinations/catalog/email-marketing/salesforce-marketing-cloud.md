---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;salesforce;salesforce bestemming
title: Verbinding met Salesforce-Marketing Cloud
seo-description: De Marketing Cloud van Salesforce is een digitale marketing reeks die vroeger als ExactTarget wordt bekend die u toestaat om reizen voor bezoekers en klanten te bouwen en aan te passen om hun ervaring te personaliseren.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] verbinding

## Overzicht {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) is een digitale marketingsuite die voorheen ExactTarget werd genoemd. Met deze suite kunt u reizen maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

Als u segmentgegevens naar [!DNL Salesforce Marketing Cloud] wilt verzenden, moet u eerst [het doel](#connect-destination) in het Platform verbinden en vervolgens [een gegevensimport](#import-data-into-salesforce) instellen vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## IP adres lijst van gewenste personen {#allow-list}

Bij het vestigen van e-mail marketing bestemmingen met opslag SFTP, adviseert Adobe dat u bepaalde IP waaiers aan uw lijst van gewenste personen toevoegt.

Verwijs naar [IP adreslijst van gewenste personen voor wolkenopslagbestemmingen ](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

Dit doel ondersteunt de volgende verbindingstypen:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u verstrekken:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u verstrekken:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]

* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan uw geëxporteerde bestanden onder de sectie **[!UICONTROL Key]**. Uw openbare sleutel moet als [!DNL Base64] gecodeerde koord worden geschreven.
* **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming.
* **[!UICONTROL Folder Path]**: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV- of tabgescheiden bestanden indient.
* **[!UICONTROL File Format]**:  **** CSVor  **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Segmenten naar dit doel activeren {#activate}

Zie [Profielen en segmenten activeren aan een doel](../../ui/activate-destinations.md) voor instructies bij het activeren van publiekssegmenten aan bestemmingen.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan deze bestemming, adviseert Adobe dat u een uniek herkenningsteken van uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Voor meer informatie, verwijs naar [Selecteer welke schemagebieden om als bestemmingsattributen in uw uitgevoerde dossiers te gebruiken](./overview.md#destination-attributes).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Salesforce Marketing Cloud] bestemmingen, leidt het Platform tot een lusje-afgebakend `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Nadat u [!DNL Platform] hebt aangesloten op uw [!DNL SFTP]-opslag, moet u de gegevensimport vanaf uw opslaglocatie instellen op [!DNL Salesforce Marketing Cloud]. Om te leren hoe te om dit te verwezenlijken, zie [Invoerend Abonnees in Marketing Cloud van een Dossier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in [!DNL Salesforce Help Center].
