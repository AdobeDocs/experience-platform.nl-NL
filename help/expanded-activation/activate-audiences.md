---
title: Soorten publiek van Audience Manager activeren door Uitgebreide activering
description: Leer hoe u het publiek van de Audience Manager activeert naar sociale en advertentiebestemmingen, via Uitgebreide activering van de Audience Manager.
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Het publiek activeren via uitgebreide activering van Audience Manager

Deze pagina beschrijft de werkstroom van begin tot eind die u moet volgen om publiek van Audience Manager aan de bestemmingsplatforms te activeren die door Uitgebreide Activering worden gesteund.

## Voordat u begint {#before-you-begin}

De stappen die in deze gids worden beschreven veronderstellen u de [ Uitgebreide het overzichtspagina van de Activering ](overview.md) hebben gelezen en u hebt bevestigd dat u aan de eerste vereisten voor publieksactivering voldoet.

>[!IMPORTANT]
>
>Om publiek door [!DNL Expanded Activation] te activeren, zorg ervoor uw publiek van de Audience Manager op **gehakt e-mailadressen** gebaseerd is. Zie de [ eerste vereisten ](overview.md#prerequisites) voor meer details.

## Stap 1: Vorm de Audience Manager bronverbinding {#configure-source}

De [ Audience Manager bronschakelaar ](../sources/connectors/adobe-applications/audience-manager.md) verzendt publieksgegevens die in Adobe Audience Manager voor activering in de bestemmingsplatforms worden verzameld die door Uitgebreide Activering worden gesteund.

Volg de gids op hoe te [ een Audience Manager bronverbinding ](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) tot stand brengen om uw bronschakelaar te vormen.

![ beeld UI van het Platform dat het Bronlusje met de Audience Manager bronverbinding toont.](assets/sources-tab.png)

>[!TIP]
>
>De Adobe Audience Manager-bronaansluiting is de enige bronaansluiting die beschikbaar is in Uitgebreide activering.
>
>Als u publiek wilt opnemen dat op extra herkenningstekens wordt gebaseerd, moet u een uitgave van [ Real-Time CDP ](../rtcdp/overview.md) kopen. Neem voor meer informatie contact op met uw Adobe.

### Ingeten publiek weergeven en controleren {#view-audiences}

Het publiek dat u via Audience Manager naar de uitgebreide activering stuurt, kunt u bekijken op het dashboard van **[!UICONTROL Audiences]** .

Ga naar **[!UICONTROL Customer]** -> **[!UICONTROL Audiences]** -> **[!UICONTROL Browse]** om uw publiek weer te geven.

![ beeld UI van het Platform dat de pagina van het publiek toont.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* Het kan tot 48 uur duren voordat het publiek volledig kan worden geactiveerd. Dit geldt ook voor updates van bestaande Audience Managers.
>* Nieuw gemaakt publiek van Audience Manager wordt niet automatisch weergegeven in Uitgebreide activering. Om nieuwe segmenten in Uitgebreide Activering in te voeren, moet u hen door de bronschakelaar van de Audience Manager toevoegen.

Nadat u uw Audience Manager bronschakelaar hebt gevormd, beweging aan [ stap 2 ](#create-destination-connection).

## Stap 2: Een nieuwe doelverbinding maken {#create-destination-connection}

Voordat u het publiek van de Audience Manager naar keuze kunt sturen, moet u eerst een verbinding naar een doelplatform maken.

Ga in de linkerzijbalk naar **[!UICONTROL Connections]** -> **[!UICONTROL Destinations]** -> **[!UICONTROL Catalog]** .

De beschikbare bestemmingscategorieën voor [!DNL Expanded Activation] zijn [ reclame ](../destinations/catalog/advertising/overview.md) en [ sociaal ](../destinations/catalog/social/overview.md).

![ beeld UI van het Platform die de bestemmingscatalogus voor Uitgebreide Activering tonen.](assets/destination-catalog.png)

Om een nieuwe verbinding aan een bestemmingsplatform tot stand te brengen, volg de gids op [ hoe te om een nieuwe bestemmingsverbinding ](../destinations/ui/connect-destination.md) tot stand te brengen. Dan, beweging aan [ stap 3 ](#activate-audiences).

## Stap 3: Activeer publiek naar uw bestemming {#activate-audiences}

Nadat u met succes [ ingebed Audience Manager publiek ](#configure-source) en [ een nieuwe bestemmingsverbinding ](#create-destination-connection) hebt gecreeerd, kunt u uw publiek aan het bestemmingsplatform van uw keus nu activeren.

![ beeld UI van het Platform die de bestemmingscatalogus voor Uitgebreide Activering tonen.](assets/activate-audiences.png)

Om publiek aan uw bestemming te activeren, volg de gids op [ hoe te om publiek aan het stromen bestemmingen ](../destinations/ui/activate-segment-streaming-destinations.md) te activeren.

## Activering van publiek controleren {#verify}

Controleer de [ documentatie van de bestemmings controle ](../dataflows/ui/monitor-destinations.md) voor gedetailleerde informatie over hoe te om de stroom van gegevens aan uw bestemmingen te controleren.
