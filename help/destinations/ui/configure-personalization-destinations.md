---
keywords: personalisatie; doel; bestemming; personalisatiebestemmingen; vormen verpersoonlijkingsbestemmingen; dezelfde pagina; volgende bladzijde;
title: Vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Leer hoe te om verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking te vormen.
seo-description: Configure personalization destinations for same-page and next-page personalization.
source-git-commit: 24e8d088dd79304e0bf0335b7c3df2ef75baf81d
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 1%

---


# Vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking

## Overzicht {#overview}

Adobe Experience Platform gebruikt [randsegmentatie](../../segmentation/ui/edge-segmentation.md) om klanten toe te laten om publiekssegmenten tot stand te brengen en te richten op hoge schaal, in echt - tijd.

Met deze functie kunt u gebruiksgevallen voor personalisatie op dezelfde pagina en op de volgende pagina configureren.

Dit artikel verstrekt geleidelijke instructies op hoe te om Experience Platform en uw verpersoonlijkingsbestemmingen voor deze gebruiksgevallen te vormen.

## Stap 1: Een SDK-gegevensstroom voor het web van Experience Platforms configureren {#configure-datastream}

De eerste stap in het vormen van uw het gebruiksgeval van het verpersoonlijkingsgebruik is een [!DNL Web SDK datastream].

Volg de instructies in de [gegevensstroomconfiguratie](../../edge/fundamentals/datastreams.md) documentatie.

## Stap 2: Vorm uw verpersoonlijkingsbestemming {#configure-destination}

Nadat u uw gegevensstroom hebt gevormd, kunt u beginnen uw verpersoonlijkingsbestemming te vormen.

Volg de [zelfstudie over het maken van doelverbinding](../ui/connect-destination.md) voor gedetailleerde instructies op hoe te om een nieuwe bestemmingsverbinding tot stand te brengen.

Afhankelijk van de bestemming u vormt, verwijs naar de volgende artikelen voor bestemmings-specifieke eerste vereisten en verwante informatie:

* [Adobe Target-verbinding](../catalog/personalization/adobe-target-connection.md)
* [Aangepaste aanpassingsverbinding](../catalog/personalization/custom-personalization.md)

## Stap 3: Een [!DNL Active-On-Edge] samenvoegingsbeleid {#create-merge-policy}

Nadat u de doelverbinding hebt gemaakt, moet u een [!DNL Active-On-Edge] samenvoegbeleid.

Volg de instructies op [samenvoegingsbeleid maken](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)en zorgt ervoor dat de **[!UICONTROL Active-On-Edge Merge Policy]** schakelen.

## Stap 4: Nieuw segment maken in Platform {#create-segment}

Nadat u het [!DNL Active-On-Edge] samenvoegbeleid, moet u een nieuw segment in Platform tot stand brengen.

Volg de [segmentbuilder](../../segmentation/ui/segment-builder.md) gids om uw nieuw segment tot stand te brengen, en zorg ervoor [toewijzen](../../segmentation/ui/segment-builder.md#merge-policies) de [!DNL Active-On-Edge] samenvoegbeleid dat u in stap 3 hebt gemaakt.

## Stap 5: Activeer het segment aan uw bestemming

De laatste stap van het configuratieproces is het segment te activeren dat u bij stap 4 aan de bestemming creeerde die u bij stap 2 creeerde.

Volg deze [activeringszelfstudie](../ui/activate-profile-request-destinations.md).

## De configuratie valideren {#validate-configuration}

Nadat u de bovenstaande stappen met succes hebt uitgevoerd, ziet u de nieuwe segmenten in uw aanpassingsdoel.