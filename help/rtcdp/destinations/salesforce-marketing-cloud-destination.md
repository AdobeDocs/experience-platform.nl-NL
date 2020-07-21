---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud is een digitale marketingsuite die voorheen ExactTarget werd genoemd en waarmee u ritten kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.
seo-description: Salesforce Marketing Cloud is een digitale marketingsuite die voorheen ExactTarget werd genoemd en waarmee u ritten kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## Overzicht

[!DNL Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) is een digitale marketingsuite die voorheen ExactTarget werd genoemd. Met deze suite kunt u reizen maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

Als u segmentgegevens naar wilt verzenden, moet u eerst de bestemming [!DNL Salesforce Marketing Cloud]in Adobe Real-time CDP [verbinden en vervolgens een gegevensimport](#connect-destination) [instellen vanaf uw opslaglocatie naar](#import-data-into-salesforce) [!DNL Salesforce Marketing Cloud].

## Connect-doel {#connect-destination}

1. Selecteer in **[!UICONTROL Verbindingen > Doelen]** de optie [!DNL Salesforce Marketing Cloud]en selecteer vervolgens de **[!UICONTROL Connect-bestemming]**.

   ![Verbinding maken met Salesforce](/help/rtcdp/destinations/assets/connect-salesforce.png)

2. Als u in de stap **[!UICONTROL Verificatie]** eerder een verbinding met uw bestemming voor cloudopslag had ingesteld, selecteert u **[!UICONTROL Bestaande account]** en selecteert u een van uw bestaande verbindingen. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. Voor [!DNL Salesforce Marketing Cloud], kunt u tussen **[!UICONTROL SFTP met Wachtwoord]** en **[!UICONTROL SFTP met SSH Sleutel]** selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Verbinden met bestemming]**.

   Voor **[!UICONTROL SFTP met de verbindingen van het Wachtwoord]** , moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.
Voor **[!UICONTROL SFTP met SSH Zeer belangrijke]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

   ![Salesforce-informatie invullen](/help/rtcdp/destinations/assets/salesforce-authenticate.png)

3. In de stap van de **[!UICONTROL Opstelling]** , vul de relevante informatie voor uw bestemming zoals hieronder getoond in:
   * **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
   * **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
   * **[!UICONTROL Pad naar]** map: Geef het pad op in de opslaglocatie waar CDP in realtime uw exportgegevens als CSV- of tabgescheiden bestanden indient.
   * **[!UICONTROL Bestandsindeling]**: **[!UICONTROL CSV]** of **[!UICONTROL TAB_DELIMITED]**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.

   ![Basisinformatie over Salesforce](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

4. Klik op Doel **** maken nadat u de bovenstaande velden hebt ingevuld. Uw bestemming is nu verbonden en u kunt segmenten [aan de bestemming](/help/rtcdp/destinations/activate-destinations.md) activeren.

## Doelkenmerken {#destination-attributes}

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de [!DNL Salesforce Marketing Cloud] bestemming, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Gegevensimport instellen in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Nadat u CDP in realtime hebt verbonden met uw Amazon S3- of SFTP-opslag, moet u de gegevensimport instellen vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud]. Zie Abonnees [importeren in Marketing Cloud vanuit een bestand](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in de [!DNL Salesforce Help Center]app voor meer informatie over het uitvoeren van dit proces.