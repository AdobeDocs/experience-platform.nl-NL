---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;oracle responsys bestemming
title: Verbinding oracle Responsys
description: Responsys is een marketingtool voor e-mailberichten voor marketingcampagnes over meerdere kanalen die door Oracle worden aangeboden om interacties via e-mail, mobiele apparaten, displays en sociale media te personaliseren.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# [!DNL Oracle Responsys] verbinding

## Overzicht {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) is een marketingtool voor e-mailberichten van bedrijven voor marketingcampagnes over meerdere kanalen die worden aangeboden door [!DNL Oracle] interacties personaliseren op e-mail, mobiel, beeldscherm en sociaal gebied.

Om publieksgegevens te verzenden naar [!DNL Oracle Responsys], moet u eerst [verbinden met de bestemming](#connect-destination) in Adobe Experience Platform, en vervolgens [een gegevensimport instellen](#import-data-into-responsys) vanaf uw opslaglocatie naar [!DNL Oracle Responsys].

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Deze bestemming steunt de activering van alle publiek dat door het Experience Platform wordt geproduceerd [Segmenteringsservice](../../../segmentation/home.md).

*Aanvullend* Deze bestemming ondersteunt ook de activering van het publiek zoals beschreven in de onderstaande tabel.

| Type publiek | Beschrijving |
---------|----------|
| Aangepaste uploads | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP adres lijst van gewenste personen {#allow-list}

Bij het vestigen van e-mail marketing bestemmingen met opslag SFTP, adviseert Adobe dat u bepaalde IP waaiers aan uw lijst van gewenste personen toevoegt.

Zie [IP adres lijst van gewenste personen voor bestemmingen SFTP](../cloud-storage/ip-address-allow-list.md) als u Adobe IPs aan uw lijst van gewenste personen moet toevoegen.

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

Dit doel ondersteunt de volgende verbindingstypen:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

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
* U kunt desgewenst een openbare sleutel met RSA-indeling toevoegen om versleuteling met PGP/GPG toe te voegen aan geëxporteerde bestanden onder de **[!UICONTROL Key]** sectie. Uw openbare sleutel moet worden geschreven als een [!DNL Base64] gecodeerde tekenreeks.
* **[!UICONTROL Name]**: Kies een relevante naam voor de bestemming.
* **[!UICONTROL Description]**: Voer een beschrijving in voor uw doel.
* **[!UICONTROL Folder Path]**: Geef het pad op in uw opslaglocatie waar Platform uw exportgegevens als CSV-bestanden indient.
* **[!UICONTROL File Format]**: Select **CSV** om CSV-bestanden naar uw opslaglocatie te exporteren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../../ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Doelkenmerken {#destination-attributes}

Wanneer u een publiek activeert naar dit doel, raadt Adobe u aan een unieke id te selecteren in uw [samenvoegingsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Selecteer de unieke id en andere XDM-velden die u naar het doel wilt exporteren. Raadpleeg voor meer informatie [best practices bij het activeren van doelgroepen naar marketingdoelen per e-mail](overview.md#best-practices).

## Geëxporteerde gegevens {#exported-data}

Voor [!DNL Oracle Responsys] doelen, Platform maakt een `.csv` in de opslaglocatie die u hebt opgegeven. Zie voor meer informatie over de bestanden [doelactivering controleren](../../ui/activate-batch-profile-destinations.md#verify) in de zelfstudie voor publieksactivering.

## Gegevensimport instellen in [!DNL Oracle Responsys] {#import-data-into-responsys}

Na verbinding [!DNL Platform] aan uw [!DNL SFTP] -opslag, moet u de gegevens die u importeert vanaf uw opslaglocatie naar [!DNL Oracle Responsys]. Ga voor meer informatie over het uitvoeren van deze taak naar [Contactpersonen of accounts importeren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in de [!DNL Oracle Responsys Help Center].
