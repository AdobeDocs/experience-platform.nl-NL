---
title: Soorten publiek van Audience Manager activeren door Uitgebreide activering
description: Leer hoe u het publiek van de Audience Manager activeert naar sociale en advertentiebestemmingen, via Uitgebreide activering van de Audience Manager.
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# Het publiek activeren via uitgebreide activering van Audience Manager

Deze pagina beschrijft de werkstroom van begin tot eind die u moet volgen om publiek van Audience Manager aan de bestemmingsplatforms te activeren die door Uitgebreide Activering worden gesteund.

## Voordat u begint {#before-you-begin}

De stappen die in deze gids worden beschreven veronderstellen u hebt gelezen [Overzicht van uitgebreide activering](overview.md) en u hebt bevestigd dat u aan de voorwaarden voor publieksactivering voldoet.

>[!IMPORTANT]
>
>Het publiek activeren via [!DNL Expanded Activation], zorg ervoor dat uw publiek van de Audience Manager op **gehashte e-mailadressen**. Zie de [voorwaarden](overview.md#prerequisites) voor meer informatie .

## Stap 1: Vorm de Audience Manager bronverbinding {#configure-source}

De [Audience Manager-bronaansluiting](../sources/connectors/adobe-applications/audience-manager.md) verzendt publieksgegevens die in Adobe Audience Manager zijn verzameld voor activering op de doelplatforms die worden ondersteund door Uitgebreide activering.

Volg de handleiding voor hoe u [een Audience Manager-bronverbinding maken](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) om uw bronschakelaar te vormen.

![De beeld van UI van het platform die het Bronlusje met de Audience Manager bronverbinding toont.](assets/sources-tab.png)

>[!TIP]
>
>De Adobe Audience Manager-bronaansluiting is de enige bronaansluiting die beschikbaar is in Uitgebreide activering.
>
>Als u een publiek wilt innemen op basis van aanvullende id&#39;s, moet u een editie van [Real-Time CDP](../rtcdp/overview.md). Neem voor meer informatie contact op met uw Adobe.

### Ingeten publiek weergeven en controleren {#view-audiences}

Het publiek dat u vanuit de Audience Manager naar de uitgebreide activering brengt, kunt u bekijken in het dialoogvenster **[!UICONTROL Audiences]** dashboard.

Ga naar **[!UICONTROL Customer]** -> **[!UICONTROL Audiences]** -> **[!UICONTROL Browse]**.

![Platform UI-afbeelding die de pagina Soorten publiek weergeeft.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Het kan tot 48 uur duren voordat het publiek volledig kan worden geactiveerd. Dit geldt ook voor updates van bestaande Audience Managers.
>* Nieuw gemaakt publiek van Audience Manager wordt niet automatisch weergegeven in Uitgebreide activering. Om nieuwe segmenten in Uitgebreide Activering in te voeren, moet u hen door de bronschakelaar van de Audience Manager toevoegen.

Nadat u uw bronschakelaar van de Audience Manager hebt gevormd, beweging aan [stap 2](#create-destination-connection).

## Stap 2: Een nieuwe doelverbinding maken {#create-destination-connection}

Voordat u het publiek van de Audience Manager naar keuze kunt sturen, moet u eerst een verbinding naar een doelplatform maken.

Ga in de linkerzijbalk naar **[!UICONTROL Connections]** -> **[!UICONTROL Destinations]** -> **[!UICONTROL Catalog]**.

De beschikbare doelcategorieën voor [!DNL Expanded Activation] zijn [reclame](../destinations/catalog/advertising/overview.md) en [sociaal](../destinations/catalog/social/overview.md).

![Platform UI-afbeelding die de doelcatalogus voor uitgebreide activering weergeeft.](assets/destination-catalog.png)

Als u een nieuwe verbinding met een doelplatform wilt maken, volgt u de handleiding op [hoe te om een nieuwe bestemmingsverbinding te creëren](../destinations/ui/connect-destination.md). Ga vervolgens naar [stap 3](#activate-audiences).

## Stap 3: Activeer publiek naar uw bestemming {#activate-audiences}

Nadat u [publiek van ingeslikte Audience Manager](#configure-source) en [een nieuwe doelverbinding gemaakt](#create-destination-connection), kunt u uw publiek nu activeren naar het doelplatform van uw keuze.

![Platform UI-afbeelding die de doelcatalogus voor uitgebreide activering weergeeft.](assets/activate-audiences.png)

Om publiek aan uw bestemming te activeren, volg de gids op [hoe te om publiek aan het stromen bestemmingen te activeren](../destinations/ui/activate-segment-streaming-destinations.md).

## Activering van publiek controleren {#verify}

Controleer de [doelcontroledocumentatie](../dataflows/ui/monitor-destinations.md) voor gedetailleerde informatie over hoe te om de stroom van gegevens aan uw bestemmingen te controleren.