---
title: Activeren het potentiële publiek aan bestemmingen
type: Tutorial
hide: true
hidefromtoc: true
description: Leer hoe te om perspectiefpubliek aan bestemmingen te activeren
source-git-commit: e04d7a3cd75f4e61329a2de8ca5ddcc4d9518a57
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Perspectiefpubliek activeren

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die het Real-Time CDP-pakket Premier en Ultimate hebben aangeschaft. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.

In dit artikel wordt uitgelegd welke workflow nodig is om te exporteren [publiek perspectief](/help/segmentation/ui/prospect-audience.md) van Adobe Experience Platform naar uw voorkeursbestemming.

## Ondersteunde doelen {#supported-destinations}

Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab. Gebruik de **[!UICONTROL Data types]** filter en selecteer **[!UICONTROL Prospects]** de bestemmingen te zien die de activering van het beoogde publiek ondersteunen. Op dit moment is het exporteren van mogelijke doelgroepen alleen beschikbaar voor de [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) bestemming.

![Doelen die de uitvoer van gegevenssets ondersteunen](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Vereisten {#prerequisites}

* U moet eerst innemen [perspectiefprofielen](/help/profile/ui/prospect-profile.md) en maken [publiek perspectief](/help/segmentation/ui/prospect-audience.md) voordat u ze kunt activeren naar downstreamdoelen.
* Om perspectiefpubliek aan bestemmingen te activeren, moet u met succes met een bestemming verbonden hebben. Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken. De zelfstudie UI lezen op [verbinden met bestemmingen](./connect-destination.md) voor meer informatie .

### Vereiste machtigingen {#permissions}

Als u een publiek met perspectief wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Om ervoor te zorgen dat u de noodzakelijke toestemmingen hebt om perspectiefpubliek te activeren, doorblader de bestemmingscatalogus. Als een doel een **[!UICONTROL Activate]** controle, dan hebt u de aangewezen toestemmingen.

## Kies uw bestemming {#select-destination}

Volg de instructies om een bestemming te selecteren waar u uw datasets kunt uitvoeren:

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus met besturingselement Catalogus gemarkeerd.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Selecteren **[!UICONTROL Activate]** op de kaart die aan de bestemming beantwoordt dat u datasets naar wilt uitvoeren.

>[!TIP]
>
>De bestemmingen die profielpubliek kunnen uitvoeren zijn vermeld met een pictogram in de hogere juiste hoek van de kaart, gelijkend op de hieronder benadrukte bestemming, of u kunt de filter van het gegevenstype gebruiken om bestemmingen slechts te tonen die potentiële publiek, zoals kunnen uitvoeren [hoger weergegeven op de pagina](#supported-destinations).

![Amazon S3 bestemmingspagina die gemarkeerde profielsoorten kan exporteren.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Selecteren **[!UICONTROL Data type Prospects]**, gevolgd door de doelverbinding waarnaar u datasets wilt exporteren, en vervolgens selecteren **[!UICONTROL Next]**.

>[!TIP]
> 
>Als u opstelling een nieuwe bestemming wilt om perspectiefpubliek te activeren, selecteer **[!UICONTROL Configure new destination]** om de [Verbinden met doel](/help/destinations/ui/connect-destination.md) workflow.

![Workflow voor doelactivering met besturingselement voor vooruitzichten gemarkeerd.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Ga naar de volgende sectie tot [uw profielpubliek selecteren](#select-profile-audiences) voor uitvoer.

## Selecteer een publiek met perspectief {#select-prospect-audiences}

Gebruik de controledozen links van de namen van het perspectiefpubliek om het publiek te selecteren dat u naar de bestemming wilt uitvoeren, dan selecteren **[!UICONTROL Next]**. Merk op dat slechts het potentiële publiek in deze mening wordt getoond, en geen ander publiek wordt getoond.

![Workflow voor het exporteren van gegevenssets waarin de stap Doelgroepen selecteren wordt weergegeven, waarin u kunt aangeven welk publiek in het vooruitzicht moet worden geëxporteerd.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Planning en volgende stappen

Voor de rest van het activeringswerkschema om perspectiefpubliek uit te voeren, lees het leerprogramma over het activeren van gegevens aan dossier-gebaseerde bestemmingen. Doorgaan vanaf het tabblad [exportstap voor doelgroep plannen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Merk op dat in de het plannen stap, het werkschema om perspectiefpubliek te activeren slechts u toestaat om [volledige bestanden exporteren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Incrementele bestandsexport wordt niet ondersteund.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->