---
title: Activeren het potentiële publiek aan bestemmingen
type: Tutorial
description: Leer hoe te om perspectiefpubliek aan bestemmingen te activeren
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Perspectiefpubliek activeren

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die het Real-Time CDP-pakket Premier en Ultimate hebben aangeschaft. Neem contact op met uw Adobe voor meer informatie.

Dit artikel verklaart het werkschema wordt vereist om [ perspectiefpubliek ](/help/segmentation/ui/prospect-audience.md) van Adobe Experience Platform naar uw aangewezen bestemming uit te voeren dat.

## Ondersteunde doelen {#supported-destinations}

Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer de tab **[!UICONTROL Catalog]** . Gebruik het filter **[!UICONTROL Data types]** en selecteer **[!UICONTROL Prospects]** om de bestemmingen te zien die de activering van perspectiefpubliek steunen. Op dit moment is het exporteren van mogelijke doelgroepen alleen beschikbaar voor cloudopslagdoelen.

![ Doelen die vooruitgangspubliek steunen.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Vereisten {#prerequisites}

* U moet [ perspectiefprofielen ](/help/profile/ui/prospect-profile.md) eerst opnemen en [ perspectiefpubliek ](/help/segmentation/ui/prospect-audience.md) creëren alvorens u hen aan stroomafwaartse bestemmingen kunt activeren.
* Om perspectiefpubliek aan bestemmingen te activeren, moet u met succes met een bestemming verbonden hebben. Als u dit niet reeds hebt gedaan, ga naar de [ bestemmingscatalogus ](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken. Lees het leerprogramma UI op [ verbindend met bestemmingen ](./connect-destination.md) voor meer informatie.

### Vereiste machtigingen {#permissions}

Om perspectiefpubliek te activeren, hebt u de **[!UICONTROL View Destinations]** en **[!UICONTROL Activate Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om ervoor te zorgen dat u de noodzakelijke toestemmingen hebt om perspectiefpubliek te activeren, doorblader de bestemmingscatalogus. Als een bestemming een **[!UICONTROL Activate]** controle heeft, dan hebt u de aangewezen toestemmingen.

## Kies uw bestemming {#select-destination}

Volg de instructies om een bestemming te selecteren waar u uw datasets kunt uitvoeren:

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer de tab **[!UICONTROL Catalog]** .

   ![ de cataloguslusje van de Bestemming met benadrukte controle van de Catalogus.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Selecteer **[!UICONTROL Activate]** op de kaart die overeenkomt met het doel waarnaar u gegevenssets wilt exporteren.

>[!TIP]
>
>De bestemmingen die profielpubliek kunnen uitvoeren worden vermeld met een pictogram in de hogere juiste hoek van de kaart, gelijkend op de hieronder benadrukte bestemming, of u kunt de filter van het gegevenstype aan slechts vertoningsbestemmingen gebruiken die vooruitgangspubliek kunnen uitvoeren, zoals [ getoond hoger op de pagina ](#supported-destinations).

![ de bestemmingspagina van Amazon S3 die benadrukte profielpubliek kan uitvoeren.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Selecteer **[!UICONTROL Data type Prospects]**, gevolgd door de doelverbinding waarnaar u gegevenssets wilt exporteren en selecteer vervolgens **[!UICONTROL Next]** .

>[!TIP]
> 
>Als u opstelling een nieuwe bestemming wilt om perspectiefpubliek te activeren, uitgezocht **[!UICONTROL Configure new destination]** om [ te teweegbrengen verbind met bestemmings ](/help/destinations/ui/connect-destination.md) werkschema.

![ benadrukte het activeringswerkschema van de Bestemming met de controle van Vooruitzichten.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Ga aan de volgende sectie te werk aan [ selecteer uw profielpubliek ](#select-profile-audiences) voor de uitvoer.

## Selecteer een publiek met perspectief {#select-prospect-audiences}

Gebruik de selectievakjes links van de namen van de mogelijke doelgroepen om het publiek te selecteren dat u naar het doel wilt exporteren en selecteer vervolgens **[!UICONTROL Next]** . Merk op dat slechts het potentiële publiek in deze mening wordt getoond, en geen ander publiek wordt getoond.

![ de uitvoerwerkschema tonen van de Dataset die de Uitgezochte publieksstap tonen waar u kunt selecteren welk vooruitgangspubliek om uit te voeren.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planning en volgende stappen

Voor de rest van het activeringswerkschema om perspectiefpubliek uit te voeren, lees het leerprogramma over het activeren van gegevens aan dossier-gebaseerde bestemmingen. Ga van de [ stap van de de uitvoeruitvoer van het programmapubliek ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) verder.

>[!NOTE]
>
>Merk op dat in de het plannen stap, het werkschema om perspectiefpubliek slechts te activeren u [ volledige dossiers ](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) uitvoeren. Incrementele bestandsexport wordt niet ondersteund.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Andere gebruiksgevallen die worden bereikt via ondersteuning van partnergegevens {#other-use-cases}

Verken verdere gebruiksgevallen die door de steun van partnergegevens in Real-Time CDP worden toegelaten:

* [ Supplement eerste-partijprofielen met attributen van vertrouwde op gegevenspartners ](/help/rtcdp/partner-data/supplement-first-party-profiles.md) om uw gegevensstichting te verbeteren en nieuwe inzichten in uw klantenbasis te verkrijgen en betere publieksoptimalisering te bereiken.
* De steun van de derdegegevens van het gebruik in Real-Time CDP om [ uw profielbasis met perspectiefprofielen van gegevenspartners uit te breiden en met hen in gesprek te gaan om nieuwe klanten ](/help/rtcdp/partner-data/prospecting.md) te verwerven of te bereiken.
* [ de partner van de Leverage verleende erkenning voor het personaliseren van ervaringen ter plaatse ](/help/rtcdp/partner-data/onsite-personalization.md) tijdens het bezoek zonder de gebruiker voor authentiek verklaren of het hebben van vroegere geschiedenis met uw merk.
