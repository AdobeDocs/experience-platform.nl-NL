---
keywords: email;Email;e-mail;email destinations;salesforce;salesforce destination
title: Salesforce-Marketing Cloud
seo-title: Salesforce-Marketing Cloud
description: De Marketing Cloud van Salesforce is een digitale marketing reeks die vroeger als ExactTarget wordt bekend die u toestaat om reizen voor bezoekers en klanten te bouwen en aan te passen om hun ervaring te personaliseren.
seo-description: De Marketing Cloud van Salesforce is een digitale marketing reeks die vroeger als ExactTarget wordt bekend die u toestaat om reizen voor bezoekers en klanten te bouwen en aan te passen om hun ervaring te personaliseren.
translation-type: tm+mt
source-git-commit: 67a353c950bef11ccbaa52c49d213f08449baa96
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## Overzicht

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) is een digitale marketingsuite die voorheen ExactTarget werd genoemd. Met deze suite kunt u reizen maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

Om segmentgegevens naar te verzenden [!DNL Salesforce Marketing Cloud], moet u eerst de bestemming [in Adobe in real time CDP](#connect-destination) verbinden, en dan [opstelling een gegevensinvoer](#import-data-into-salesforce) van uw opslagplaats in [!DNL Salesforce Marketing Cloud].

## Exporttype {#export-type}

**Op profiel gebaseerd** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor [doelactivering](/help/rtcdp/destinations/activate-destinations.md#select-attributes).

## Connect-doel {#connect-destination}

1. Selecteer in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** de optie [!DNL Salesforce Marketing Cloud]en selecteer vervolgens de **[!UICONTROL Connect-bestemming]**.

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

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](/help/rtcdp/destinations/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer het [activeren van segmenten](/help/rtcdp/destinations/activate-destinations.md) aan de [!DNL Salesforce Marketing Cloud] bestemming, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../profile/home.md#profile-fragments-and-union-schemas)selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteren welke schemavelden u als doelkenmerken wilt gebruiken in uw geëxporteerde bestanden](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Salesforce Marketing Cloud] bestemmingen, leidt Adobe in real time CDP tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie de bestemmingen van de Marketing van de [E-mail en de opslagbestemmingen](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) van de Wolk in de zelfstudie van de segmentactivering.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Salesforce_Marketing_Cloud_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## Gegevensimport instellen in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Nadat u CDP in realtime hebt verbonden met uw [!DNL Amazon S3] of SFTP-opslag, moet u de gegevensimport instellen vanaf uw opslaglocatie naar [!DNL Salesforce Marketing Cloud]. Leren hoe te om dit te verwezenlijken, zie het [Invoeren van Abonnees in Marketing Cloud van een Dossier](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in [!DNL Salesforce Help Center].