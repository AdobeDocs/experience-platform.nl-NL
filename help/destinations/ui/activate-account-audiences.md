---
title: Accountpubliek naar doelen activeren
type: Tutorial
description: Leer hoe u het publiek van een account activeert voor doelen
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 044306709747c32c4ce265d03d3908bbae169edc
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 0%

---

# Accountsoorten activeren

>[!AVAILABILITY]
>
>De functionaliteit om rekeningspubliek aan bestemmingen te activeren is beschikbaar voor bedrijven die [ zaken-aan-Zaken ](/help/rtcdp/overview.md#rtcdp-b2b) en [ zaken-aan-Persoon ](/help/rtcdp/overview.md#rtcdp-b2p) uitgaven van Real-Time Customer Data Platform kopen.

Dit artikel verklaart het werkschema wordt vereist om [ rekeningspubliek ](/help/segmentation/types/account-audiences.md) van Adobe Experience Platform naar uw aangewezen bestemming uit te voeren dat.

## Ondersteunde doelen {#supported-destinations}

Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer de tab **[!UICONTROL Catalog]** . Gebruik het filter **[!UICONTROL Data types]** en selecteer **[!UICONTROL Accounts]** om de doelen weer te geven die activering van accountsoorten ondersteunen. Momenteel, is het uitvoeren van rekeningspubliek beschikbaar slechts aan bepaalde wolkenopslagbestemmingen ([ Amazon S3 ](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ ADLS Gen 2 ](/help/destinations/catalog/cloud-storage/adls-gen2.md), [ Azure BlobOpslag ](/help/destinations/catalog/cloud-storage/azure-blob.md), [ Gegevens Landing Zone ](/help/destinations/catalog/cloud-storage/data-landing-zone.md), en [ SFTP ](/help/destinations/catalog/cloud-storage/sftp.md)) en [ Demandbase ](/help/destinations/catalog/advertising/demandbase.md) en [ (Bedrijven) LinkedIn De gestroomde bestemming van het publiek ](/help/destinations/catalog/social/linkedin-b2b.md) stromen.

![ Doelen die rekeningspubliek steunen.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Video-overzicht

Bekijk de onderstaande video voor een overzicht van het maken en activeren van accountsoorten en de ondersteunde gebruiksgevallen bij het activeren van accountsoorten.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Vereisten {#prerequisites}

* U moet eerst [ rekeningsprofielen ](/help/rtcdp/accounts/account-profile-overview.md) opnemen en [ rekeningspubliek ](/help/segmentation/types/account-audiences.md) creëren alvorens u hen aan stroomafwaartse bestemmingen kunt activeren.
* Als u het publiek van een account naar bestemmingen wilt activeren, moet u verbinding hebben met een doel. Als u dit niet reeds hebt gedaan, ga naar de [ bestemmingscatalogus ](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken. Lees het leerprogramma UI op [ verbindend met bestemmingen ](./connect-destination.md) voor meer informatie.

### Vereiste machtigingen {#permissions}

Om rekeningspubliek te activeren, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Activate Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Blader in de doelcatalogus om ervoor te zorgen dat u over de benodigde machtigingen beschikt om het accountpubliek te activeren. Als een bestemming een **[!UICONTROL Activate]** controle heeft, dan hebt u de aangewezen toestemmingen.

## Kies uw bestemming {#select-destination}

Volg de instructies om een bestemming te selecteren waar u uw datasets kunt uitvoeren:

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer de tab **[!UICONTROL Catalog]** .

   ![ de cataloguslusje van de Bestemming met benadrukte controle van de Catalogus.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate]** op de kaart die overeenkomt met het doel waarnaar u gegevenssets wilt exporteren.

>[!TIP]
>
>De bestemmingen die rekeningspubliek kunnen uitvoeren worden vermeld met een pictogram in de hogere juiste hoek van de kaart, gelijkend op de hieronder benadrukte bestemming, of u kunt de filter van het gegevenstype aan slechts vertoningsbestemmingen gebruiken die rekeningspubliek kunnen uitvoeren, zoals [ getoond hoger op de pagina ](#supported-destinations).

![ de bestemmingspagina van de Vereis die benadrukte profielpubliek kan uitvoeren.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. Selecteer **[!UICONTROL Data type Accounts]**, gevolgd door de doelverbinding waarnaar u gegevenssets wilt exporteren en selecteer vervolgens **[!UICONTROL Next]** .

>[!TIP]
> 
>Als u opstelling een nieuwe bestemming wilt om rekeningspubliek te activeren, selecteer **[!UICONTROL Configure new destination]** om [ te teweegbrengen verbind met bestemmings ](/help/destinations/ui/connect-destination.md) werkschema en [ uitgezochte rekeningen als gegevenstype ](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![ benadrukte het activeringswerkschema van de Bestemming met rekeningscontrole.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Ga aan de volgende sectie te werk aan [ selecteer uw rekeningspubliek ](#select-profile-audiences) voor de uitvoer.

## Uw accountpubliek selecteren {#select-account-audiences}

Gebruik de selectievakjes links van de namen van accountgebruikers om het publiek te selecteren dat u naar het doel wilt exporteren en selecteer vervolgens **[!UICONTROL Next]** . Merk op dat slechts *rekeningspubliek* in deze mening wordt getoond, en geen andere publiekstypes worden getoond.

![ de uitvoerwerkschema tonen van de Dataset die de Uitgezochte publieksstap tonen waar u kunt selecteren welk accountpubliek om uit te voeren.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planning en volgende stappen

Lees de zelfstudie over het activeren van gegevens naar bestandsbestemmingen voor de rest van de activeringsworkflow voor het exporteren van accountsoorten. Ga van de [ stap van de de uitvoeruitvoer van het programmapubliek ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) verder. Als u het publiek van de account activeert naar het doel van **[!UICONTROL (Companies) LinkedIn Matched Audiences]** , leest u de zelfstudie over het activeren van streaming doelen. Ga van de [ toewijzingsstap ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) verder.

>[!NOTE]
>
>Merk op dat in de het plannen stap wanneer het uitvoeren van rekeningspubliek naar de bestemmingen van de wolkenopslag, het werkschema om rekeningspubliek slechts te activeren u [ volledige dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) en [ stijgende dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _op een dagelijks programma_ toestaat uitvoeren. Uuruitvoer wordt niet ondersteund. **[!UICONTROL After audience evaluation]** is het enige ondersteunde evaluatietype.

## Belangrijke callouts en bekende beperkingen {#important-callouts-known-limitations}

Let op de volgende belangrijke callouts en bekende beperkingen voor de algemene beschikbaarheidsversie van de functionaliteit om accountpubliek te activeren.

### Vereiste toewijzingsparen in de toewijzingsstap bij het activeren van accountpubliek naar de **[!UICONTROL (Companies) LinkedIn Matched Audiences]** -bestemming {#required-mappings}

Houd er bij het activeren van het accountpubliek naar het **[!UICONTROL (Companies) LinkedIn Matched Audiences]** -doel rekening mee dat de volgende twee toewijzingsparen verplicht zijn om gegevens te exporteren:

![ LinkedIn afbeelding vereiste gebieden.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Source-veld | Doelveld |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (selecteer dit veld in de **[!UICONTROL Select Identity namespace]** -weergave wanneer u de **[!UICONTROL Target Field]** selecteert). <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om rekeningspubliek aan bestemmingen te activeren."){width="100" zoomable="yes"} |

### Handhaving van gegevensbeheer {#data-governance-enforcement}

De toestemming wordt afgedwongen op de persoon of het profielniveau voor *klant en vooruitgangspubliek*. Daarom [ wordt de evaluatie van het toestemmingsbeleid ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) momenteel niet gesteund wanneer het activeren van rekeningspubliek aan bestemmingen. In de revisiestap van de activeringsworkflow ziet u een grijs besturingselement voor **[!UICONTROL View applicable consent policies]** .

![ stap van het Overzicht van de activeer het werkschema van het rekeningspubliek met de controle van de toestemmingshandhaving grayed uit.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Andere mechanismen van het gegevensbeheer in Real-Time CDP zoals [ de controles van het het beleid van het gegevensgebruik ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) en [ op attribuut-gebaseerde toegangsbeheer ](/help/destinations/home.md#attribute-based-access) worden gesteund.
