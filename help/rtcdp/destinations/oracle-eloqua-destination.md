---
title: Oracle Eloqua-bestemming
seo-title: Oracle Eloqua-bestemming
description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen bij het beheren van marketingcampagnes en het genereren van verkooplood.
seo-description: Oracle Eloqua is een SaaS-platform (software as a service) voor marketingautomatisering dat door Oracle wordt aangeboden en bedoeld is om B2B-marketers en -organisaties te helpen bij het beheren van marketingcampagnes en het genereren van verkooplood.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## Overzicht

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) is een softwareplatform als service (SaaS) voor het automatiseren van de marketing dat door [!DNL Oracle] die wordt aangeboden bedoeld om B2B-marketers en -organisaties te helpen marketing campagnes en verkooploodproductie te beheren.

Als u segmentgegevens naar wilt verzenden, moet u eerst de bestemming [!DNL Oracle Eloqua]in Adobe Real-time Customer Data Platform [verbinden en vervolgens een gegevensimport](#connect-destination) [instellen vanaf uw opslaglocatie naar](#import-data-into-eloqua) [!DNL Oracle Eloqua].

## Verbinden met doel {#connect-destination}

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de optie [!DNL Oracle Eloqua]en selecteer vervolgens de **[!UICONTROL Connect-bestemming]**.

   ![Verbinden met Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Als u in de stap **[!UICONTROL Verificatie]** eerder een verbinding met uw bestemming voor cloudopslag had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u een van uw bestaande verbindingen. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. Voor [!DNL Oracle Eloqua], kunt u tussen **[!UICONTROL SFTP met Wachtwoord]** en **[!UICONTROL SFTP met SSH Sleutel]** selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Verbinden met bestemming]**.

   Voor **[!UICONTROL SFTP met de verbindingen van het Wachtwoord]** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **[!UICONTROL SFTP met SSH Zeer belangrijke]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

   ![De wizard Eloqua instellen](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. In de stap van de **[!UICONTROL Opstelling]** , vul de relevante informatie voor uw bestemming zoals hieronder getoond in:
   * **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
   * **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
   * **[!UICONTROL Pad naar]** map: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **[!UICONTROL Bestandsindeling]**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

   ![Basisinformatie over Eloqua](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Klik op Doel **** maken nadat u de bovenstaande velden hebt ingevuld. Uw bestemming wordt nu gecreeerd en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de [!DNL Oracle Eloqua] bestemming, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Gegevensimport instellen in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Nadat u CDP in realtime hebt verbonden met uw Amazon S3- of SFTP-opslag, moet u de gegevensimport instellen vanaf uw opslaglocatie naar [!DNL Oracle Eloqua]. Leren hoe te om dit te verwezenlijken, zie het [Importeren van contacten of rekeningen](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center].