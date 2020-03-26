---
title: Oracle Responsys-bestemming
seo-title: Oracle Responsys-bestemming
description: Responsys is een marketingtool voor e-mailberichten voor marketingcampagnes over meerdere kanalen die door Oracle worden aangeboden om interacties via e-mail, mobiele apparaten, displays en sociale media aan te passen.
seo-description: Responsys is een marketingtool voor e-mailberichten voor marketingcampagnes over meerdere kanalen die door Oracle worden aangeboden om interacties via e-mail, mobiele apparaten, displays en sociale media aan te passen.
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9

---


# Oracle Responsys

## Overzicht

[Responsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) is een marketingtool voor e-mailmarketing voor bedrijven die via verschillende kanalen marketingcampagnes aanbieden die Oracle aanbiedt om interacties te personaliseren voor e-mail, mobiele apparaten, displays en sociale media.

Om segmentgegevens naar Oracle Responsys te verzenden, moet u eerst [verbinding maken met de bestemming](#connect-destination) in het platform van de Gegevens van de Klant van Adobe Real-time, en dan [opstelling een gegevensimport](#import-data-into-responsys) van uw opslagplaats in Oracle Responsys.

## Connect-doel {#connect-destination}

1. Selecteer in **[!UICONTROL Connections > Destinations]** Oracle Responsys en selecteer vervolgens **[!UICONTROL Connect destination]**.

   ![Verbinden met Responssys](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. Als u in de stap **Verificatie** eerder een verbinding met uw bestemming voor cloudopslag hebt ingesteld, selecteert **[!UICONTROL Existing Account]** en selecteert u een van uw bestaande verbindingen. U kunt ook selecteren **[!UICONTROL New Account]** om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Connect to destination]**. Voor Oracle Responsys, kunt u tussen **SFTP met Wachtwoord** en **SFTP met SSH Sleutel** selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Connect to destination]**.

   Voor **SFTP met de verbindingen van het Wachtwoord** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **SFTP met SSH Zeer belangrijke** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

   ![Gegevens van Responsys invullen](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. In de stap van de **Opstelling** , vul de relevante informatie voor uw bestemming zoals hieronder getoond in:
   * **Naam**: Kies een relevante naam voor de bestemming.
   * **Omschrijving**: Voer een beschrijving in voor uw bestemming.
   * **Pad naar** map: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **Bestandsindeling**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
   ![Basisinformatie van Responsys](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. Klik op Doel **** maken nadat u de bovenstaande velden hebt ingevuld. Uw bestemming is nu verbonden en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken {#destination-attributes}

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de bestemming van Oracle Responsys, adviseren wij dat u een uniek herkenningsteken van uw [unieschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Gegevensimport instellen in Oracle Responsys {#import-data-into-responsys}

Nadat u CDP in realtime hebt verbonden met uw Amazon S3- of SFTP-opslag, moet u de gegevensimport vanaf uw opslaglocatie instellen in Oracle Responsys. Leren hoe te om dit te verwezenlijken, zie het [Importeren van contacten of rekeningen](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in het Centrum van de Hulp van Oracle Responsys.