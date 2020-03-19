---
title: Oracle Eloqua-bestemming
seo-title: Oracle Eloqua-bestemming
description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen bij het beheren van marketingcampagnes en het genereren van verkooplood.
seo-description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen bij het beheren van marketingcampagnes en het genereren van verkooplood.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Eloqua

## Overzicht

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en het genereren van verkooplood te beheren.

Als u gesegmenteerde gegevens naar Oracle Eloqua wilt verzenden, moet u eerst de bestemming [](#connect-destination) verbinden in het Adobe Real-time Customer Data Platform en vervolgens een gegevensimport [](#import-data-into-eloqua) instellen vanaf uw opslaglocatie naar Oracle Eloqua.

## Verbinden met doel {#connect-destination}

1. Selecteer vervolgens Oracle Eloqua in **[!UICONTROL Verbindingen > Doelen]** en selecteer **[!UICONTROL Connect-doel]**.

   ![Verbinden met Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. Selecteer in de wizard Connect-bestemming het type **[!UICONTROL Verbinding]** voor uw opslaglocatie. Voor Oracle Eloqua kunt u kiezen tussen **SFTP met wachtwoord** en **SFTP met SSH-sleutel**. Vul de informatie hieronder in, afhankelijk van het verbindingstype en selecteer **[!UICONTROL Connect]**.

   ![De wizard Eloqua instellen](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   Voor **SFTP met de verbindingen van het Wachtwoord** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **SFTP met SSH Zeer belangrijke** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

   ![Eloqua-informatie invullen](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. Vul in **Basisinformatie** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
   * **Naam**: Kies een relevante naam voor de bestemming.
   * **Omschrijving**: Voer een beschrijving in voor uw bestemming.
   * **Pad naar** map: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **Bestandsindeling**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
   ![Basisinformatie over Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. Klik op **Maken** nadat u de velden in de **basisinformatie** hebt ingevuld. Uw bestemming is nu verbonden en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de bestemming van Oracle Eloqua, adviseren wij dat u een uniek herkenningsteken van uw [unieschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Gegevensimport instellen in Oracle Eloqua {#import-data-into-eloqua}

Nadat u CDP in realtime hebt verbonden met uw Amazon S3- of SFTP-opslag, moet u de gegevensimport van uw opslaglocatie naar Oracle Eloqua instellen. Zie Contactpersonen of accounts [importeren in het Oracle Eloqua Help Center voor meer informatie over het](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) importeren van deze gegevens.