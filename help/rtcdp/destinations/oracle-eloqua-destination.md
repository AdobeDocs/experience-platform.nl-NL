---
title: Oracle Eloqua-bestemming
seo-title: Oracle Eloqua-bestemming
description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen bij het beheren van marketingcampagnes en het genereren van verkooplood.
seo-description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen bij het beheren van marketingcampagnes en het genereren van verkooplood.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Oracle Eloqua

## Overzicht

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen marketingcampagnes en het genereren van verkooplood te beheren.

Als u gesegmenteerde gegevens naar Oracle Eloqua wilt verzenden, moet u eerst de bestemming [](#connect-destination) verbinden in het Adobe Real-time Customer Data Platform en vervolgens een gegevensimport [](#import-data-into-eloqua) instellen vanaf uw opslaglocatie naar Oracle Eloqua.

## Verbinden met doel {#connect-destination}

1. Selecteer in **[!UICONTROL Connections > Destinations]** Oracle Eloqua de optie **[!UICONTROL Connect destination]**.

   ![Verbinden met Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Als u in de **[!UICONTROL Authentication]** stap eerder een verbinding met de bestemming voor cloudopslag hebt ingesteld, selecteert **[!UICONTROL Existing Account]** en selecteert u een van de bestaande verbindingen. U kunt ook selecteren **[!UICONTROL New Account]** om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Connect to destination]**. Voor Oracle Eloqua kunt u kiezen tussen **[!UICONTROL SFTP with Password]** en **[!UICONTROL SFTP with SSH Key]**. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Connect to destination]**.

   Voor **[!UICONTROL SFTP with Password]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **[!UICONTROL SFTP with SSH Key]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel SSH verstrekken.

   ![De wizard Eloqua instellen](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. Vul in de **[!UICONTROL Setup]** stap de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
   * **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
   * **[!UICONTROL Description]**: Voer een beschrijving in voor uw bestemming.
   * **[!UICONTROL Folder Path]**: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **[!UICONTROL File Format]**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
   ![Basisinformatie over Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Klik **[!UICONTROL Create destination]** nadat u de bovenstaande velden hebt ingevuld. Uw bestemming wordt nu gecreeerd en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de bestemming van Oracle Eloqua, adviseren wij dat u een uniek herkenningsteken van uw [unieschema](../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Gegevensimport instellen in Oracle Eloqua {#import-data-into-eloqua}

Nadat u CDP in realtime hebt verbonden met uw Amazon S3- of SFTP-opslag, moet u de gegevensimport van uw opslaglocatie naar Oracle Eloqua instellen. Zie Contactpersonen of accounts [importeren in het Oracle Eloqua Help Center voor meer informatie over het](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) importeren van deze gegevens.