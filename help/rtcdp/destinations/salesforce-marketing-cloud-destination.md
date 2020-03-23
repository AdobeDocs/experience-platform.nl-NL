---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud is een digitale marketingsuite die voorheen ExactTarget werd genoemd en waarmee u ritten kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.
seo-description: Salesforce Marketing Cloud is een digitale marketingsuite die voorheen ExactTarget werd genoemd en waarmee u ritten kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Overzicht

[De Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) is een digitale marketingsuite die voorheen ExactTarget werd genoemd en waarmee u ritten kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

Als u segmentgegevens naar Salesforce Marketing Cloud wilt verzenden, moet u eerst de bestemming [in Adobe Real-time CDP](#connect-destination) verbinden en vervolgens een gegevensimport [](#import-data-into-salesforce) instellen vanaf uw opslaglocatie naar Salesforce Marketing Cloud.

## Connect-doel {#connect-destination}

1. Selecteer **[!UICONTROL Connections > Destinations]** Salesforce Marketing Cloud in en selecteer vervolgens **[!UICONTROL Connect destination]**.

   ![Verbinding maken met Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Selecteer in de Connect-doelwizard de locatie **[!UICONTROL Connection type]** voor uw opslaglocatie. Voor de Marketing Cloud van Salesforce, kunt u tussen **SFTP met Wachtwoord** en **SFTP met de Sleutel** van SSH selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Connect]**.

   ![De wizard Salesforce instellen](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Voor **SFTP met de verbindingen van het Wachtwoord** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **SFTP met SSH Zeer belangrijke** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

   ![Salesforce-informatie invullen](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. Vul in **Basisinformatie** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
   * **Naam**: Kies een relevante naam voor de bestemming.
   * **Omschrijving**: Voer een beschrijving in voor uw bestemming.
   * **Pad naar** map: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **Bestandsindeling**: **CSV** of **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
   ![Basisinformatie over Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Klik op **Maken** nadat u de velden in de **basisinformatie** hebt ingevuld. Uw bestemming is nu verbonden en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken {#destination-attributes}

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de bestemming van de Wolk van de Marketing Salesforce, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Gegevensimport instellen in Salesforce Marketing Cloud {#import-data-into-salesforce}

Nadat u CDP in realtime hebt verbonden met uw Amazon S3- of SFTP-opslag, moet u de gegevensimport vanaf uw opslaglocatie instellen op Salesforce Marketing Cloud. Zie Abonnees [importeren in Marketing Cloud vanuit een bestand](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) in het Help Center van Salesforce voor meer informatie over het uitvoeren van dit proces.