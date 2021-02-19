---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;oracle responsys bestemming
title: Oracle Responsys-verbinding
description: Responsys is een marketingtool voor e-mailberichten voor marketingcampagnes over meerdere kanalen die door Oracle worden aangeboden om interacties via e-mail, mobiele apparaten, displays en sociale media aan te passen.
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---


# [!DNL Oracle Responsys] verbinding

[](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) Reageren op een marketingtool voor e-mailberichten van bedrijven voor marketingcampagnes over meerdere kanalen die worden aangeboden door interacties  [!DNL Oracle] te personaliseren voor e-mail, mobiele apparaten, displays en sociale media.

Als u segmentgegevens naar [!DNL Oracle Responsys] wilt verzenden, moet u eerst [verbinding maken met het doel](#connect-destination) in Adobe Experience Platform en vervolgens [een gegevensimport instellen](#import-data-into-responsys) vanaf uw opslaglocatie naar [!DNL Oracle Responsys].

## Exporttype {#export-type}

**Op profiel gebaseerd**  - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met kenmerken selecteren van de workflow voor  [doelactivering](../../ui/activate-destinations.md#select-attributes).

## Doel {#connect-destination} verbinden

Selecteer **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]**, selecteer [!DNL Oracle Responsys] en selecteer **[!UICONTROL Doel verbinden]**.

![Verbinden met Responssys](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

Selecteer **[!UICONTROL Bestaande account]** in de stap **[!UICONTROL Verificatie]** als u eerder een verbinding met de bestemming voor cloudopslag had ingesteld, en selecteer een van uw bestaande verbindingen. U kunt ook **[!UICONTROL Nieuwe account]** selecteren om een nieuwe verbinding in te stellen. Vul de verificatiereferenties van uw account in en selecteer **[!UICONTROL Verbinding maken met doel]**. Voor [!DNL Oracle Responsys], kunt u tussen **[!UICONTROL SFTP met Wachtwoord]** en **[!UICONTROL SFTP met SSH Sleutel]** selecteren. Vul de informatie hieronder in, afhankelijk van uw verbindingstype, en selecteer **[!UICONTROL Verbinding maken met doel]**.

Voor **[!UICONTROL SFTP met Wachtwoord]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Wachtwoord verstrekken.

Voor **[!UICONTROL SFTP met SSH Key]** verbindingen, moet u Domein, Haven, Gebruikersnaam, en Sleutel van SSH verstrekken.

![Gegevens van Responsys invullen](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

Vul in de stap **[!UICONTROL Setup]** de relevante informatie voor uw bestemming in, zoals hieronder wordt getoond:
- **[!UICONTROL Naam]**: Kies een relevante naam voor de bestemming.
- **[!UICONTROL Omschrijving]**: Voer een beschrijving in voor uw bestemming.
- **[!UICONTROL Naam]** emmertje: Uw Amazon S3-emmertje, waar Platform de gegevensexport zal deponeren. De invoer moet tussen 3 en 63 tekens lang zijn. Moet beginnen en eindigen met een letter of cijfer. Moet alleen kleine letters, cijfers of afbreekstreepjes ( - ) bevatten. Mag niet als IP adres (bijvoorbeeld, 192.100.1.1) worden geformatteerd.
- **[!UICONTROL Pad naar]** map: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV- of tabgescheiden bestanden indient.
- **[!UICONTROL Bestandsindeling]**:  **** CSVor  **TAB_DELIMITED**. Selecteer de bestandsindeling die u naar de opslaglocatie wilt exporteren.
- **[!UICONTROL Handelingen]** voor marketing: Marketingsacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie de pagina [Gegevensbeheer in Adobe Experience Platform](../../../data-governance/policies/overview.md) voor meer informatie over marketingacties. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor informatie over de afzonderlijke door Adobe gedefinieerde marketingacties.

![Basisinformatie van Responsys](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Klik op **[!UICONTROL Doel maken]** nadat u de bovenstaande velden hebt ingevuld. Uw doel is nu verbonden en u kunt segmenten [activeren](../../ui/activate-destinations.md) aan de bestemming.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md) voor informatie over de workflow voor segmentactivering.

## Doelkenmerken {#destination-attributes}

Wanneer [het activeren van segmenten](../../ui/activate-destinations.md) aan [!DNL Oracle Responsys] bestemming, adviseren wij dat u een uniek herkenningsteken van uw [verenigingsschema](../../../profile/home.md#profile-fragments-and-union-schemas) selecteert. Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Zie [Selecteer welke schemavelden als doelkenmerken in uw geëxporteerde bestanden moeten worden gebruikt](./overview.md#destination-attributes) in E-mailmarketingdoelen voor meer informatie.

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Oracle Responsys] bestemmingen, leidt het Platform tot een lusje-afgebakend `.txt` of `.csv` dossier in de opslagplaats die u verstrekte. Voor meer informatie over de dossiers, zie [E-mail de bestemmingen van de Marketing en de opslagbestemmingen van de Wolk](../../ui/activate-destinations.md#esp-and-cloud-storage) in de zelfstudie van de segmentactivering.

## Gegevensimport instellen in [!DNL Oracle Responsys] {#import-data-into-responsys}

Nadat u het Platform hebt aangesloten op uw [!DNL Amazon S3]- of SFTP-opslagruimte, moet u de gegevensimport instellen vanaf uw opslaglocatie naar [!DNL Oracle Responsys]. Zie [Contactpersonen of accounts importeren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in [!DNL Oracle Responsys Help Center] voor meer informatie over het uitvoeren van deze taak.