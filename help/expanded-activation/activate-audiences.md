---
title: Audience Manager-soorten publiek activeren via uitgebreide activering
description: Leer hoe u het Audience Manager-publiek activeert naar sociale en advertentiebestemmingen via Audience Manager Expanded Activation.
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Soorten publiek activeren via uitgebreide Audience Manager-activering

Op deze pagina vindt u een beschrijving van de end-to-end workflow die u moet volgen om een publiek van Audience Manager naar de doelplatforms te activeren die worden ondersteund door Uitgebreide activering.

## Voordat u begint {#before-you-begin}

De stappen die in deze gids worden beschreven veronderstellen u de [ Uitgebreide het overzichtspagina van de Activering ](overview.md) hebben gelezen en u hebt bevestigd dat u aan de eerste vereisten voor publieksactivering voldoet.

>[!IMPORTANT]
>
>Om publiek door [!DNL Expanded Activation] te activeren, zorg ervoor uw publiek van Audience Manager op **gehakt e-mailadressen** gebaseerd is. Zie de [ eerste vereisten ](overview.md#prerequisites) voor meer details.

## Stap 1: De Audience Manager-bronverbinding configureren {#configure-source}

De [ bron van Audience Manager schakelaar ](../sources/connectors/adobe-applications/audience-manager.md) verzendt publieksgegevens die in Adobe Audience Manager voor activering in de bestemmingsplatforms worden verzameld die door Uitgebreide Activering worden gesteund.

Volg de gids op hoe te om [ een bron van Audience Manager verbinding ](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) tot stand te brengen om uw bronschakelaar te vormen.

{het beeld van 0} Experience Platform UI die het Bronlusje met de bron van Audience Manager verbinding toont.](assets/sources-tab.png)![

>[!TIP]
>
>De Adobe Audience Manager-bronaansluiting is de enige bronaansluiting die beschikbaar is in Uitgebreide activering.
>
>Als u publiek wilt opnemen dat op extra herkenningstekens wordt gebaseerd, moet u een uitgave van [ Real-Time CDP ](../rtcdp/overview.md) kopen. Neem contact op met uw Adobe-vertegenwoordiger voor meer informatie.

### Ingeten publiek weergeven en controleren {#view-audiences}

Het publiek dat u via Audience Manager naar de uitgebreide activering stuurt, kunt u bekijken op het dashboard van **[!UICONTROL Audiences]** .

Ga naar **[!UICONTROL Customer]** -> **[!UICONTROL Audiences]** -> **[!UICONTROL Browse]** om uw publiek weer te geven.

{het beeld van 0} Experience Platform UI die de pagina van het publiek toont.](assets/audiences-browse.png)![

>[!IMPORTANT]
>
>* Het kan tot 48 uur duren voordat het publiek volledig kan worden geactiveerd. Dit geldt ook voor updates voor bestaande Audience Manager-doelgroepen.
>* Nieuw Audience Manager-publiek wordt niet automatisch weergegeven bij Uitgebreide activering. Als u nieuwe segmenten wilt opnemen in Uitgebreide activering, moet u deze toevoegen via de Audience Manager-bronconnector.

Nadat u uw bron van Audience Manager schakelaar hebt gevormd, beweging aan [ stap 2 ](#create-destination-connection).

## Stap 2: Een nieuwe doelverbinding maken {#create-destination-connection}

Voordat u uw Audience Manager-publiek naar keuze kunt sturen, moet u eerst een verbinding met een doelplatform maken.

Ga in de linkerzijbalk naar **[!UICONTROL Connections]** -> **[!UICONTROL Destinations]** -> **[!UICONTROL Catalog]** .

De beschikbare bestemmingscategorieën voor [!DNL Expanded Activation] zijn [ reclame ](../destinations/catalog/advertising/overview.md) en [ sociaal ](../destinations/catalog/social/overview.md).

{het beeld van 0} Experience Platform UI die de bestemmingscatalogus voor Uitgebreide Activering toont.](assets/destination-catalog.png)![

Om een nieuwe verbinding aan een bestemmingsplatform tot stand te brengen, volg de gids op [ hoe te om een nieuwe bestemmingsverbinding ](../destinations/ui/connect-destination.md) tot stand te brengen. Dan, beweging aan [ stap 3 ](#activate-audiences).

## Stap 3: Activeer publiek naar uw bestemming {#activate-audiences}

Nadat u met succes [ hebt opgenomen Audience Manager publiek ](#configure-source) en [ creeerde een nieuwe bestemmingsverbinding ](#create-destination-connection), kunt u uw publiek aan het bestemmingsplatform van uw keus nu activeren.

{het beeld van 0} Experience Platform UI die de bestemmingscatalogus voor Uitgebreide Activering toont.](assets/activate-audiences.png)![

Om publiek aan uw bestemming te activeren, volg de gids op [ hoe te om publiek aan het stromen bestemmingen ](../destinations/ui/activate-segment-streaming-destinations.md) te activeren.

## Activering van publiek controleren {#verify}

Controleer de [ documentatie van de bestemmings controle ](../dataflows/ui/monitor-destinations.md) voor gedetailleerde informatie over hoe te om de stroom van gegevens aan uw bestemmingen te controleren.
